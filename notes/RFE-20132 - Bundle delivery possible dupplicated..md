---
attachments: [Clipboard_2025-03-10-11-57-31.png, Clipboard_2025-03-10-11-58-54.png]
tags: [__JIRA Tickets]
title: RFE-20132 - Bundle delivery possible dupplicated.
created: '2025-03-06T10:24:49.578Z'
modified: '2025-03-10T15:05:24.185Z'
---

# RFE-20132 - Bundle delivery possible dupplicated.

### Mini spike to know how works the order status "Suspended (Possible Duplicate). Resume status: Sourcing Pending"

<details>
  <summary>Client information</summary>

  + Client name: **Takeda**.
  + Client Id:  **12123**
  
  On client configuration, in the Order Options tab we can see the **Duplicate Handling -> User Approval**
  `ClientDuplicateOrderHandling.UserNotify;`

  Duplicate Window: Default value: 48 hours.

  Reproduce on DEV Continue with bundle?

  + Impersonate client 
    - Manage my company account - Manage orders: Filtered orders by status: **92 orders in status Suspended**
    - Work Queues - Suspended Items: Filtered results by Suspend Reason Possible **duplicate: 84 Work Queues**
</details>

<details>
  <summary>Investigation result</summary>

  **OrderProcessor** contains a method called **DoDuplicateCheck**. On this method gets all possible duplicated orders from the database with this Query (For this specific case used these parameters: UserId: 1122411, UseId: 1094, ContentId: 144848057,174616998):
  ```
  SELECT top 100 * FROM OrderItem I WITH (NOLOCK) 
    WHERE I.UserId = @UserId AND I.ContentId = @ContentId AND I.UseId = @UseId AND I.LinkExpiration > GETUTCDATE()
  ```
  If the result of this query return any results, the code has two possibilities depending on duplicateHandling value:
    - ClientDuplicateOrderHandling.AutoCancel: Cancel the order
    - Suspend the order. **user or admin should be notified and given opportunity to accept/decline** 
</details>

<details>
  <summary>Reproduce in lower environment - solution</summary>

  - Create a new order
    - Search for the **Snijders Blok-Campeau**
    - Create a order without Bundle delivery 10.1038/s41431-020-0654-4 
    - Order complete: 7709470

  - Search again 
    - Create a new order automatically: 7709471

  - To add this content for a new order and to make this order like a Bundle delivery. The user needs to show advanded options on CRO page.
  ![](@attachment/Clipboard_2025-03-10-11-57-31.png)
  VS
  ![](@attachment/Clipboard_2025-03-10-11-58-54.png)

  **EXPLANATION** The order processor tries to process these orders and when detects the Suspended status, removes these orders from the Bundle for an “Invalid Status” reason.

</details>

<details>
  <summary>Order: 23266455 Audit</summary>

  - General	Removed from Bundle. Reason - inappropriate status [Suspended].	2/24/2025 12:37:32 PM
  - General	Requested in Bundle ID - 33	2/24/2025 10:37:23 AM
  - Notification	Sent to rose.wallace@takeda.com using **Possible Duplicate Order** - User - 2014	2/24/2025 10:37:23 AM
  - WorkItem	AutoProc: **Order Suspended - Possible Duplicate**	2/24/2025 10:37:23 AM
  - Status	Changed to Suspended by rose.wallace@takeda.com	2/24/2025 10:37:23 AM
  - Status	Changed to Sourcing Pending by rose.wallace@takeda.com
</details>

<details>
  <summary>Order: 23266456 Audit</summary>

  - General	Removed from Bundle. Reason - inappropriate status [Suspended].	2/24/2025 12:37:33 PM
  - General	Requested in Bundle ID - 33	2/24/2025 10:37:23 AM
  - Notification	Sent to rose.wallace@takeda.com using **Possible Duplicate Order** - User - 2014	2/24/2025 10:37:23 AM
  - WorkItem	AutoProc: **Order Suspended - Possible Duplicate**	2/24/2025 10:37:23 AM
  - Status	Changed to Suspended by rose.wallace@takeda.com	2/24/2025 10:37:23 AM
  - Status	Changed to Sourcing Pending by rose.wallace@takeda.com
</details>
  
<details>
  <summary>Code investigation</summary>

  - OrderEventHandler
    ```
    public virtual void DuplicateOrder(OrderItem p_oOrder, ClientConfig p_oClient, UserIdent p_oUser, InformationSource p_eInfoSource, DbContext p_oDb)
    {
      EventProcessor.Process(p_oClient.DuplicateOrderHandling == ClientDuplicateOrderHandling.AdminNotify ? ProcessingEvent.PossibleDuplicateOrderAdmin : ProcessingEvent.PossibleDuplicateOrder, p_oUser, p_oOrder, 0, p_eInfoSource, p_oDb);
    }
    ```
  - Overrides on:
    + ILLOrderEventHandler
    + RapidOrderEventHandler
    + OrderProcessor
    + WIAdvancedRef

</details>















