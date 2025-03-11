---
tags: [Dev Training]
title: Dev Training Documentation. Cart.
created: '2022-09-21T08:43:55.249Z'
modified: '2024-11-05T08:51:34.277Z'
---

# Dev Training Documentation. Cart. 

##### https://docs.google.com/document/d/1HOltlTnDwDAPfwoE4F0L73gTrFw2IEfTAP00vwnz0Z4/edit#

*****************************

#### OrderForm.aspx - button Get Content - Cart.aspx
In Cart.aspx->Page_Init() the content allready exists into a LiveCart. 
What is reponsable method?
- OrderCitRes.aspx -> SubmitBtn_Click -> _cart.AddItem


## Notes
When a client adds items to the cart, this is saved on OrderItemSaved and OrderItemSavedExtended tables. At this moment the application creates a fake cart with items.

## Proposed challenges and Key points

- Try to find out in the code by debugging, in how many places we need to initialize the live cart for the application to work properly.
    * I think that it’s necessary a lot of times because the logon functionality it’s not implemented in one site over one unique object, independent of the method to access the application.

- Try adding items for cart and check out how the entities are created in OrderItemSaved
    * This process occurs into:  OrderCitRes.aspx -> SubmitBtn_Click -> _cart.AddItem

- When logging off and on with the cart full of items, try to debug and summarize what the live cart does to retrieve said items.
    * This occurs in InitializeCurrent methods into LiveCart.cs

- Once you proceed with ordering several items, try to describe the correlation that exists between what was previously in the OrderItemSaved table and their newly created OrderItems.
    * This occurs into OrderProcessor. 


## How to running?
All users has a DeliveryProfile, this DeliveryProfile it’s a relation with active user and yours active Cart
