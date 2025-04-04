---
attachments: [Clipboard_2025-03-12-12-16-51.png, Clipboard_2025-03-12-12-18-05.png]
tags: [__JIRA Tickets]
title: Client Authorization
created: '2025-03-12T11:16:31.237Z'
modified: '2025-04-03T10:15:00.956Z'
---

# Client Authorization

<details>
  <summary>Ticket details</summary>

  ![](@attachment/Clipboard_2025-03-12-12-16-51.png)

  This section describes the access to a WebServices from clients:

  ![](@attachment/Clipboard_2025-03-12-12-18-05.png)

  SOAP RESTAPI and Business Inteligence.
</details>

<details>
  <summary>SQL to update </summary>

  ```
  UPDATE ClientAuthorization SET WebServiceAuth =
  CASE 
    WHEN WebServiceAuth & 0x0000000001000 > 0 and WebServiceAuth & 0x0000000002000 > 0 THEN 12288
    WHEN WebServiceAuth & 0x0000000001000 > 0 THEN 4096
    WHEN WebServiceAuth & 0x0000000002000 > 0 THEN 8192
  END
  WHERE ClientId = 13649
  
  -- 16383 all
  -- 12288 => RestAPI and BI
  -- 8192 => RestAPI
  -- 4096 => BI
  ```
</details>

<details>
  <summary>This is the SQL to get a list of all clients.</summary>
  
  ```
  SELECT c.ClientId, c.ClientName, 
  CASE c.Status
      WHEN 0 THEN 'Active'
    WHEN 1 THEN 'Pending Delete'
    WHEN 2 THEN 'Deleted'
    WHEN 3 THEN 'Pending Merge'
    WHEN 4 THEN 'Inactive'
    WHEN 5 THEN 'DbDelete'
    WHEN 100 THEN 'Template'
  END AS ClientStatus,
  ca.ClientAuthorizationName,
  ca.IPAddressRange,
  CASE WHEN (
    WebServiceAuth & 0x0000000000001 > 0 or
    WebServiceAuth & 0x0000000000002 > 0 or
    WebServiceAuth & 0x0000000000004 > 0 or
    WebServiceAuth & 0x0000000000008 > 0 or
    WebServiceAuth & 0x0000000000010 > 0 or
    WebServiceAuth & 0x0000000000020 > 0 or
    WebServiceAuth & 0x0000000000040 > 0 or
    WebServiceAuth & 0x0000000000080 > 0 or
    WebServiceAuth & 0x0000000000100 > 0 or
    WebServiceAuth & 0x0000000000200 > 0 or
    WebServiceAuth & 0x0000000000400 > 0 or
    WebServiceAuth & 0x0000000000800 > 0 or
    WebServiceAuth & 0x0000000000001 > 0
  ) THEN 'True'
  ELSE 'False'
  END AS SOAP,
  CASE WHEN (WebServiceAuth & 0x0000000001000 > 0) THEN 'True' ELSE 'False' END AS BI,
  CASE WHEN (WebServiceAuth & 0x0000000002000 > 0) THEN 'True' ELSE 'False' END AS RESTAPI

  FROM ClientAuthorization AS ca WITH(NOLOCK)
  JOIN Client c WITH(NOLOCK) ON c.ClientId = ca.ClientId

  ORDER BY c.ClientId ASC
  ```
</details>


