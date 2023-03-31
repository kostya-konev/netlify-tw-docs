---
title: "Credit Memo Import [6.41]"
date: 2023-03-28T11:23:00-05:00
draft: true
weight: 1805
---
<!-- Weight => sstt; ss=>2nd letter's nbr/tt=>3rd letter's nbr (w/leading zeros) -->

<!-- begin comment block (when active)-------------------- -->
{{% notice warning %}}
The API Reference is currently under construction and its contents should not be used until further notice.
{{% /notice %}}

- [Overview](#Overview)
- [Request endpoint](#RequestEndpoint)
- [Request format](#RequestFormat)
- [Request schema](#RequestSchema)
- [Request example(s)](#RequestExamples)
- [Response example(s)](#ResponseExamples)

---
<!-- end comment block (when active)-------------------- -->

## Overview {#Overview}

The **Credit Memo Import** API is used to import credit memos into CHQ.

See [*How to make an import API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnImportRequest_6.41/) for a description on how import requests are made and on the standard response formats used. The API-Specific request format for this API will be described below. 

---

## Request endpoint {#RequestEndpoint}

Method: **POST**  
URL: <span class="fg-brown">***\<your-chq-url\>***</span>**/chqapi/import/credit-memo**  
HTTP Headers: **Content-Type: application/json**  
HTTP Headers: **ApiKey:** <span class="fg-brown">***\<your-api-key\>***</span>

<span class="fg-brown">***\<your-chq-url\>***</span> is the URL of your CHQ as supplied by Teamwork.  
<span class="fg-brown">***\<your-api-key\>***</span> is your API key value. See [*How to manage API keys*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToManageApiKeys_6.41/) for further info.

This import request must always be asyncronous. <span class="ir">???? Is this true? ????</span>

In the Swagger UI the **/chqapi/import/credit-memo** endpoint is a member of the **Stored Values** endpoint group.

---

## Request format {#RequestFormat}

Any field not explicitly marked as **Required** is optional and can be omitted. See  [*JSON Data Types*](https://twdocs.netlify.app/dev/API_Reference/Supporting_Information/JsonDataTypes_6.41/) for a description of the values which could appear in the **Data Type** column.

**Field Name** | **Data Type** | **Description** |
---- | ---- | ---- |
Source | string | The source of the data being supplied to the import. **Required** |
CommunicationId | string, guid | A unique identifier of the request (see [*Handling the CommunicationId parameter*](https://twdocs.netlify.app/dev/API_Reference/Supporting_Information/HandlingTheCommunicationIdParam_6.41/) for additional info). |
<span class="api-gn">Data</span> | | <span class="api-gd">A group containing the following fields and groups. **Required**</span> |
<span class="api-gn">Data: Request</span> | | <span class="api-gd">A group containing the following fields and groups. **Required**</span> |
<span class="api-gn">Data: Request: ImportSettings:</span> | | <span class="api-gd">A group containing the following fields and groups. |
ReceiptSetting | string, enum | An indicator of which value is to be used to identify receipts. Its value must be one of the following: "ReceiptNum”, “TeamworkId”, "Dtn". If omitted, the default is "ReceiptNum”.|
LocationSetting | string, enum | An indicator of which value is to be used to identify locations. Its value must be one of the following: "Code", "TeamworkId", "ExternalId". If omitted, the default is "Code". |
<span class="api-gs">---</span>  | | <span class="api-gde">end of Data: Request: ImportSettings</span> |
<span class="api-gn">Data: Request: CouponTransactions</span> |  | <span class="api-gd">A group containing the following fields and groups. This group is an array with one or more entries. **Required**</span> |
TransactionId | integer | An identifier of the transaction. |
CouponNumber | string | An identifier of the coupon used for the transaction. |
Amount | number | The amount of the transaction. |
ReceiptIdentifier | string | An identifier of the receipt for which the transaction occured. |
LocationIdentifier | string | An identifier of the location where the transaciton occured. |
LocalTransactionTime | string, datetime | A timestamp, in the local timezone, of when the transaction occured. |
TransactionTime | string, datetime | A timestamp, in the universal timezone<span class="ir">?????????</span>, of when the transaction occured. |
IncomingIp | string | <span class="ir">?????????</span> |
TransactionStatus | string, enum | An indicator of the transaction's status. Its value must be one of the following: "Authorized", "Captured", "Discarded". |
<span class="api-gs">---</span>  | | <span class="api-gde">end of Data: Request: CouponTransactions</span> |
<span class="api-gs">---</span>  | | <span class="api-gde">end of Data: Request</span> |
<span class="api-gs">---</span>  | | <span class="api-gdc">continuation of Data</span> |
ApiDocumentId | string, guid | A unique identifier of the API document being used. |
<span class="api-gs">---</span>  | | <span class="api-gde">end of Data</span> |

## Request schema {#RequestSchema}

~~~
~~~

---

## Request example(s) {#RequestExamples}

**Request Example #1:**

~~~
~~~

## Response example(s) {#ResponseExamples}

**Response Example #1: Success**

~~~
~~~

**Response Example #2: In Process**

<span class="ir">?????????? The below example provided by the developers has the wrong 'ApiType'. It is 'coupon-transation-import' rather than 'coupon-transaction'. This means that other aspects of the example could be wrong. We should probably get new examples to ensure that they are correct. ?????????</span>

~~~
~~~

**Response Example #3: Error**

~~~
~~~
