---
tags: [RFE Sections]
title: OrderProcesor and friends
created: '2025-02-04T10:41:56.983Z'
modified: '2025-02-05T12:45:50.163Z'
---

# OrderProcesor and friends

<details>
  <summary>PendingBundleProcessor</summary>

  #### Sample to call pendingBundleProcessor from jobTester.
  ```
  var cartId = 7791935;
  using (DbContext db = new DbContext())
  {
    PendingBundleProcessor pendingBundleProcessor = new PendingBundleProcessor(db, null, null, null, null, null, null, null);
    pendingBundleProcessor.Process(new OrderBundle()
    {
      Id = 1985,
      CartId = cartId,
      Status = RFE.Domain.Enums.OrderBundleStatus.Processed,
      ProcessingDelayTime = DateTime.Parse("2025-01-21 12:27:39.4630000"),
      MaximumProcessingTime = DateTime.Parse("2025-01-22 00:27:39.4630000"),
      CorrelationId = "c1ca775c-8965-4b95-978d-344ad339e940",
      ArchiveKey = "2818e11f-0d10-4bbc-9a57-945ad5a5b7a8.zip",
      ArchiveKeyChecksum = -1066030314,
      ArchiveLink = "https://www.test.rightfind.com/delivery/orderbundle.aspx?file=2818e11f-0d10-4bbc-9a57-945ad5a5b7a8.zip&key=1",
      LinkExpirationTime = DateTime.Parse("2025-02-20 12:31:42.2030000"),
      Orders = ParseOrderItem(cartId, db)
    });
  }
  ```
  #### Code to convert a orderItem to BundleOrderItem
  ```
  public static List<BundledOrderItem> ParseOrderItem(int id, DbContext db)
  {
    var result = new List<BundledOrderItem>();
    var orderItemList = OrderItem.GetByCartId(id, db);
    foreach(var item in orderItemList)
    {
      result.Add(new BundledOrderItem()
      {
        CartId = item.CartId,
        ClientId = item.ClientId,
        ExternalId = item.ExternalId,
        FFFileExt = item.FFFileExt,
        Id = item.Id,
        InDb = item.InDb,
        OrderItemId = item.Id,
        Status = BundledOrderStatus.PendingBundleDelivery,
      });
    }
    return result;
  }
  ```
  #### Get information about a S3 file.
  ```
    IRFEFileInfo fileInfo = RFEIOService.Instance.File.GetInfo($"s3://com-copyright-rfe-rtest/_delivery/order/{item.ExternalId.ToString().ToLowerInvariant()}.pdf");
    Console.WriteLine(fileInfo.Length);
  ```


  ### Notes:
  To test this orders/bundle... remember to reset the status at first time:
  ```update orderItem set UnbundlingReasonCode = null, bundled = 1, Status=11 where orderItemId in (...)```

<details>
