---
tags: [Dev Training]
title: Dev Training Documentation. My Libraries.
created: '2022-10-04T07:56:31.911Z'
modified: '2024-11-05T08:51:34.445Z'
---

# Dev Training Documentation. My Libraries.
https://docs.google.com/document/d/1QiF15Ik72S5MsnwuGOK8edPApsPA1rr8IxwBFffyYWY/edit#
___

## About
You can access to this option in this URL: vlib/library/librarymgt.aspx but this option filtered libraries with clientId = 0
Libraries are the collection for user content. RFE has these types:
- Digital -> Not standar library.
- Personal -> All content that the client purchased.
- Shared -> All content that the client shared.


****Enable for a clients. Only with RightFind Enterprise products.****
- Select a client,
- edit your product options 
- check Modules to be enabled.


## General Classes
* LibraryDocument.cs
    - LibraryDocumentDBSelectCommand, LibraryDocumentDBInsertCommand, LibraryDocumentDBUpdateCommand.
    - LibraryDocumentAggregationTag and LibraryDocumentAggregationNoTag derived from ContentSearchAggregation class.
* LibraryTag.cs
* LibraryMember.cs
* LibraryDocumentTag.cs
* LibraryDocumentAnnotation.cs
* LibraryDocumentRating.cs

### My libraries classes and my libraries search classes. 
***IMPORTANT*** The capability to search and filter using the semantic vocabularies defined in the shared library.
* MyLibrary.aspx.cs
    * LibrarySearchBase -> abstract
    * LibrarySearchElastic: LibrarySearchBase 
    * ElasticHighting 
* librarymgt.aspx.cs
* sharedlibdlg.aspx.cs -> Edit library content/users,...


### Database Schema
- Library. Main table for storing all libraries regardless of their type: Digital, Shared…
- LibraryDocument. Store documents.
- LibraryDocumentTag. Tags for each document.
- LibraryDocumentRating. All information related to document ratings.
- LibraryDocumentStatsSummary. Statistics about rating, reviews, comments per document.
- LibraryMember. Store the membership relations between users and libraries.
- LibraryTag. Existing tag for each library.

## Proposed challenges and Key points
- Debug MyLibrary Search results. 
    
- Tag matching in Search results.
- Semantic topics highlighting.
