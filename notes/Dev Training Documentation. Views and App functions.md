---
tags: [Dev Training]
title: Dev Training Documentation. Views and App functions
created: '2022-09-15T09:46:40.696Z'
modified: '2024-11-05T08:51:34.591Z'
---

# Dev Training Documentation. Views and App functions

##### https://docs.google.com/document/d/1o18_Pu9rOGw0BEjdEjb3F_O_hGsjrAATNhVJk3lmscc/edit#heading=h.s422etnzug7j

*****************************

## Notes
Exists an environment variable "ImpView" to defines a default view on Impresonation client
SELECT * FROM ExplorerView WITH (NOLOCK) WHERE ViewId = 527917


## Interesting links
https://docs.google.com/document/d/1alCUYq-wtLqzvj8Zne3qBcuBgVM1EpFIVM9tmXdzT-E/edit#


## Views
When you are a client or a impersonating client.
- Advanced Company Settings - User Views => Create or modify a views options. You can modify all UI elements.

## Users, Groups and views
- Create a View from CCC Admin. Important check "Visible to Clients" option.
- Edit this view with your preferred menu options and folders



 
## Proposed challenges and Key points 
* Add an empty folder on the “Edit View” page and when you login inside the user with the empty folder, find the line of code that prevents the folder from showing.
    - An empty folder hasn't a functionId value: rfe.aspx.cs:786

* Find the list of all of the possible explorer entries and find how the folder children get filled to create the IEnumerable responsible for the Explorer entries.
* Add multiple entries to a view from different categories and find which column from “AppFunction” is used to read the rights of each entry.
    - The column functionId
* Debug the point where a client gets associated with a function when creating the view item.
