---
title: "How to make an import request [6.41]"
date: 2022-02-21T10:17:00-05:00
draft: false
weight: 13
---

<!-- begin comment block (when active)-------------------- -->
{{% notice warning %}}
The API Reference is currently under construction and its contents should not be used until further notice.
{{% /notice %}}

- [Making an *Import* request](#ImportRequest)
- &nbsp;&nbsp;&nbsp;&nbsp;[Identifying value classes](#IdentifyingValueClasses)
- &nbsp;&nbsp;&nbsp;&nbsp;[*Import* request endpoint](#ImportRequestEndpoint)
- &nbsp;&nbsp;&nbsp;&nbsp;[*Import* request format](#ImportRequestFormat)
- [Making a *Check Status* request](#CheckStatusRequest)  
- &nbsp;&nbsp;&nbsp;&nbsp;[*Check Status* request endpoint](#CheckStatusRequestEndPoint)
- [Receiving a response](#ReceivingAResponse)
- &nbsp;&nbsp;&nbsp;&nbsp;[Response format](#ResponseFormat)
- [Import API Name/Id Cross-Reference](#NameIdXref)
<!-- end comment block (when active)-------------------- -->

{{% notice tip %}}
The **Swagger UI** can be used to make the request(s) related to importing information. See [*How to use the Swagger UI*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToUseTheSwaggerUI_6.41/) for details. Use of Swagger is not *required* to import information to Teamwork.
{{% /notice %}}

---

## Making an *Import* request {#ImportRequest}

Making an import request involves you posting an *Import* request supplying the data to be imported and then processing the response(s) sent back by Teamwork. These responses could either be *Success*, *Error*, or *In Process*, depending on the execution mode of a given API.

Unlike export APIs where you can choose either the synchronous or asynchronous processing mode, the mode for import APIs are hard-coded for each API. In other words, a given import API will either automatically run synchronously or asynchronously.

When a request is made for an *Import* which is synchronous, you'll receive either a *Success* or *Error* response, as appropriate. When a request is made for an *Import* which is asynchronous, you'll always automatically receive an *In Process* response. You'll need to continue checking the status of the request until either a *Success* or *Error* response is received. See [Making a *Check Status* request](#CheckStatusRequest) below.

### Identifying value classes {#IdentifyingValueClasses}

*Import* requests can, optionally, include a *Settings* group (sometimes named *ImportSettings*) containing zero or more items identifying which value (field) is to be used for a particular value class.

For example, the **Adjustment Import API** has the **ImportSettings** entry **ItemSetting**. This setting indicates which of the supported values (in this instance, “ExternalId”, “Plu”, “Clu”, or “Upc”) is to be used to identify items while that import request is being processed.

Each import API has its own settings (or perhaps no settings at all). The settings that can be used for a given API will be described in that API’s documentation. The documentation will list the available settings along with the valid values for that setting, and the default value if the setting is omitted.

### *Import* request endpoint {#ImportRequestEndpoint}

Request method: **POST**  
Request URL: <span class="fg-brown"><b><i>\<your-chq-url\></i></span>/chqapi/import/<span class="fg-brown"><i>\<api-id\></i></b></span>  
HTTP Headers: **Content-Type: application/json**  
HTTP Headers: **ApiKey:** <span class="fg-brown">***\<your-api-key\>***</span>

<span class="fg-brown">***\<your-chq-url\>***</span> is the URL of your CHQ as supplied by Teamwork.  
<span class="fg-brown">***\<api-id\>***</span> is an identifier of the API as listed in the [Import API Name/Id Cross-Reference](#NameIdXref) below.  
<span class="fg-brown">***\<your-api-key\>***</span> is your API key value. See [*How to manage API keys*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToCreateManageApiKeys_6.41/) for further info.

### *Import* request format  {#ImportRequestFormat}

The format of an *Import* request differs for each import API. See the API’s documentation in the **Import APIs** section for details on each import API.

--- 

## Making a *Check Status* request {#CheckStatusRequest}

As noted above, when requesting an import which is asynchronous, the initial response will always be an *In Process* response. As long as an *In Process* response is received, you'll need to continue making *Check Status* requests until either a *Success* or *Error* response is returned.

{{% notice info %}}
When checking the status of an asynchronous import you must provide the initial *Import* request's **ApiDocumentId** value. The **ApiDocumentId** is a GUID which can, optionally, be generated by you and supplied in the initial *Import* request. If you do not supply an **ApiDocumentId** in the *Import* request, a GUID for the request will be generated by Teamwork and will be included in the initial *In Process* response. Whether the id is generated by you or by Teamwork, that id **must** be provided in subsequent status check requests.
{{% /notice %}}

### *Check Status* request endpoint {#CheckStatusRequestEndPoint}

Method: **POST**  
URL: <span class="fg-brown">***\<your-chq-url\>*</span>/chqapi/status**  
HTTP Headers: **Content-Type: application/json**  

<span class="fg-brown">***\<your-chq-url\>***</span> is the URL of your CHQ as supplied by Teamwork.  

In addition, as mentioned above, you will need to supply the appropriate **APIDocumentId** value in the **documentId** field of the request in order to check the status of that document.

---

## Receiving a response {#ReceivingAResponse}

The response received after posting a request can be one of three possible types: *Success*, *Error*, or *In Process*.

The *Success* response is automatically returned when the processing of a synchronous *Import* request has completed successfully or when a *Check Status* request is made after the successful completion of the processing of an asynchronous *Import* request.

An *Error* response will automatically be received when the processing of a synchronous *Import* request has completed with an error or when a *Check Status* request is made after the unsuccessful completion of the processing of an asynchronous *Import* request.

An *In Process* response is automatically returned in response to an initial asynchronous *Import* request and will also be returned after each *Check Status* request until the processing of the initial *Import* request has completed. See [Making a *Check Status* request](#CheckStatusRequest) above.

### Response format {#ResponseFormat}

Below is the response format. See [*JSON Data Types*](https://twdocs.netlify.app/dev/API_Reference/Supporting_Information/JsonDataTypes_6.41/) for a description of the values which could appear in the **Data Type** column.

<span class="ir">***?????????? Need to confirm that this format is still valid. The JSON source code I have available to me is very old. Also, is this a generic format? In other words, is the 'Lines' group in this format a generic representation of the specific lines which might appear in a specific response format? ??????????***</span>

**Field Name** | **Data Type** | **Description** |
---- | ---- | ---- |
Id | string, guid | A unique identifier of the API document used to make the import request. **Required**|
Status | string, enum  | An indication of the status of the request. Its value will be one of the following: "Error", "InQueue", "Validation", "InProcess", "Successful" **Required**|
Progress | number, null | <span class="ir">***????????***</span> |
TotalRecords | integer, null | The total number of records processed. <span class="ir">***????????***</span> |
AcceptedRecords | integer, null | The number of submitted records accepted (written to the database). <span class="ir">***????????***</span> |
ErrorRecords | integer, null | The number of submitted records which had errors. <span class="ir">***????????***</span> |
ElapsedTime | string, datetime, null | The time it took to execute the import request. |
ErrorMessage | string, null | A general error message if there were any errors. |
<span class="api-gn">Lines</span> | | <span class="api-gd">A group containing the following fields and groups. This is an array containing zero or more entries.</span> |
EntityNo | string | An identifier of the entity being referenced.<span class="ir">***????????***</span> |
EntityId | string, guid | A unique identifier of the entitiy being referenced.<span class="ir">***????????***</span> |
Error | string, null | A message describing the error related to the entitiy being referenced.<span class="ir">***????????***</span> |
Status | string, enum | An indicator of status of the entity being referenced. Its value will be one of the following: "Error", "InQueue", "Validation", "InProcess", "Successful" <span class="ir">***????????***</span>|
<span class="api-gs">---</span>  | | <span class="api-gde">end of Lines</span> |
ApiType | string | <span class="ir">***????????***</span> **Required** |
Source | string | The source of the data being supplied. <span class="ir">***????????***</span> |

---

## Import API Name/Id Cross-Reference {#NameIdXref}

<span class="ir">***????????? This list needs to be reviewed to ensure that the values are correct. ??????????***</span>

**Import API Name** | **Import API Id**
--- | --- |
Adjustment | adjustment |
Advance Ship Notice | asn |
Count Memo Scan | CountMemoScan |
Create Count Memo | CreateCountMemo |
Create Count Memo Adjustment | CreateAdjustmentForCountMemo |
Credit Memo | credit-memo |
Credit Memo Transaction | credit-memo-transaction |
Custom Table | custom-table |
Custom Table Definition | custom-table-definition |
Customer | customer |
Echo ECommerce Quantity | echo/EcommQty |
External Location | external-location |
External Location Qty | external-location-qty |
External Order | external-order |
Gift Card | gift-card |
Inventory | inventory |
Inventory Brand | invenbrand |
Inventory Class | invenclass |
Inventory Department | invendepartment |
Inventory Department Settings | invendepset |
Inventory Price | inven-price |
Inventory Season | invenseason |
Location | location |
Merge Customers | merge-customer |
Postal Code | postalcode |
Promo Engine | promoengine |
Promo Group | promogroup |
Purchase Order | purchase-order |
Purchase Order Acknowledgement | purchase-order-acknowledgement |
Purchase Order Sent Acknowledgement | purchase-order-sent-acknowledgement |
Purchase Receipt | purchase-receipt |
Quantity Status Update | QtyStatusUpdate |
Quantity Status Reset | QtyStatusItem |
Reserve Orders | reserve-order |
Return Receipt | return-receipt |
RMA Order | rma-order |
RMA Worksheet | rma-worksheet |
Role Employee | role-employee |
Sales Order | sales-order |
Sales Receipt | receipt |
Sales Receipt Update | receipt-update |
Secure Customers | secure-customers |
Teamwork Analytic Services Report | tasreport/stream |
Traffic Counter | traffic-counter-import |
Transfer Order | transfer-order |
Vendor | vendor |
Vendor Invoice | vendor-invoice |
