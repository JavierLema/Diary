---
attachments: [Clipboard_2025-01-30-12-24-18.png, Clipboard_2025-01-30-12-29-16.png, Clipboard_2025-01-30-12-32-05.png, Clipboard_2025-01-30-12-32-37.png]
tags: [__JIRA Tickets]
title: Spreadsheet field
created: '2025-01-30T11:22:46.641Z'
modified: '2025-02-13T08:18:47.316Z'
---

# Spreadsheet field
### RFE-19354 - Summary spreadsheet: Unbundled orders not appear in spreadsheet Reason code 2

<details>
  <summary>Investigate this particular case (Test environment)</summary>

  ![](@attachment/Clipboard_2025-01-30-12-29-16.png)

  - CartId: 7791935
  - Orders fails:
    + 11509734 => s3://com-copyright-rfe-rtest/_fulfillment/5383d1d1-6dca-4484-9ab1-86ded221864cf.pdf
    ![](@attachment/Clipboard_2025-01-30-12-32-05.png)

    + 11509729 => s3://com-copyright-rfe-rtest/_fulfillment/CD732953-761A-4096-80D6-9AC3DF584F78.pdf
    ![](@attachment/Clipboard_2025-01-30-12-32-37.png)

  In the first view, these orders has the right size (< 1MB) but if you take a look at audit information you can view this:
  *Removed from Bundle. Reason - the total file size limit (1MB) of the bundle was exceeded.*

  **IMPORTANT** The name of the file on S3 is the **ExternalId**

</details>

<details>
  <summary>JobTester code</summary>

  ```
    using (DbContext db = new DbContext())
    {
        BundleMetadataGenerator excelGenerator = new BundleMetadataGenerator();
        BundleMetadata metadata = excelGenerator.GenerateMetadata(new int[] { 11509730, 11509731 }, new int[] { 11509734, 11509729 }, db, UserIdent.GetAnonymous());

        BundleMetadataExcelSerializer bundleMetadataExcelSerializer = new BundleMetadataExcelSerializer();
        ClientConfig clientConfig = ClientConfig.Get(12202);

        string path = @"C:\Temp\Bundle\" + DateTime.Now.ToString("yyyyyMMddHHmmss") + ".xlsx";
        byte[] xlsx = bundleMetadataExcelSerializer.Serialize(metadata, clientConfig, CultureInfo.InvariantCulture);
        using (MemoryStream memoryStream = new MemoryStream(xlsx))
        {
          using (Stream stream = new FileStream(path, FileMode.CreateNew))
          {
            memoryStream.CopyTo(stream);
          }
        }
    }
  ```
</details>


<details>
  <summary>Bundle delivery file howto</summary>

  - This is the code to get the name of the file
    ```
      if (FFFileName.IsNullOrEmpty())
      {
        var _strFFDir = AppState.FulfillmentBasePath;
        string name = ExternalId.ToString();

        var origFFExt = ("." + FFFileExt).ToLower();
        var ffExt = RequiresEncryption ? ".pdf" : origFFExt;
        var origFFFilename = RFEIOUri.NormalizeUri(string.Format("{0}{1}{2}", Utils.AssureTrailingBackslash(_strFFDir), name, origFFExt));
        FFFileName = RFEIOUri.NormalizeUri(string.Format("{0}{1}F{2}", Utils.AssureTrailingBackslash(_strFFDir), name, ffExt));
      }
    ```

  - This is the method to check the file size:
    ```
      bool sizeExcedeed = order.CheckBundleMaxFileSize();
    ```
    This method returns that the file exits and this check: 
    ```
      int bundleDeliveryMaxFileSize = AppState.GetSettingAsInt("BundleDeliveryMaxFileSize", 0);
      return file.Length < bundleDeliveryMaxFileSize;
    ``` 
</summary>

