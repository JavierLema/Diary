---
tags: [HowTo]
title: HOWTO resove Jira. Resolution ticket.
created: '2022-11-29T09:41:27.530Z'
modified: '2024-11-07T09:04:00.967Z'
---

# HOWTO resove Jira. Resolution ticket.

## IMPORTANT
- **IF YOU CREATED A COMMIT AND CREATED A PULL REQUEST, YOU CAN NOT RESOLVE JIRA BEFORE YOUR CHANGE ARE IN DEV, AND AFTER YOU TESTED THIS CHANGE.**

### When you go to resolve a Jira, you have two possible scenarios:

- (A)**Report or Question**
    - If the Jira has a report petition you must attach a XLS report and SQL used to make it.
    - Select on dropdown **"Resolution"** and select option **"Done"** for a report petition.
    - Select on dropdown **"Resolution"** and select option **"Question Answered"**: for a ticket has a question.    
    - Select on dropdown **"Root Cause"** and select option **"Data"**
    - Assignee ticket to Reporter
- (B)**Modify code**
    - Select on dropdown **"Resolution"** and select option **"Fixed or Completed"**
    - Select on dropdown **"Root Cause"** and select option **"Code"**
    - Fill **"Root cause details"** and **"Resolution details"** with the old code and new code, and the reason to change this.
        + These descriptions are made for QA team not for developers
    - Select on dropdown **"Fixed version"** Next tag when your commit merged on master branch.
    - Assignee ticket to Iana

### Add comment to Ping reporter.
    For example: **@reporter**. I Attached the report for this ticket: **<Link to report Attached>**
    

## Custom cases: 
### In case we don't have permissions, or we don't test 100% it is necessary to indicate it.: For example:
The code Javi posted is exactly the same widget code that can be found in RFE, we didn't do any modifications.
Following MS's documentation, as Javi explained with the proper permissions you can embed the code and it should work, but we were unable to run real tests because we don't have such permissions.
Please, let us know if you are able to try this successfully so it is tracked in this ticket.
