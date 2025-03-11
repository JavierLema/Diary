---
title: You need to know.
created: '2022-08-18T08:25:46.922Z'
modified: '2024-11-05T08:53:10.421Z'
---

# You need to know.
--------------------
### IIS Express configuration
- Open RFEWeb project properties from the Solution Explorer window
- Go to Web tab
- Change http in the Project URL to https
- Change port to some value in range 44300-44399

### Know common issues on vl.sln

#### Atalasoft: Could not load file or assembly 'Atalasoft.dotImage.AdvancedDocClean'
- You only change on RFEWeb properties page - Web - IISExpress Bitness to **x86**
#### Load al TS files and assemblies
- Open - Task Runner Explorer - and run first task (default)



### Environment variables are in EnvConfig Table.
- More information on **EnvConfig.cs:245** on method: static private EnvConfigSettingList **GetAllValuesFromDB**(string envConfigName, DbContext db)

### JOBS
- Table JobsPending contains information about a Job. Most important field is **JobData**, this field contains all characteristics about job.

### Collections Fields
- CollectionCopyrightType:  
    + Local - this is just has some settngs for rights, that can be customized
    + LocalEstimated - this some clearance provide - CVV, I'm not sure what it's
    + CCCQuote - this take some info about rights from CCC internal services
    + CCCPlatform - is used for Related Items, but this functionality is disabled on Prod for now
    + Inherited - inherits from parent collections

- CRCollectionId
    + Clearance Collection
- FFCollectionId
    + Full Fillment Collection
