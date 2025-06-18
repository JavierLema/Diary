---
favorited: true
title: AWS
created: '2025-05-29T08:58:55.641Z'
modified: '2025-06-06T12:41:24.259Z'
---

# AWS 

<details>
  <summary>AWS configuration help</summary>
  
  - Get current user credentials:
    ```aws sts get-caller-identity```
  - Configuration files:
    ```C:\Users\1jlema\.aws\config```
    ```C:\Users\1jlema\.aws\credentials```
  
</details>

<details>
  <summary>X-Ray</summary>

  #### How to run JobTester with XRay:

  <details>
    <summary>App.config</summary>

  Add these lines on the app.config at the **first line** after **configuration** node.
  ```
    <configSections>
      <section name="XRayTelemetry" type="VLUtils.Configuration.XRayTelemetryConfigSection, VLUtils, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </configSections>
    <XRayTelemetry configSource="XRayTelemetry.config"></XRayTelemetry>
  ```
  </details>
    
  <details>
    <summary>Autofac.cs</summary>

  You need to change these methods:
  - **Create**: Add these lines
    ```
      ContainerBuilder builder = new ContainerBuilder();
      IXRayTelemetryConfig xRayTelemetryConfig = XRayTelemetryConfigSection.GetInstance();
      builder.RegisterInstance(xRayTelemetryConfig);
      builder.ConfigureXRayTelemetry(xRayTelemetryConfig);
      ConfigureDependencies(builder, xRayTelemetryConfig);
      IContainer container = builder.Build();
    ```
  - **ConfigureDependencies**:
    ```
      builder.RegisterType<OrderProcessor>()
        .As<IOrderProcessor>()
        .InstancePerDependency() // a new and unique instance is resolved everytime (default)
        .TraceWithXRay<IOrderProcessor>(xRayTelemetryConfig); // intercept interface if configured

      builder.RegisterType<CreditCardPaymentClient>()
        .As<ICreditCartPaymentClient>()
        .InstancePerDependency() // a new and unique instance is resolved everytime (default)
        .TraceWithXRay<ICreditCartPaymentClient>(xRayTelemetryConfig); // intercept interface if configured
    ```
  </details>
  
  <details>
    <summary>Add metadata at some segment </summary>

  ```
    Dictionary<string, object> metadata = new Dictionary<string, object>()
    {
      { "OderItemId", workItemId }
    };

    using (new XRayTraceSegment<IOrderProcessor>(metadata))
    {
      using (DbContext db = new DbContext())
      {
        using (IOrderProcessor _oProcessor = OrderProcessorFactory.Create(AppUser.None, InformationSource.AutoProc, db))
        {
          DateTime _dtStartTime = DateTime.UtcNow;
          _oProcessor.Process(workItemId);
        }
      }
    }
  ```
  </details>
  
  <details>
    <summary>XRay daemon</summary>
    
  - Download the XRay daemon
  - Launch the daemos with a user has configured the AWS credentials
    ```.\xray_windows.exe  -o -n us-east-1```
  - Configure de Interceptor in **TelemetryContainerExtensions** to load the local proxy
    ```recorder.SetDaemonAddress("127.0.0.1:2000");```
  </details>

  <details>
    <summary>JobServer topics</summary>

  - Service.cs comentar líneas de atalasoft
  - Order.config => Autostart true
  - Demás servicios apagados
  - VLServer.config => serverId: 1000
  - OrderProcessor -> Process() breakpoint
  - XRayTelemetryInterceptor -> Intercept() breakpoint
  </details>

</details>



