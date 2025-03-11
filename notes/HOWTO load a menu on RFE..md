---
tags: [HowTo]
title: HOWTO load a menu on RFE.
created: '2023-01-30T09:32:47.047Z'
modified: '2024-11-07T09:04:30.780Z'
---

# HOWTO load a menu on RFE.
## ExplorerView
#### For example: What is the menu to user: 'testadmin2@example.com'? Following this steps
- Find the userId
``` 
select UserId, ClientId from AppUser with(nolock) where email = 'testadmin2@example.com' 
```
- Find the ExplorerView assigned to this user:
```
select * from explorerView with(nolock) where UserId=1626874 
```
- Find All views related with this.
``` 
select * from ExplorerView with(nolock) where ViewId in (1665631, 118131, 743758) 
```
- **Grand - Parent** `` 743758	RFEFullUser+Admin               NULL	                                0 ``
- **Parent** `` 118131	Administrator	                Default administrative view             743758 ``
- **Child** `` 1665631	Training User's Default View	User Training User's custom view	118131 ``
