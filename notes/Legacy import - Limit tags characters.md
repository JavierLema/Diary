---
attachments: [Clipboard_2024-12-12-14-24-29.png, Clipboard_2024-12-12-14-26-13.png, Clipboard_2024-12-12-14-27-37.png, Clipboard_2024-12-12-14-31-06.png, Clipboard_2024-12-12-14-31-25.png, Clipboard_2024-12-13-13-58-18.png]
tags: [__JIRA Tickets]
title: Legacy import - Limit tags characters
created: '2024-12-12T11:42:11.995Z'
modified: '2025-02-13T08:16:37.281Z'
---

# Legacy import - Limit tags characters
## RFE-14016 - Limit tags characters entry to only the list of supported characters

#### Import new library content

- **Solution Branch** JavierLema:RFE-14016_LegacyImportTags

- **Future improvement**For the task we need to add ',' as separator.
  ```
  string[] tags = State.ImpRec.Tags.Split(new char[] { ';' }, StringSplitOptions.RemoveEmptyEntries);
  ```
<hr/>

- **Import Formats**: Create a new report format. (Copyright Type is mandatory)
<details>
  <summary>Screenshot</summary>

  ![](@attachment/Clipboard_2024-12-12-14-24-29.png) 
</details>

- **Advanced Company Settings**. Select the destiny library and select import option.
<details>
  <summary>Screenshots</summary>

  ![](@attachment/Clipboard_2024-12-12-14-26-13.png)
  ![](@attachment/Clipboard_2024-12-12-14-27-37.png)
  ![](@attachment/Clipboard_2024-12-12-14-31-06.png)
  ![](@attachment/Clipboard_2024-12-12-14-31-25.png)
</details>

- Find the job into database:
```SELECT TOP 10 * FROM JobsPending WITH (NOLOCK) WHERE (Status=0 OR Status=3) ORDER BY jobId desc```

- Using JobTester to degub your importation
<details>
  <summary>JobTester code</summary>
  
  ```
  try
  {

    using (DbContext db = new DbContext())
    {
      ImportJob job = new ImportJob();
      job.Load(74741, db);

      LibraryImportJP processor = new LibraryImportJP();
      processor.BeginExecution(job, 1000, Callback);
    }
  }
  catch(Exception ex)
  {
    Console.WriteLine(ex);
  }

  private static void Callback(JobProcessor processor)
  {
  }

  ```
  **JobProcessor**
  ```
  public virtual bool BeginExecution(Job p_oJob, short serverId, JobCompleteCB p_oCB)
  ...
  #if DEBUG
		ExecuteThread();
		return true;
  #endif
  ```
  **LibraryImportJP**
  ```
  protected JobResult DoLibraryImport()
  ...
  #if DEBUG
				sourceFilePath = @"C:\Temp\Import";
  #endif
  ```
</details>

#### Questions and solutions
- Can I import multiple tags for one record?

- To validate tags:
  - Add condition at PreProcessRecord() in LibraryImportJP class
  - Add a new method to the LibraryFieldSet class and check this on DoLibraryImport() method in LibraryImportJP class

#### Regular expression to validate:
```
// \u002C Comma
// \u007F Delete
// \u0081 Unused
// \u008D Unused
// \u008F Unused
// \u0090 Unused
// \u009D Unused
// \u00AD Soft hyphen
// \u00B6 Pilcrow sign - paragraph sign

private const string CharPatternExclude = @"[\u002C\u007F\u0081\u008D\u008F\u0090\u009D\u00AD\u00B6]";
```

#### Regular expression to exclude all non-printable chars and comma char
```
private const string AllNonPrintableCharsPattern = @"[\x00-\x1F\x7F,]";
```


