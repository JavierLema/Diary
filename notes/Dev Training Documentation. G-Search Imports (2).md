---
tags: [Dev Training]
title: Dev Training Documentation. G-Search Imports
created: '2022-08-18T08:25:46.917Z'
modified: '2024-11-05T08:51:34.389Z'
---

# Dev Training Documentation. G-Search Imports

##### https://docs.google.com/document/d/16erKXuq9qLtg2KIVxjx-w5iX6aQ8LzdHq7YPhMvPlcI/edit#

*****************************
## Usedful links
+ Reseller Reports => https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/reports/reseller-reports
- /vlib/admin/reporttask.aspx?task=Reseller (only accesible via URL) 

+ PV Libraries => Create a custom fields/controls/filters/... customization clients
- https://docs.google.com/document/d/15ypyuYXGE9wNCqOuP9iCLPfn0rt4nZlVidFWLHoTR2Q/edit#
- PV Libraries (PharmacoVigilance) libraries is a special feature designed to allow clients to configure in a more granular way how documents are displayed within these libraries.
- Impersonate client -> Advanced Company Settings > Library Field Sets
- https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/pv-shared-libraries
- Super configurable options. Save in DB as a string with separated chars. vl\VLUtils\Utils.cs

#### Related database schema
- Library - LibraryView - LibraryFieldSet - LibraryCustomField - LibraryFieldSetTrigger - LibraryFieldSetTriggerLibrary.

+ Process Tasks => https://docs.google.com/document/d/1bnpmk603Zau8XTuIxKVGM74EXOdwbPpDOtbQHmFno58/edit#
    Process Tasks are light-weighted backend tasks intended for simple jobs which don't need too much complexity.

+ VL Server Console
    https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/vlserverconsole

 
## Referral classes, methods and links
1. **GSearchImportProcessTask** => Can be isolated from the JobTester.

****************************************************
## Proposed challenges and Key points

### STEPS.
==========
* https://jira.copyright.com/browse/RFE-10049
----
1. The exercise proposed in this case will be to download the sample files from above, change the data, and force the Execute method to read the files locally rather than via FTP to create a new G-Search client with multiple users. Pay attention to the import data method and find where and why the import sets the partner value.
