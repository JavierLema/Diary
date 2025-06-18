---
tags: [__JIRA Tickets]
title: RFE matching algorithm - RFE-20729
created: '2025-05-07T08:11:53.195Z'
modified: '2025-05-12T05:06:07.782Z'
---

# RFE matching algorithm - RFE-20729

<details>
  <summary>cbe.06-07-0173_cccv2_0000001_pubType-1-</summary>
    
  #### FindBestMatch
  - string stdNum, 
  - string eStdNum, **"19317913"** 
  - ContentTitleList parentTitles, **"CBE—Life Sciences Education"**
  - string group1, 
  - string group2, **"4"**
  - DateCode pubDate, **"{12/1/2006}"**
  - Pages pages, **"315"**
  - string title, **"RESPONSE:Re: The Use of a Knowledge Survey as an Indicator of Student Learning in an Introductory Biology Course"**
  - string doi, **"10.1187/cbe.06-07-0173"**
  - Genres genre, **"article"**
  - bool loadIds **"true"**

  ##### Calculate fields: group1, group2, pages, pubdates
  - **Group1**: ''
  - **Group2**: '4'
    + State.ImpRec.JournalIssue ```<issue>4</issue>```
    + State.ImpRec.JournalIssue ((genre == Genres.article) && !string.IsNullOrEmpty(State.ImpRec.JournalIssue))
  - **Pages**: '315-315'
  - **Pages**: ''

  #### Candidates

  - Match on Prepub if Title available =>  (contentTitle != Empty) => **return 0 results**
  - Search articles by DOI (articles, AppState.GetSettingAsBool("MatchDOIFirst", true, true), doi != Empty) => **0 results**
  - Match on Group1, Group2, Year, Page (group1 or group2 != empty) => **return 0 results**

  Lookup publications => Fill State.DBPub

  #### Final result
  Insert a new article => 179614392

</details>

<details>
  <summary>cbe.06-07-0174_cccv2_0000001_pubType-1-</summary>

  #### FindBestMatch
  - string stdNum, 
  - string eStdNum, **"19317913"** 
  - ContentTitleList parentTitles, **"CBE—Life Sciences Education"**
  - string group1, 
  - string group2, **"4"**
  - DateCode pubDate, **"{12/1/2006}"**
  - Pages pages, **"315-316"**
  - string title, **"RESPONSE:Re: The Use of a Knowledge Survey as an Indicator of Student Learning in an Introductory Biology Course"**
  - string doi, **"10.1187/cbe.06-07-0174"**
  - Genres genre, **"article"**
  - bool loadIds **"true"**

  ##### Calculate fields: group1, group2, pages, pubdates
  - **Group1**: ''
  - **Group2**: '4'
    + State.ImpRec.JournalIssue ```<issue>4</issue>```
    + State.ImpRec.JournalIssue ((genre == Genres.article) && !string.IsNullOrEmpty(State.ImpRec.JournalIssue))
  - **Pages**: '315-316'
  - **Pages**: ''

  #### Candidates

  - Match on Prepub if Title available =>  (contentTitle != Empty) => **return 0 results**
  - Search articles by DOI (articles, AppState.GetSettingAsBool("MatchDOIFirst", true, true), doi != Empty) => **0 results**
  - Match on Group1, Group2, Year, Page (group1 or group2 != empty) => **return 1 candidate**
  - DetermineBestCandidate -> determine a newRank => 100
    - AcceptableFuzzyMatch => if rank == 100 return true.


  Lookup publications => Fill State.DBPub

  #### Final result 
  Merge with existing article.
  

</details>


<details>
  <summary>Investigation</summary>

  - After talk with Greg, he sent me this document url: https://docs.google.com/document/d/1o9C-PZ2o5qdS4CfRgGG9HlHEiiM6uD0iSaGpdj6Oyhs/edit?tab=t.0. 
  - To start this investigation I start read this document at **Article Import - Find best match method - Match Parent Pub Date Page** section
  - After conversation with Jennifer Lockfort she say this:

      It is a publisher feed that runs through the feeds team's template producing CCCXML that we configure RFE to pick up via FTp
      **The CCCXML8.0.1 files are a CCC creation** based off of metadata files provided by the publisher on a trickle-through basis
      RFE is set to look for it every day but deliveries usually aren't daily
 
  ### Library content import process
  - ArticleImportJP
    + Run()
    + DoArticleImport()
  - ProcessRecord()
  - LookupImportArticle()
  - ImportApprovalContentDBSelectCommand.FindBestMatch()

</details>
