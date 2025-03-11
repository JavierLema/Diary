---
tags: [Dev Training]
title: Dev Training Documentation. TRS API (Transactional Reporting Service)
created: '2022-08-18T08:25:46.922Z'
modified: '2024-11-05T08:51:34.564Z'
---

# Dev Training Documentation. TRS API (Transactional Reporting Service)

### The TRS provides to the user instant permissions to share content.
##### https://docs.google.com/document/d/16XqeWBotzed1Ehi4e2Ibkvf2IgxUtaIJiV0VGoc9ipU/edit#

*****************************
## Referral classes, methods and links
1. **ClearanceResults**
    - **GetCCCQuote**: Determines whether the citation is available from the TRS API and returns a quote for the estimated cost if available.
        If it returns an actual fee, clearance is granted. If it returns DbUtils.NoMoney, clearance is not granted.
2. **Transactional REST API (external)**
    - **[Swagger](http://rs-trx-rest-svc.aws-p-dev.copyright.com/rs-transactional-rest/swagger-ui.html)**
        Very short documentation about this
3. **TransactionalHttpClient**. It is located in VLShared\external\CCC
    - **SearchPublication**: Search the publication we are trying to get permission from on the TRS system.
    - **GetPermissions**: Returns permissions available for the workId 
    - **GetPrice**: Returns the estimated pricing
    - **PlaceOrder**: IMPORTANT! Submits the existing order to CCC TRS.

*****************************
## Questions

- This document have a lot of TODO (pending link to document x)
    * Order Processor (Sourcing/Fulfillment Tables) - TODO: Pending to link
    * CRO Page (Order Options) (Order Pre Processor) - TODO: Pending to link
    * TODO: Link document to JobTester solution usage
    * TODO: Link document to order processor exercises / overview
    * ...

- Exists any form to get an order list from publication or citation?
- It's recommended create a diagram to related a publication, citation, order,...


****************************************************
## Proposed challenges and Key points

### STEPS.
==========
1. Choose a citation for a content from the Journal Postgraduate Medicine (contentId 20690 in DEV) 
    and use the Job Tester to verify the following:
    * Check the permissions this content has.
    * Determine the fees for this content.
    * Check how we match our citation to the publication that is returned by the CCC TRS API and 
        describe at a very high level the matching algorithm.
2. Debug the GetCCCQuote method and try to describe the algorithm that calls other TRS API methods and why it performs such calls.
