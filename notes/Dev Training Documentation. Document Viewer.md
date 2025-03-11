---
tags: [Dev Training]
title: Dev Training Documentation. Document Viewer
created: '2022-10-11T14:32:29.420Z'
modified: '2024-11-05T08:51:34.326Z'
---

# Dev Training Documentation. Document Viewer
https://docs.google.com/document/d/13dTqFDus6GXri8tPEtkgDhnNOiG36gNNIbCtPrVafZs/edit#
___

## About
When the user click on MyLibraries element access the Document Viewer, where you encounter three different scenarios:
- Linkout: -> The documento it's linked to another page leave on CCC
- Item of interest -> You need order this items to view. Wishlist.
- PDF Document -> You can see the document.
    + You can add/edit annotations
    + You can show a history changes (Audit trail)


## General Classes.
- mylibrary.aspx.cs
- LibraryDocument.cs
- documentViewer.aspx.cs
- editdocument.aspx.cs

### Review Section
- DocumentRatingInfo reviewInfo = DocumentRatingInfo.FetchDocumentRatingInfo(_id, Db);
`
SELECT S.LibraryDocumentId, S.AverageRating, S.NumRatings FROM LibraryDocumentStatsSummary S WITH (NOLOCK) WHERE S.AverageRating > 0 AND S.LibraryDocumentId  IN ({0}) ORDER BY S.LibraryDocumentId
`
- List<LibraryDocumentRating> reviews = LibraryDocumentRating.GetRatingsForDocument(_id, Db);
`
SELECT LibraryDocumentRatingId, LibraryDocumentId, UserId, Rating, Review, Title, RatingTime FROM LibraryDocumentRating WITH (NOLOCK) WHERE LibraryDocumentId = {0} ORDER BY RatingTime DESC
`
- decimal averageRating = (reviewInfo == null) ? 0 : reviewInfo.Ratings;
- Read History
`
SELECT DISTINCT(U.Email) FROM LibraryDocumentReadHistory H WITH (NOLOCK) JOIN AppUser U WITH (NOLOCK) ON H.UserId = U.UserId WHERE H.LibraryDocumentId = {0}
`

### Example.

- Event Onclick for the documents on your library: showDocument(100058091, event, 66273474)
    + getdocument.aspx?inframe=yes&docId=100041562&action=annots&docIdForAnnotations=100058091

`SELECT LibraryId FROM LibraryDocument WITH (NOLOCK) WHERE LibraryDocumentId = 100058091`

`select * from Content where ContentId = 66273474`

`SELECT Citation FROM CitationCache WITH (NOLOCK) WHERE ContentId = 66273474`

`SELECT 
	C.ContentId, C.PartOfContentId, C.Title, C.TitleLanguage, C.StdNum, C.EStdNum, C.DOI, C.Genre, C.Language, C.SubjectAreaId, 
	C.Group1, C.Group2, C.Group3, C.Pages, C.StartDateCode, C.EndDateCode, C.Author, C.Publisher, C.ClientId, C.TrustLevel, C.SourceCollection, 
	C.Status, C.Scope, C.Popularity, C.Flags, C.CreatedTime, C.LastUpdate, PubDates = dbo.GetContentPubDates(C.ContentId), C.TitleLastUpdate, 
	C.Subtitle, C.HasAbstract, C.HasFullText, C.DateCode1, C.DateCode2, C.ContentOptions, C.Caption 
    FROM Content C WITH (NOLOCK) 
	WHERE C.ContentId = 66273474`

`SELECT * FROM ContentAltId WITH (NOLOCK) WHERE ContentId = 66273474`

`SELECT LibraryFieldSetId, ClientId, Name, Description, Icon 
	FROM LibraryFieldSet WITH (NOLOCK) WHERE LibraryFieldSetId = (SELECT FieldSetId FROM Library WHERE LibraryId = 69268)`

`SELECT A.LibraryDocumentAnnotationId, A.LibraryDocumentId, A.UserId, A.Type, A.Text, A.Page, A.CreatedTime, A.ModifiedTime, A.Properties, A.Status, U.Email 
	FROM LibraryDocumentAnnotation A WITH (NOLOCK) 
	LEFT OUTER JOIN AppUser U WITH (NOLOCK) ON A.UserId = U.UserId 
	WHERE 
		A.LibraryDocumentId = 100058091  AND A.Type IN (1) AND A.Status = 0 ORDER BY A.Page DESC, A.ModifiedTime ASC`
