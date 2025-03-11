---
deleted: true
tags: [Grooming]
title: 20241112/13 Grooming
created: '2024-11-08T09:43:57.122Z'
modified: '2024-11-29T09:35:21.254Z'
---

# 20241112/13 Grooming 

### GOAL 1 – Prepare SL main page improvements for refinement (ET-85) - 2 stories
- RFE-13882: Selecting items in SL/PL with Ctrl/Shift buttons
  + Possibility to select multiple items using the Ctrl and Shift buttons
  + Using the right button to select one by one (usabilty?)

- RFE-18066: [SPIKE] Filters tab: How to include “None” option in pub. date filter field.
  + Simple investigation to add "-None" at the Publication date to show results with no pubdate data asigned.

### GOAL 2 – Prepare Apply Tags improvements (ET-139) – 4 stories
I make a question to Dima:
**If I understand correctly, all these stories are already implemented in DEV, are these stories created to make a refactor?**
And this is your answer:
**Not really refactor, but additional checks and implementation in case something is not implemented and re-implementation to use DocViewer controls where possible**

- RFE-13424: Apply tags dialog: Create Add Tags dialog shell
  + On DEV environment already exists this dialog, but do not works fine
- RFE-13430: Apply tags dialog: Ability to search for tags
  + On DEV environment already exists this dialog, but do not works fine
- RFE-13429: Apply tags dialog: Ability to apply tags to documents
  + On DEV environment already exists this dialog, but do not works fine
- RFE-13534: From the SL's datagrid: Add tags to the citation
  + On DEV environment already exists this dialog, but do not works fine


### GOAL 3 – Prepare Manage Tags improvements (ET-95) – 4 stories
**These histories are the same that the previus Goal**
- RFE-13425: Manage tags: Create Add Tags dialog shell
- RFE-13428: Manage tags: Ability to search an add a new tag
- RFE-17471: Manage tags: Ability to add multiple non-duplicated tags
- RFE-13427: Manage tags: Ability to rename/remove library tags

### GOAL 4 - Prepare Tagging – Max size control and the entry to only DB supported characters (ET-120) - 2 stories
- RFE-17953: [TECH] Fix tags indexing
  + Change GetLibraryDocumentTags from type varchar to NVarchar
- RFE-14016: IMPORT – Limit tags characters entry to only DB supported characters
  + 

### GOAL 5 - rreview some Technical/QA stories: 
- RFE-18157: [AQA] Add automation IDs on Sl page. 
