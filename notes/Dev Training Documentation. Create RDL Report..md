---
tags: [Dev Training]
title: Dev Training Documentation. Create RDL Report.
created: '2022-08-18T08:25:46.920Z'
modified: '2024-11-05T08:51:34.311Z'
---

# Dev Training Documentation. Create RDL Report.

##### https://docs.google.com/document/d/1EYFt6WZJi7fEIhQWydkNM1qIcuO2RU1kCzwnOniB5hs/edit#

*****************************
## Usedful links
- Create report => https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/reports#h.ck06cs6sl8tm
    **IMPORTANT** In this document exists a section to upload document.
- Upload document => https://jira.copyright.com/browse/RFE-10314

 
## Steps to create and upload a RDL Report
### Create a report
- Opening solution VLReportsOnly
- Configure a ConnectionStrings on RLDB.rds:
    * rdev1ag1.win-rfe-dev.copyright.com
    * rtest1ag1.win-rfe-test.copyright.com
    * rprod1ag1.win-rfe-prd.copyright.com 	

- Create a new report or copy for a existent report
    * Modify a SQL to add or remove fields
    * Modify design to implemented report
    * Test your report on Preview tab.

### Upload de report:
- Go to Application Configuration > Report Definitions
- Click New to create a new report definition:
    - Name: ***name-of-the-report***
    - Report file: ***select a rdl file***
- Select the created report in the top grid and click New in the bottom grid to create a new App Function:
    - Name: ***name-of-the-function***
    - Function Category: ***SELECT A APPROPRIATE CATEGORY***
    - Security Id: ***UNIQUE ID FROM APPFUNCTION TABLE***
    - Client Visible: ***unchecked***
- Go to Application Configuration > View Management and find view CCC Admin with id = 2 and start edit Items.
    - Find the entry Reports and click on the section where you want add this report.
    - Function Category: ***PICK A SELECTED CATEGORY IN PREVIOUS STEP***
    - Function: ***PICK A SELECTED FUNCTION IN PREVIOUS STEP***
    - Title: ***Report title on menu***
    - Location: ***After item or child of a item***
- Go to reports section and update the page ***(F5)*** to reload all reports definitions


### Send report to RFE
- Create a report entry on DEV (Application Configuration > Report Definition & View Management)
- Create a Pull Request. Indicate a URL and path on RFE website.
- Wait to aprove PR (**IMPORTANT!!**)
    - Create a report entry on TEST (Application Configuration > Report Definition & View Management)
    - Wait to merge PR on master
        - Create a report entry on PRO (Application Configuration > Report Definition & View Management)
