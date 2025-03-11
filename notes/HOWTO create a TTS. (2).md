---
attachments: [Clipboard_2024-11-07-10-03-40.png]
tags: [HowTo]
title: HOWTO create a TTS.
created: '2022-11-29T09:41:27.545Z'
modified: '2024-11-07T09:03:43.695Z'
---

# HOWTO create a TTS. 

### Follow this steps:

- Create a new Jira with this characterists
  + **Project**: Tech Team Support (TTS)
  + **Type**: Support Request
  + **Summary**: *Describe_a_reason_to_create_this_tts*  
  + **TTS Request Type**:Database Administration
  + **Component/s**: RightFind Enterprise
  + **TTS Approver**: Michael Lawless
  + **Client(s)**: <name-of-the-client>
  + **Target Release**: TBD
  + **CCC Environment**: RFE PRD
  + **Environment Family**: RFE Prod

### Description
  
In the Description of TTS you must be explain and indicates environment, reason, expected results,...
  
  Run this **RFE-11434_UpdateScript.sql** attached in **RFE REPORTING PROD DB** to ..... and its records reported in link **link to jira caused this tts**
  
  **(rprd1rptdb1.win-rfe-prd.copyright.com,2433 – RFEPRD database)**
  
  Please, execute with **"Results to text"** in SSMS and **upload the output**.
  
  The reason to execute this in the Reporting DB first is because we couldn't work with a similar dataset in Test or Dev environments. 
  A successful execution on the reporting DB should ensure that this is safe to execute in prod.
  
  **This script should update/delete/insert xxxxx records.**
  
  **It's important that this is executed during Seville office hours so we can check the results before the reporting database is restored again.**
  
### Attachments and Links  
  
  - It's necessary attach a SQL. Its recommended add to your SQL script a Console Log semaphores.
  - It's necessary add link to Jira "Was caused by"
  
### Final Steps
  - Assigned Ticket to your team lead
  - Add comment with a petition review to your team lead.
  
### Before your team lead review your script  
  - Assigned ticket at Michael Lawless and wait!
  
### For example:
  + https://jira.copyright.com/browse/TTS-85330 --> Example to make a petition to replica.
  + https://jira.copyright.com/browse/TTS-85631 --> Example to make a petition to Production environment.
  + https://jira.copyright.com/browse/TTS-69807

# Before the TTS launch on a Replica.
  
## Create a report or something like that in a Jira ticket to review for reporter before launch this script on production environment.
