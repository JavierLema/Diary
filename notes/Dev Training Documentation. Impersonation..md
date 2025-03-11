---
tags: [Dev Training]
title: Dev Training Documentation. Impersonation.
created: '2022-09-23T07:56:05.917Z'
modified: '2024-11-05T08:51:34.402Z'
---

# Dev Training Documentation. Impersonation. 

https://docs.google.com/document/d/18cx0KKbLff3EA88Fa9Q45ntTFsBN03X8gtUHfhBXFgA

*****************************
## About
Admin users are allowed to impersonate other clients and users. Some clients have the ability to impersonate other users within the same client.

* When the project start, RFE make a login into Win-rfe-dev with the user RFEDevRWUser (DEV Env)
* EXProxy need's Impersonate an user too.
### This article don't related with ImpersonationContext.cs methods.

## Involved classes
* ImpersDlg.aspx.cs -> Shows a popup "Impersonation client"
* Rfe.aspx.cs -> Manage date to active user/client.
* UIUtils.cs -> Contains a method "ImpersonateUser" to manage all data of a impersonation



## Proposed challenges and Key points
* Try to debug a user with a scope of 16, this scope is the equivalent of the access right level of “Deny”.
    public enum AccessRightLevel : short { None = 0, Info = 1, Edit = 3, Full = 7, Deny = 16 };
    select * from AppUser where UserId in (select top 10 UserId from UsersInGroups where UserGroupId in (select top 10 UserGroupId from RightsForGroup where scope = 16))

* Debug which query is used to get the clients for the Client Impersonation popup
    - Executing this query:
        p.e: SELECT SettingValue FROM AppUserSetting where SettingName = 'MostRecentImpersonations' and UserId = 1098530
    - Results:
        1098949,-65,-7163,-7875,-11421
    - Popup items:
        * 1098949 -> User.
        * -65,-7163,-7875,-11421 -> Clients

* Try to spot the difference between impersonating a client and a user by debugging the ImpersonateUser method.
    UIUtils.cs => public static bool ImpersonateUser(int userId, HttpRequest request, HttpSessionState session, DbContext db, out string alert)

* Find what is the suspicion level that you are using when impersonating
    * Authorization.cs => static public void AdjustSuspicionLevel(UserIdent ident, string ipAddress, double adjustment)
    * iden.SuspiciusLevel = 1.25
