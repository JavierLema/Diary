---
tags: [Dev Training]
title: Dev Training Documentation. Sales Tax Calculations
created: '2022-12-01T12:11:56.567Z'
modified: '2024-11-05T08:51:34.516Z'
---

# Dev Training Documentation. Sales Tax Calculations
https://docs.google.com/document/d/1LVir4tjKIKGCS-MMKaaYY12B1z14zj1fWke4t2gXxME/edit

## About
RFE has a subscription to VeraTax Service. 
VeraTax  File. The  file  you  receive  is  a  sequential  file containing the individual (state, county, city) sales/use tax rates for a location (ZIP code) and the combined sales and use tax rates.

### Database Schema.
#### Tables
- **SaleTax**: Tax information for each unique ZIP code within the United States.
- **SalesTaxTaxable**: Originated in the iDocument system that was the predecessor of RFE from a hundred years ago. 
    * SourceId: 1: Copyright Clearance Center // 2: ISI (Thomson-Reuters) // 5: To be Ingnored
    * TaxCategory: 1: Document Delivery // 10: Patent // 13: Copyright Clearance // 100: Book
    * DeliveryType: 0: Paper delivery // 1: Electronic delivery
    * ...
- **ClientTaxExemption**:  
    * Region: S: state code // C:country name // “A|All” Fully tax exempt, // “IA|All” Taxable in all European Union member countries
    * ...

#### Triggers
- **OrderItem_Insert**: 
    * Launch when order is inserted into OrderItem table.
    * Call stored procedure: CalcTaxProc(@OrderItemId, @FeeTax OUTPUT, @OtherTax OUTPUT)
- **OrderItem_Update**:
    * Launch when any field implicated on Tax calculation changed.
    * Call stored procedure: CalcTaxProx (@OrderItemId, @FeeTax OUTPUT, @OtherTax OUTPUT) 
- **OrderItemFees_Insert**
    * Entries with FeeType < 10000
        - Calculate Fees and apply to OrderItem.FeeOther
    * Entries with FeeType >= 10000
        - Apply to invoices and credit card charges.
        - Not apply to orderItem table. 
        - Call stored procedure: CalcTaxAdjustmentProc (@OrderItemFeeId, @FeeTax OUTPUT, @OtherTax OUTPUT) 
- **OrdertemFees_Update**
    * Same logic that OrderItemFees_Insert but a SQL Script it's neccesary to adjustment.

#### Procedures
- **CalcTaxProc**: Accept params: @OrderItemId, @Currency and returns the calculated @FeeTax and @OtherTax.
- **CalcTaxAdjustmentProc**: Accepts params: @OrderItemFeeId, @Currency and returns the calculated @FeeTax and @OtherTax.
- **CalcTaxHelperProc**: It's a Wrapper for the CalcTaxHelper.
- **CalcTaxProcSaved**: Accepts param @CartItemId and returns the calculated @FeeTax and @OtherTax.
- **CalcTaxExternal**: Deprecated
- **CalcTax**: Initial layer of logic in the tax calculation
- **CalcTaxHelper**: Is responsible for calculating tax
- **CalcTaxAdjustment**: Logical to calculate rounding errors.
