---
tags: [Dev Training]
title: Dev Training Documentation. PVLibraries.
created: '2022-10-06T07:32:47.941Z'
modified: '2024-11-05T08:51:34.486Z'
---

# Dev Training Documentation. PVLibraries.
https://docs.google.com/document/d/15ypyuYXGE9wNCqOuP9iCLPfn0rt4nZlVidFWLHoTR2Q/edit
___

## About
PV Libraries (PharmacoVigilance) libraries is a special feature designed to allow clients to configure in a more granular way how documents are displayed within these libraries.
Funcionality:

- Library fields sets -> Define mapped fields. **Advaced company settings > Library field sets**
    * A **"PV-enabled library"** will be the library that is configured with some Field Set in library settings.
    
- Library views -> Configure "My Libraries" page. **Advanced Company Settings > Library Views **
    * Library Views are a tool for filtering documents in a shared library list.
    * Filters: View Filter or User Filter

- Library Triggers -> Library triggers automatically set values based on conditions for specific PV fields. **Advanced Company Settings>> Library Triggers**
    * Trigger type **RealTime**. Don't depends the date. Run withing 30 seconds
    * Trigger type **Scheduled**. Depends the date. Run withing 30 minutes


These custom fields are visible on "More info" tab in a Doc viewer.

**Import**  Advanced Company Settings > Shared Library Management
To import documents into libray, you need create a import format. This import format it's necessary related to Field Set, for this purpose you need select a "library content" on a "Data type" combobox and select this option.


## General Classes
The classes to implemented this funcionality allowed into **VLShared project**
* LibraryFieldSet -> Contains a list of LibraryCustomFields. It persists in the LibraryFieldSet database table.
* LibraryCustomFields
    * LibraryFieldSetTrigger
    * LibraryFieldSetTriggerCondition
    * LibraryFieldSetTriggerAction

* LibraryView -> Determines how to display fields defined into FieldSet.

### Database Schema
* Library
* LibraryView
* LibraryFieldSet
* LibraryCustomField
* LibraryFieldSetTrigger
* LibraryFieldSetTriggerLibrary


## Proposed challenges and Key points
* Case study RFE-10498
* PV Shared Library creation 
    - Navigate into "Advanced company settings" > "Library Fielsets" and create one.
    - Now go to "Advanced company settings" > "Library Views" and create one with this Fieldset.
    - Now go to "Advanced company settings" > "Library Trigger" and create one with this Fieldset.

*
