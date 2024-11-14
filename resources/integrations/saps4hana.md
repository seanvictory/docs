---
description: Connect to your users' SAP S/4HANA systems.
---

# SAP S/4HANA

## Setup Guide

You can find your SAP S/4HANA app credentials in your [SAP S/4HANA Developer Account.](https://api.sap.com/)

You'll need the following information to set up your SAP S/4HANA App with Paragon Connect:

* SAP Host URL
* Username
* Password

## Connecting to SAP S/4HANA

Once your users have connected their SAP S/4HANA account, you can use the Paragon SDK to access the SAP S/4HANA API on behalf of connected users.

See the SAP S/4HANA [REST API documentation](https://api.sap.com/) for their full API reference.

Any SAP S/4HANA API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get the top 50 supplier invoices
paragon.request("saps4hana", "/odata/sap/API_SUPPLIERINVOICE_PROCESS_SRV/A_SupplierInvoice?$top=50&$inlinecount=allpages", {
  method: "GET"
});

// Release an invoice by ID
paragon.request("saps4hana", "/odata/sap/API_SUPPLIERINVOICE_PROCESS_SRV/Release?SupplierInvoice=<SupplierInvoiceID>&FiscalYear=2022&DiscountDaysHaveToBeShifted=true", {
  method: "POST"
});

// Get a customer by ID
paragon.request("saps4hana", "/odata/sap/API_BUSINESS_PARTNER/A_Customer(%27<Customer ID>%27)", {
  method: "GET"
});
  
```

## Building SAP S/4HANA workflows

Once your SAP S/4HANA account is connected, you can add steps to perform the following actions:

* Create Supplier Invoice
* Get Supplier Invoice by ID
* Search Supplier Invoices
* Delete Supplier Invoice
* Get Supplier by ID
* Search Suppliers
* Update Supplier
* Get Customer by ID
* Search Customer
* Update Customer

You can also use the SAP S/4HANA Request step to access any of SAP S/4HANA's API endpoints without the authentication piece.

When creating or updating records in SAP S/4HANA, you can reference data from previous steps by typing `{{` to invoke the variable menu.
