---
tags: [Dev Training]
title: Dev Training Documentation. SAML Imports
created: '2022-08-18T08:25:46.919Z'
modified: '2024-11-05T08:51:34.533Z'
---

# Dev Training Documentation. SAML Imports

##### ##### SAML Imports: https://docs.google.com/document/d/1MYBuWTeKduqJ_KGhvCVOnrAy3YitraCWzUBTCVCkKNk/edit

*****************************
## Usedful links
- SAML: https://sites.google.com/a/pubget.com/mobile-library/rfe-knowledge-base/saml
-

## Questions
- Create a developer account in https://developer.okta.com
- Create an Application to SAML integration with RFE.
    + https://docs.google.com/document/d/1T1lOsin20miqS-nastkPd1XPpnb6ciMXQUZ978v6bOE/edit
    + The “Identity Provider Single Sign-On URL” and “Identity Provider Issuer” and download the X.509 Certificate details
- Create an user on section Directory-people
    + In the section "Attribute Statements" are a fields to import to RFE. Mapping Okta-RFE

### IMPORTANT!
The relation into okta fields and RFE Import Fields are in:
* Directory - People - User - Profile - Attributes: Italic/gray fields: This are fields names neccesary to mapping in a Attibutes section on a application **"ATTRIBUTE STATEMENTS"**. For Ex:
>Name..........Name Format........Value
>
>FirstName.....Unspecified........user.firstName


## Possible errors

+ Unable to add or update user record: InvalidEmail
    Error en el Mapping de los campos
+ Unable to add or update user record: InvalidView
    ###### En el mapping faltan:
    - "Base View Name" **Default Value** => "User"
    - "User Groups"    **Default Value** => "Administrator"



## Referral classes, methods and links
*****************************
+ recassert.aspx.cs
+ SAMLIdentityProvider.cs
+ To view XML from OKTA: "System Administration" - Logs - Traces.

## Questions
+ Al data into Import format are "valid" until click on profile validate button.
+ All validations of imports fields are validated after importation.


****************************************************
## Proposed challenges and Key points

### STEPS.
==========
1. Create an OKTA account and create an application for DEV environment, then create a user for that application..
    - Register on developer.okta.com
        * Create users under "Directoy"-"People" option.
    - Create a new "Import Format" on RFE - Impersonate Client
        ##### IMPORTANT. This is a User mapping:
        - First Name => FirstName
        - Last Name => LastName
        - Email => email
        - "Base View Name" **Default Value** => "User"
        - "User Groups"    **Default Value** => "Administrator"

2. Create a new Client with a proper SAML Identity provider using the guidelines from the documents at 1.2.
    - Create a new "SAML Identity Provider" with data of OKTA
    - Access to Embed Link shows in Okta page!

3. Enter a wrong address in the import format as a default and check the two different messages that you can get in Splunk. You can check existing import formats for SAML identity providers to help you better understand how this works.
    - Done
    
4. Create two different import formats for one provider and change the first import, the one you used to create the user to the second, updating the user.
    - Done
5. Finally, once you’ve been able to reproduce these scenarios try to debug the import process and pinpoint where those validations are being done and explain how we record the assertion from OKTA upon login.
    - All validations of this import fields are begin on: **SAMLIdentityProvider.cs**:399: 
        * codeManager.UserPostProcess = format.PostProcessingScript;
    - Address validation make in **AddressValidationClient.cs** 
        * public static AddressValidationResult ValidateAddress(TaxRestRequestAddress addressRequest)
        * Call http://tax-rest.aws-p-dev.copyright.com/tax-rest/ecom/validate/address and try to get a GeoPoint.
