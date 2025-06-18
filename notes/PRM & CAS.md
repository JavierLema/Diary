---
title: PRM & CAS
created: '2025-04-08T10:58:44.304Z'
modified: '2025-04-08T11:14:17.961Z'
---

# PRM & CAS

### PRM Party Relationship Management

- PRM provides a set of RESTful sevices
  + Over 55 systems integrate
  + Each subsystem uses a subset of features within PRM.
  + Key concept: knows nothing about the system consuming it.
- Provide an internal UI to view and configure
- Allows management of organization.
  + Buyers -> Licensees. We have two different types:
    - Company: 1 or more users and 1 or more AR Accounts
    - Individual: 1 User and 1 AR Account.
  + Vendors/suppliers
- Each system (marketplace app) can provide Roles/Users permissions.

### CAS Central Authenticatoin Service

- Based on OS project: https://www.apereo.org
- PRM and LDAP is integrated 
- Only RFE not uses CAS
- Support IdP via SAML
- 
