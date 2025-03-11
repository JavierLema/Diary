---
tags: [Dev Training]
title: 'Dev Training Documentation. Collections, Holdings and Libraries'
created: '2022-10-25T14:41:56.915Z'
modified: '2024-11-05T08:51:34.296Z'
---

# Dev Training Documentation. Collections, Holdings and Libraries
https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/collections-holdings-libraries
https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/rro-license
___

## Collection: 
Is used to refer to any set of related content. For example: publisher subscription, a print library, a digital repository,...

### IMPORTANT ### 
When you create a new query, not only in this case, you need check record status:
- ```public enum RecordStatus : short { Unknown = -1, Active = 0, PendingDelete = 1, Deleted = 2, PendingMerge = 3, Inactive = 4, DBDelete = 5, Template = 100 };```

### Collections types and related queries
When you enter in a https://www.test.rightfind.com/vlib/collections/collections.aspx you can see a gridview with 1251 items. This is the result of this query:
``select CollectionId, CollectionName, Type as CollectionType from Collection with(nolock) where ParentCollectionId = 0 and Status <> 1 and ClientId = 0 and CollectionId > 0``

- **Regular Collections** => **CollectionType = 0**
    + ``select CollectionId, CollectionName, Type as CollectionType from Collection with(nolock) where ParentCollectionId = 0 and Status <> 1 and ClientId = 0 and CollectionId > 0 and Type = 0``

- **Regular Subcollections** => **ParentCollectionId = CollectionId**
    + ``select * from Collection with(nolock) where collectionid = 9677 or ParentCollectionId = 9677 order by CollectionId asc``

- **Publisher Collections** => **CollectionType = 1**
    +   ``select CollectionId, CollectionName, Type as CollectionType from Collection with(nolock) where ParentCollectionId = 0 and Status <> 1 and ClientId = 0 and CollectionId > 0 and Type = 1``

- **Publisher subcollections** => **ParentCollectionId = CollectionId**
    + ``select CollectionId, CollectionName, Type as CollectionType, * from Collection with(nolock) where collectionid = 99 or ParentCollectionId = 99`` => **Elsevier Ltd.**

- **Client Subscription collections**
    + 34627	Mary Ann Liebert, Inc.
    
- **Client Token collections**
    + 34898	Mary Ann Liebert Tokens

- **Repository (Digital Library) collections**

- **Shared Library collections**

- **RRO Collections (Reproduction Rights Organization)**

- **Named Collection**


## Holding
Holdings are the individual content items that are part of the collection

## Fulfillment Collections
The fulfillment collection (or fulfillment source) is used to determine where RightFind Enterprise can obtain a copy of the content requested by the user.

### Fulfillment sources
- **Client Digital Library**: RightFind Enterprise stores documents ordered by the client in the digital library if the content is covered by an RRO license and storage in a digital library is not prohibited by the rights holder.
- **Client Shared Libraries**: RightFind Enterprise stores documents delivered to users in the user’s personal library. The users can then share these documents in one or more shared libraries. Users may also place orders in which these documents are sourced from the shared library if the user has already purchased rights to the document (meaning the document exists in the user’s personal library).
- **Client Subscription/Token Collections**: Clients often purchase subscriptions to content from publishers that gives the client rights to access this content. In this case, staff create a client subscription or token collection for the client that contains the holdings for the content the client can access.
- **Global publishers collections**: These collections are typically configured to download content directly from a publisher’s web site.
- **Service API collections**: The British Library supports an API that allows requesting documents that may be either automatically or manually fulfilled. RightFind Enterprise initially uses the API to determine the availability of the content. If the content is available, RightFind Enterprise uses the API to place an order and periodically polls the API until the document is available. Once the document is available, RFE downloads the document via the API and passes off the order to the fulfillment/delivery process.
- **Work Item**: Some fulfillment sources (University of California-Los Angeles, University of Michigan, National Library of Medicine, etc.) require manual fulfillment and are sent to a manual fulfillment queue that is managed by ARS staff. These orders are then passed on to remote staff located at the library that use the library’s resources to obtain a copy of the document.
- **No Fulfillment**: If RightFind Enterprise cannot find a viable fulfillment source for an order, the order is sent to a work queue for manual clearance and/or fulfillment. In some cases, ARS staff may be able to correct information in the citation or holding and send the order back to automatic fulfillment or may locate and purchase the document from a publisher or a third-party vendor.


## Clearance Collections
The clearance collection (or clearance source) is used to determine the rights available, the cost of the content (usually a PDF file), and the entity Copyright Clearance Center must pay for using the content.

### The clearance sources 
- **RRO License**: Publishers may grant a license to reuse content stored in a digital library through a Royalty Rights Organization such as CCC’s Annual Copyright License (ACL), Multinational Copyright License (MCL), JAC DCL (Japan), or VG WORT in Germany; or the Copyright Licensing Agency (CLA) in London.
    + The field RROLicenseType it's a child of a Type RRO with value 4 
    + **Collection.Type** => public enum CollectionType : short { Unknown = -1, Regular = 0, Publisher = 1, Repository = 2, SharedLibrary = 3, RRO = 4 };
    + **Collection.RROLicenseType** => public enum RROLicenseType { None = 0,ACL = 1,VGWORT = 2,CLABusiness = 3,CLAMultinationalBusiness = 4,CLAPharmaceutical = 5,JAC = 6 }
    
- **Client Subscription Collection**: The client has already paid the publisher for rights to use the content so RFE verifies the user has rights to the content and has access to the client subscription collection.
- **Client Token Collection**: The client purchases a block of “tokens” and the publisher decrements the client’s available token count each time the client (or RFE on behalf of the client) accesses content on the publisher’s web site. Note that you should not attempt to source content from a client token collection without explicit permission because the client must pay to access these documents.
- **Global Publisher Collection**: RightFind Enterprise calculates the copyright fee the client pays to the Copyright Clearance Center and the copyright payment that CCC owes to the publisher for rights to use the content.
- **Copyright Cleared Vendor**: RightFind Enterprise pays the vendor a copyright fee and possibly a transaction and fulfillment fee for the document. The vendor is responsible for paying the publisher for rights to use the content.

### Examine the code:
- If you are a RFE Admin    -> customCategories = CollectionCategory.GetCustom(Db);
    - SELECT * FROM CollectionCategory WHERE Custom = 1 AND ClientVisible = 0 ORDER BY DisplayOrder =>> Regular Collection, Regular Sub-Collection
- If you are a RFE Client   -> customCategories = CollectionCategory.GetClientCustom(Db);
    - "SELECT * FROM CollectionCategory WHERE Custom = 1 AND ClientVisible = 1 ORDER BY DisplayOrder"; =>> Custom, Custom Sub-Collection
- Base collections
    - SELECT CollectionName, CollectionId, Type, RROLicenseType FROM Collection WITH (NOLOCK) WHERE ClientId = 0 AND MembershipCollectionId < 0 AND CollectionId > 0 AND Status = 0
