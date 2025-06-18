---
tags: [HowTo]
title: HOWTO check how many records are affected
created: '2025-05-12T08:11:13.329Z'
modified: '2025-05-12T08:49:22.767Z'
---

# HOWTO check how many records are affected

https://ccc.atlassian.net/browse/RFE-12231
```
SET NOCOUNT ON
DECLARE @tblContentIdAffected TABLE (id INT PRIMARY KEY)
DECLARE @tblHoldingIdAffected TABLE (id INT PRIMARY KEY)
/* 
STEPS 
1- You only have a holdingIds
    a - Calculate contentId's affected
    b - Replace your calculate HoldingIds into a script comment <HoldingIdAffected> 
    c - Replace your calculate ContenctIds into a script comment <ContentIdAffected> 
2- You only have a contentIds
    - Go to step 1.b
3- You have holdingIds and contentId's
    - Go to step 1 
    - Go to step 2
*/
DECLARE @EndTime datetime
DECLARE @StartTime datetime 
SELECT @StartTime=GETDATE() 
DECLARE @TotalRecordsToIndexed INT = 0
DECLARE @TotalLibraryDocsToIndexed INT = 0
INSERT INTO @tblHoldingIdAffected
 SELECT DISTINCT(ContentId) FROM Holding WITH(NOLOCK) WHERE HoldingId in 
    --('<HoldingIdAffected>')
/* For example: (183598225,182080654,178131964,176923672,177101949,61336788,181991562,183845154,183845416,183845276)*/
INSERT INTO @tblContentIdAffected
 SELECT DISTINCT(contentId) FROM Content WITH(NOLOCK) WHERE contentid IN  
    --('<ContentIdAffected>')
/* For example: (183598225,182080654,178131964,176923672,177101949,61336788,181991562,183845154,183845416,183845276)*/
DECLARE @contentId TABLE (contentId INT PRIMARY KEY)
    INSERT INTO @contentId
        SELECT contentId FROM Content c WITH(NOLOCK) 
            WHERE 
                ContentId IN (SELECT DISTINCT(id) FROM @tblContentIdAffected) 
                OR ContentId IN (SELECT DISTINCT(id) FROM @tblHoldingIdAffected)
                OR PartOfContentId IN (SELECT DISTINCT(id) FROM @tblContentIdAffected) 
                OR PartOfContentId IN (SELECT DISTINCT(id) FROM @tblHoldingIdAffected)
SET @TotalRecordsToIndexed += (SELECT COUNT(DISTINCT(contentId)) FROM @contentId)
SET @TotalLibraryDocsToIndexed = (SELECT COUNT(DISTINCT(c.ContentId)) FROM Holding h WITH(NOLOCK)
    JOIN Collection col ON col.CollectionId = h.CollectionId
    JOIN Content c ON h.ContentId = c.ContentId
    WHERE col.Type = 3 AND
        c.ContentId IN
            (SELECT DISTINCT(contentId) FROM @contentId))
SET NOCOUNT OFF
PRINT 'Predicts the number of records reindexing'
PRINT '================================================================'
PRINT 'Total Content to Indexing: ' + CAST(@TotalRecordsToIndexed AS VARCHAR)
PRINT 'Total Library document to Indexing: ' + CAST(@TotalLibraryDocsToIndexed AS VARCHAR)
SELECT @EndTime=GETDATE()
--This will return execution time of your query
DECLARE @TotalTime INT = (SELECT DATEDIFF(ms,@StartTime,@EndTime))
PRINT CHAR(13)+CHAR(10) + CHAR(13)+CHAR(10)
PRINT '= Total execution time(ms): ' + CAST(@TotalTime AS VARCHAR)
PRINT '================================'
SET NOCOUNT ON
```
