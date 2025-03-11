---
tags: [Dev Training]
title: Dev Training Documentation. ACL API
created: '2022-08-18T08:25:46.921Z'
modified: '2024-11-05T08:51:34.226Z'
---

# Dev Training Documentation. ACL API

##### https://docs.google.com/document/d/1OEX4snn4aEz5Cd-Hxl-azN6tsRgyRl6Uw9MvaiqYYws/edit#heading=h.lnxbz9

*****************************
## Referral classes and methods
1. **CCCLookup**
    - **CheckRights**: Returns the permissions available for the citation
        - **FormatCCCAclApiURL**: Make a correct format on a URL before call ACL API
        - **InternalCheckRights**: Is the method finally calls the ACL API to return the permissions of the citation.
            - **GetBestMatch**: This method determine the results are good match or not.
2. **ClearanceResults**
    - **DoACLLookup**:Determines if the citation is covered by the ACL license 

*****************************
## Questions

- What it's the procedure to create a CCC ACL Collection inside a Client?
    https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/collections-holdings-libraries


*****************************
## Possible Errors

        
- If I configured my app.config with RFEConfig => "JobServer (JLema)", after create on RFE dev, the
    application crashed with this exception:
        configuration.CasServerUrlPrefix is null or empty >>> https://sco.aws-p-dev.copyright.com/cas/
- If I configured with RFEConfig => Vlib RFE Running but the JobTester crasched with this exception:
        System.TypeInitializationException: 'The type initializer for 'DataEncryptor' threw an exception.'
        An error occurred loading a configuration file: The network path was not found. (\\win-rfe-dev\rfedev\data\_configFiles\DataEncryptor.config)
    
****************************************************
## Proposed challenges and Key points

### STEPS.
==========
1. Create a client with the option Copy. 
2. Impersonate client
3. Add CCC ACL to this client:
    1. Manage My Company Account
    2. Manage Collections
    3. New -> In Tab Type select "CCC ACL"
4. To show Holdings in this section. View menu - select holdings

### Search for an existing order that has cleared from a CCC ACL collection. 
    5. Over menu Manage Orders select an Order -> 5484884

#### Use the job tester to check what the CCC ACL API returns for that particular order.
6- Create a new method TestGetOrder

    using (DbContext db = new DbContext())
    {
        OrderItem order = OrderItem.Get(orderId, db);
        if (order != null)
        {
            var cleResult = new ClearanceResults(order, 0, null);
            Copyright2 rights;
            string crTerms;
            cleResult.DoACLLookup(out rights, out crTerms);
        }
    }


#### Find the publication’s WorkId by debugging the CCC ACL responses and try to find it in RightFind Advisor.
    If you don't have a RightFind Advisor account create one.
    The Analysis and control of less-desirable flavors in foods and beverages with workId 122883898 

#### Check if the rights in Rightfind Advisor match the rights you find CCC ACL API response.
    with permissions DIGITAL,PRINT,REACTIVELY_SHARE,SELF_USE_TRANSLATION_RIGHT,NGT_PHOTOCOPY

### Search for any journal article that belongs to the journal “Archives of environmental health” and locate the contentId of said journal article.
    Publisher: Heldref Publications Publication Date: 1960 - 2005
    ISSN: 23314303
    LCCN: 62003872 OCLC: 1513869 Catalog ID: 2232
    R/C/S 100/41.6666666666667/Semantic

#### Use the Job Tester to find out the rights that CCC ACL API returns for said citation.
Multiple forms to get de contentId of one article on this journal:
1. On URL: https://rfe.aws-rfe-dev.copyright.com/vlib/order/ordersearch.aspx?q=true&mode=TOC&ContentId=***2232***&b=cached&userid=1098530&Genres=1
2. Development Tools os webbrowser and examine de HTML Code.
3. BBDD: Make this Query:
>       select * from Content where ContentId = 2232 or PartOfContentId = 2232

4. Select de first registry 
>   using (DbContext db = new DbContext())
>    {
>        var citation = Content.GetCitation(11026534, db);
>    }

#### Find another Journal Article belonging to the same Journal.
* Repeat stepts from the previous point
 
#### Use the Job Tester to find out the rights for that new Journal Article.
* Repeat stepts from the previous point

#### Try to figure out why the Rights returned by CCC ACL API for both articles match or don’t match.
* Find rights for article with ContentId: 11026534
    DIGITAL,PRINT,REACTIVELY_SHARE,SELF_USE_TRANSLATION_RIGHT,NGT_PHOTOCOPY
* Find rights for article with ContentId: 11026535
    DIGITAL,PRINT,REACTIVELY_SHARE,SELF_USE_TRANSLATION_RIGHT,NGT_PHOTOCOPY
* All responses are the same because the rights finding by the same key: cACL-2232-2001-US (Journal Key)
    public enum Genres : short >> Types of contents
    The method IsLeafGenre on Citation defines if a content or ar part of content.
    The Key is made in CCCLookup.cs:236
    string key = string.Format("c{0}-{1}-{2}-{3}", account, citation.IsLeafGenre() ? citation.PartOfContentId : citation.ContentId, citation.PublicationYear, country);

### Find any content and use the Job Tester to check the CCC ACL API rights in any way you prefer.
#### Find where the specific API response and try to predict if the matching algorithm will get a good match or not.
#### After that, verify your prediction by debugging the GetBestMatch method
CCCLookup.cs:InternalCheckRights
Request: https://api.copyright.com/dp/1.0/publication/permissions.json?standardNumber=978-0-12-169065-6&location=US&standardNumberType=isbn&pubdate=1980
Response JSON: 448
* GetBestMatch method
    - remove all spaces, '()', '{}', '[]'
- Where are configured value of MinTitleRank?
- To comparer used a StringRelativeComparer class
- When call API to get OrderId, this return a citation on field RefCitXml, this field is part of table OrderItem. 
Citation it's necesary to methods:
+ cleResult.DoCCCLookup(CCCAccount.ACL, out rights, out crTerms, out grants, out workId);
+ cccLookup.CheckRights(cit, "US");

**The properties start with Part are Parents**
