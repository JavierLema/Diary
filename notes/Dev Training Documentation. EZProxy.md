---
tags: [Dev Training]
title: Dev Training Documentation. EZProxy
created: '2022-11-21T10:35:44.035Z'
modified: '2024-11-05T08:51:34.342Z'
---

# Dev Training Documentation. EZProxy 
https://docs.google.com/document/d/1ztiPH-a2suSLTRnc326QEDKInEXAoqrxmiB2t3HanBU/edit#

EzProxy is made by OCLC => https://www.oclc.org/en/ezproxy.html

The shortcut it's a Javascript redirect: `document.location.href;window.open('https://www.test.rightfind.com/vlib/proxy.aspx?ClientId=10979&src=p&url=' + a, '_self');void 0;`
This provides access from a outside clients to a publisher library.

Clients who have this feature get a dedicated server with white IP address and EZproxyinstalled.

### How to enable this option on a client?
- As CCC admin, select Client Management > General > Integrations > RightFind Passport

#### EZ Proxy
- https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/passportsproxy-servers
#### eILL EZ Proxy for NRC (For a Canada users*)
- https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/eill-ez-proxy-for-nrc
#### RFEProxy Deployment and Configuration
- https://docs.google.com/document/d/1BYf7W7MlBa8w4VL7gp3GmpTPV_tzxZya-nSQ9Sd-sl0/edit#heading=h.cdhm4hidv279

### Involved classes
- ClientPassport.cs
    * A persisted entity that stores each client’s EZproxy configuration, if enabled.
- EZProxy.cs
    * This is the main class related to EZproxy

## TIPS
IDP => Identity Provider
