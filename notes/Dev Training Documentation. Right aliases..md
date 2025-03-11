---
tags: [Dev Training]
title: Dev Training Documentation. Right aliases.
created: '2022-11-24T13:42:35.239Z'
modified: '2024-11-05T08:51:34.505Z'
---

# Dev Training Documentation. Right aliases. 
- https://docs.google.com/document/d/1ez9pixukh3FmSWlCqfQnUb3D68FwqyvdATElGEzfE5k/edit#heading=h.s422etnzug7j
- https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/cro-content-usage-options

## Right aliases.
This appear at the bottom of the CRO page when ordering a document.
- To access from UI: Advanced company settings >> Right aliases.
- Only client admin have access to this section.
- Only clients with productCode VL20 can access to this section.

### Products Code.
- case Client.ProductCode_VL20:
    return "RightFind Now";
- case Client.ProductCode_VL20PLUS:
    return "RightFind Enterprise";
- case Client.ProductCode_CSCM:
    return "RightFind Enterprise with Agreement Manager";
- case Client.ProductCode_BI:
    return "Business Intelligence Only";

### Related Clasess
- RightAlias.cs
- RightAliasDlg.aspx.cs
- OrderCitRes.aspx.cs
- CROUtils.cs
- OrderPreProcessor.cs

### Related database schema 
- RightAlias
- RightAliasAccess
- UserGroup
- RightDefinition

### Other information
When you create a right aliases, you can select in a General Tab:
- Required Copyright
- 2nd Required Copyright
- 3rd Required Copyright
- 4th Required Copyright

In a Display Options Tab, you can assigned these right alias to the:
- **Document Delivery** => In a Content "Usage Options" in a CRO page inside the "Get Content" Tab.
- **Copyright Permissions** => In a Content "Usage Options" in a CRO page inside the "Permissions" Tab.
- **Permission Quickcheck** => This information shows when user click on "Rights Info" into a document viewer.
