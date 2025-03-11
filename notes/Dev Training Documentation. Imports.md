---
tags: [Dev Training]
title: Dev Training Documentation. Imports
created: '2022-08-18T08:25:46.917Z'
modified: '2024-11-05T08:51:34.416Z'
---

# Dev Training Documentation. Imports

### There is a multitude of different imports that you can do all across this application.
##### Import Formats: https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/import-formats
##### Imports: https://docs.google.com/document/d/1JdF8qhyxv6abkKwi46PqnQJcDDKm0O_H8YD8xVuFn24/edit#heading=h.s422etnzug7j
##### SAML Imports: https://docs.google.com/document/d/1MYBuWTeKduqJ_KGhvCVOnrAy3YitraCWzUBTCVCkKNk/edit#heading=h.t390tk3xgjty
##### 

___
## Notes
In the Advanced Company Settings > Import History, you can view a result for the import. The columns ***Records*** indicates a number o processed records and failed records separated by a comma. (p.e. "5,0"): 

## Import Formats
https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/import-formats

## Differents data imports
1. **User Import**
    - https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/user-import-client-users-import    

### Steps to Import users on excel 

* **Available fields (Data.):** 
    Addr1, Addr2, Addr3, AltPhone, AltUserName, BillReference, BillReferenceEditable, City, Comments, Country, CostCenter, CostCenterEditable, Culture, CustOrderNumber, CustOrderNumberEditable, DeletedFlag, Department, Division, Email, Fax, FirstName, FriendlyName, LastName, Location, MobilePhone, Password, Phone, PriceLimit, PurchaseOrder, PurchaseOrderEditable, SourceFileName, State, TempValue1-5, TimeZone, UserGroups, UserSkip, Zip
#### Steps to import
    * Create a new import format in "Import Formats" menu above "Advanced Company Settings". **Impersonate client is required.**
        - On a popup Window select on "Data Type" combobox a "Users" option
        - Fill with RFE fields and mapping with your excel file. 
            + **Any field its obligatory?** 
            + **Exits any format to any field?**
        - When you finish press "save" button.
    * Create a Job to Import over "Import Schedule" option
    * Import users result show into "Import History" option. **TODO: create a popup with import results** 
    * To debug this process: **UserImportJP.cs**
        - At line 1340 established a "ImportPath" variable. 

2. **User Import (Library member import)**
    - https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/user-import-library-member-import
    * This option are into a Impersonating client->Advanced Company Settings->Shared Library Management. The option import contains a file template in CSV, XLS and XML format. This option create a Job.
    * To debug this process: LibraryMemberImportJP.cs:185. ImportBasePath change for this option and include a ClientName in the path.

    
3. **Holdings import**
    - https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/holdings-import
4. **Import of library content**
    - https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/import-of-library-content
5. **Import holdings with image**
    - https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/import-formats/content-import-image
6. **Import/Export via SFTTP**
    - https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/importexport-via-sftp

**All imports running with a JOB and a JOBProcessor** Create or select an template and create a JOB.


7. ClientInfoImportDlg. Importation Location, division, and department.
    - Supported importation file types: txt, csv, xls, xlsx
        - Location and Department => 
            * One value for line. 
            * if (!exists) saveNewItem(line)
        - Division => 
            * Allow data separated with comma and tabs. 
            * Only accepts 2 values for line. [0] => division [1] => department 
            * If values.Split().Length > 2 all line as DivisionName
            * if (!exists) saveNewItem(line)

*****************************
## Questions

- You need configure a import format: "Advance company Settings/Import Formats"
- You can import users, orders, holdings, libraries, collections....
- You can import from multiples sources: File, FTP, SFTTP, SSH,...
- You need configure a Environment variable "ImportBasePath" to route on your local machine.
    + _ImportBasePath_ => \\\win-rfe-dev\rfedev\data\import
- To test import Users on "Job Tester" you need copy your file data to "ImportBasePath".
- When imports are successful the import file has moving to the archive path. This is made for method MoveFileToArchive on ImportJobProcessor:93.
    + \\\win-rfe-dev\rfedev\data\archive\\\<ClientName>\\\<Year>\\\<Month>\
- JobType field is referred at JobEnums.cs
- Any import has a possibility to add a post-process Script. 
    + **ImportFormatCodeManager** is the class that runs this code.
    + This script save on **PPScript** field on table **ImportFormat**
    + Database query: `select top 10 * from ImportFormat where PPScript is not null order by FormatId desc`

- **Related database schema**
    - JobsCompleted - JobsPending - ImportRejects - ImportFormat
