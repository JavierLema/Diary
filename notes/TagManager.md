---
tags: [__JIRA Tickets]
title: TagManager
created: '2025-02-10T11:22:26.323Z'
modified: '2025-02-11T10:29:47.852Z'
---

# TagManager

<details>
  <summary>Tags and documents relationship</summary>

  - Shared Libraries.
    + **FetchLibraryTags**
      + When you click on Manage tags at personal library, the results contains all tags for this user and for libraryId = 0
      + When you click ... the results on this popup contains the same results that the previous.
      + You can modify any tag on any selected library. This is right?

  - LibraryController - LibraryDocument.DeleteAllTags(...)
  - DocumentViewerController - DeleteAllTags(request.DocumentId, Db)
  - LibraryDocumentDbUpdateCommand - DeleteAllTags(...)

</details>

## Possible solutions

<details>
  <summary>Dapper - Requires PoC or Spike</summary>

  - https://www.learndapper.com/bulk-operations/bulk-insert
  - https://www.learndapper.com/bulk-operations/bulk-update
  - https://www.learndapper.com/bulk-operations/bulk-delete
  - https://www.learndapper.com/dapper-query/selecting-multiple-results

</details>

<details>
  <summary>Table variable or temporay table</summary>

  ```
  update 
    sometable
  set  
    x = v.value
  from 
    (values (a, b), (c, d), (e, f)) v(id, value)
  where 
    sometable.id = v.id;
  ```
  ```
    UPDATE t
      SET Field1 = v.Field1
      FROM dbo.MyTable t JOIN
          (VALUES (95, 348923),
                  (90, 348924),
                  (100, 348925)
          ) v(Field1, MyTableId)
          ON v.MyTableId = t.MyTableId;
  ```

</details>

<details>
  <summary>Usign OUTPUT on SQL Queries</summary>

  - Insert/update/delete tags at once time.
  ```
  private IEnumerable<LibraryTag> CreateTags(IEnumerable<TagItem> tags)
  {
    List<LibraryTag> result = new List<LibraryTag>();
    using (DbCommand cmd = _db.CreateCommand())
    {
      cmd.CommandText = "INSERT INTO LibraryTag (LibraryId, Tag, UserId) ";
      cmd.CommandText += "OUTPUT inserted.LibraryTagId, inserted.LibraryId, inserted.UserId, inserted.Tag ";
      cmd.CommandText += "VALUES ";
      cmd.CommandText += string.Join(", ", tags.Select((_, index) => $"(@LibraryId{index}, @Tag{index}, @UserId{index})"));

      foreach (var tag in tags.Select((x, i) => new { Value = x, Index = i }))
      {
        cmd.AddParameter($"@LibraryId{tag.Index}", DbType.Int32, _libraryId);
        cmd.AddParameter($"@UserId{tag.Index}", DbType.Int32, _userId);
        cmd.AddParameter($"@Tag{tag.Index}", DbType.String, tag.Value.OriginalName);
      }

      using (DbDataReader reader = cmd.ExecuteReader())
      {
        while (reader.Read())
        {
          LibraryTag newItem = new LibraryTag()
          {
            Id = reader.GetInt32(reader.GetOrdinal("LibraryTagId")),
            LibraryId = reader.GetInt32(reader.GetOrdinal("LibraryId")),
            UserId = reader.GetInt32(reader.GetOrdinal("UserId")),
            Tag = reader.GetString(reader.GetOrdinal("Tag"))
          };
          result.Add(newItem);
        }
      }
    }

    return result;
  }
  ```
</details>
