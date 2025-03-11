---
attachments: [Clipboard_2025-02-05-14-08-44.png]
tags: [RFE Sections]
title: RFE Sections.
created: '2024-11-05T09:07:16.528Z'
modified: '2025-02-05T13:17:20.812Z'
---

# RFE Sections.


<details>
  <summary>RFE Proxies infraestructure.</summary>

  <span style="color:darkred">**RFEUI -> Application Configuration - External Resources**</span>
  - The customers has not access to the proxies, only RFE application can access.

  - EZ proxy -> OCLC product (Provider Id).
    + **proxy name** proxy00000-1p: 00000 => clientId 1p,2p,Xp number of proxies for the same client.

  - RFE Proxy -> PDF Direct
    + **proxy name** proxy00000-1e: 00000 => clientId 1e,2e,Xe number of proxies for the same client.
    + This is a .Net Core application allocated on EC2.
    + To use this, the client needs a public IP whitelistened on RFE

  - Both
    + **proxy name** proxy00000-1pe: 00000 => clientId 1e,2e,Xe number of proxies for the same client.

  ![](@attachment/Clipboard_2025-02-05-14-08-44.png)

</details>

<details>
  <summary>Additional Information.</summary>

  **To create an order with Additional Information** you need configure previously on:
  - Advanced Company Settings
  - Right Aliases
  - Edit **Use for Myself**
  - Enable checkbox **Additional Information**

</details>


