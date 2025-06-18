---
attachments: [Clipboard_2025-05-14-13-40-57.png, Clipboard_2025-05-27-10-27-53.png]
tags: [__JIRA Tickets]
title: RestAPI
created: '2025-05-14T08:13:26.263Z'
modified: '2025-05-27T08:27:53.552Z'
---

# RestAPI

<details>
  <summary>Differents results</summary>

  Darya Question:

  > For example: 
    P_DEV (fspadmin@cscmtest.com) 
      If I search for query 
        "(genre:2 OR genre:17 OR genre:19 OR genre:7) AND (doi:10.1016/j.annepidem.2025.02.004)" => Receive empty result. 
      But for query 
        "(genre:2 OR genre:17 OR genre:19 OR genre:7) AND (doi:10.1078/0940-2993-00349)" => Result is returned

  The answer for this is simple:
  > The scope is different. For the first one is **Scope=0** public and the others is **3** library

  ![](@attachment/Clipboard_2025-05-27-10-27-53.png)

</details>



<details>
  <summary>Configuration</summary>

  https://rfe.aws-rfe-dev.copyright.com/restapi/v1/token?username=API_client_admin@copyright.com&password=kanlegi30z!2

  Change password:
  ![](@attachment/Clipboard_2025-05-14-13-40-57.png)

</details>


<details>
  <summary>RFE-20910. [RFLR] Search by DOI does not return expected result</summary>
  ### Conclusion
  - The query method accepts multiple parameters to search
    - But can't find in libraries when the current user are not member.
  - The documents API method do not check if duplicates by DOI, title,... only by contentId

  - We will try to convert into deprecate method API citation


  ####Requests to get
  ```
    https://rfe.aws-rfe-dev.copyright.com/restapi/v1/token?username=fspadmin%40cscmtest.com&password=Zxk56LjQuT, Method=GET
    https://rfe.aws-rfe-dev.copyright.com/restapi/v1/Library/shared?User=ssae_autotests_user@copyright.com , Method=GET
    https://rfe.aws-rfe-dev.copyright.com/restapi/v1/Search/query, Method=POST, Request={"search":"(genre:2 OR genre:17 OR genre:19 OR genre:7) AND (doi:10.1016\\/j.annepidem.2025.02.004)"}
  ```

  ####Requests to post
  ```
    https://rfe.aws-rfe-dev.copyright.com/restapi/v1/token?username=fspadmin%40cscmtest.com&password=Zxk56LjQuT, Method=GET
    https://rfe.aws-rfe-dev.copyright.com/restapi/v1/Library/documents?User=ssae_autotests_user@copyright.com, Method=POST, Request={"title":"Higher prevalence of long COVID observed in cancer survivors: Insights from a US nationwide survey","libraryId":71580,"duplicateHandling":"ByContentId","documentCitation":{"genre":"article","title":"Higher prevalence of long COVID observed in cancer survivors: Insights from a US nationwide survey","authors":["Wang L.","Yang W."],"partOfTitle":"Annals of Epidemiology","entityIds":{"issn":"18732585; 10472797","isbn":"","pmid":"39947498","doi":"10.1016/j.annepidem.2025.02.004"}},"docLink":"https://www.embase.com/records?id=L2037455788"}
  ```

  ####Process
  - Create content steps
    + Get Token 
    + **RFERestAPI.Middleware** -> **UserImpersonationMiddleware** -> InvokeAsync
      This method check the security. For example, if you get the token with RESTAPI user the clientId is different and throw an exception.
    + **LibraryController** -> [HttpPost("documents")] **SuccessResponse**
      - Check if the title is empty
      - Check max doc size --> IsDocSizeValid
      - If the request contains a libraryId --> **AddDocumentToSharedLibrary**
        - Check if this client can access to this library
        - Find duplicates -> Depends the parameter DuplicateHandling and the contentId parameter
        - LibraryDocument.InsertItemOfInterest
          - DocumentType = LibraryDocumentType.Publication
          ```
          {
              "result": {
                  "libraryDocumentId": 102263547
              },
              "status": "Success"
          }
          ```

      

</details>

