---
attachments: [Clipboard_2025-01-24-07-15-26.png, Clipboard_2025-01-24-07-18-13.png, Clipboard_2025-01-24-07-21-05.png, Clipboard_2025-01-24-07-23-12.png]
tags: [__JIRA Tickets]
title: Parameter injection
created: '2025-01-23T15:07:35.880Z'
modified: '2025-02-13T08:17:10.960Z'
---

# Parameter injection 
## RFE-13222 - [Tech Debt] Parameter injection: The URL allows downloading all RFE certificates.


<details>
  <summary>Ticket definition and explanation</summary>

  In this screenshot we can see the list of differents available certificates for this client.

  ![](@attachment/Clipboard_2025-01-24-07-15-26.png)

  These certificates have these code to download

  ![](@attachment/Clipboard_2025-01-24-07-18-13.png)

  ### Explanation
  In this example we can see the Javascript method downloadCertificate and a number 9 or 8 between parentesis. This number isn't a certificate Id, this number is a Id of the SAMLCertificate table:
  ```
  SELECT SAMLCertificateId, Description FROM SAMLCertificate WITH (NOLOCK) ORDER BY SAMLCertificateId
  ```
  ![](@attachment/Clipboard_2025-01-24-07-21-05.png)
</details>


<details>
  <summary>How to add certificates?</summary>

  - As a CCC Admin go to the *System administration* section.
  - Select the SAML Identity Providers
  - Create a new provider
  ### Very important
  ![](@attachment/Clipboard_2025-01-24-07-23-12.png)
  
</details>


