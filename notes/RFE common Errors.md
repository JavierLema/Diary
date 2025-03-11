---
attachments: [Clipboard_2024-11-05-10-58-27.png, Clipboard_2024-11-05-10-59-39.png, Clipboard_2024-12-13-07-09-46.png, Clipboard_2025-02-27-13-30-25.png]
favorited: true
tags: [TIPS]
title: RFE common Errors
created: '2024-11-05T09:57:29.382Z'
modified: '2025-02-27T12:34:02.894Z'
---

# RFE common Errors 
<details>
  <summary> XRayTelemetry.config </summary>

  ![](@attachment/Clipboard_2025-02-27-13-30-25.png)

  **This error throw when we don't have the XRay configuration**
  [XRayTelemetry.config](https://github.com/CopyrightClearanceCenter/rightfind-enterprise/blob/master/Build/AWSConfigs/Local/Web/vlib/XRayTelemetry.config)

</details>

<details>
  <summary>Do you have this error with Atalasoft?</summary>
    
    ![](@attachment/Clipboard_2024-11-05-10-59-39.png)
  
    **One possible solution is change the Bitness on RFE Web Properties to x86**
</details>

<details>
  <summary>OleDBConnection</summary>

  ![](@attachment/Clipboard_2024-12-13-07-09-46.png)

  This error need to install Microsoft Access Database Engine 2016 Redistributable https://www.microsoft.com/en-us/download/details.aspx?id=54920 and configure the  Platform target project to x64
</details>

<details>
  <summary>Service locator must be initialized if Audit is enabled. Service locator is null</summary>

  You need to install Autofac.Integration.Web nuget package and add these lines to code:
  ```
  ...
  using Autofac.Integration.Web;
  using VLShared.ServiceLocator;

  CommonServiceLocator.ServiceLocator.SetLocatorProvider(() => new AutofacServiceLocator(_containerProvider.ApplicationContainer));
  ServiceLocator.Instance.Init(_containerProvider.ApplicationContainer);
  ```
</details>



