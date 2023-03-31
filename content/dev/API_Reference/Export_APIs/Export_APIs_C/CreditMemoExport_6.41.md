---
title: "Credit Memo Export API [6.41]"
date: 2023-03-24T12:47:00-05:00
draft: false
weight: 1805
---
<!-- Weight => sstt; ss=>2nd letter's nbr/tt=>3rd letter's nbr (w/leading zeros) -->

<!-- begin comment block (when active)-------------------- -->
{{% notice warning %}}
The API Reference is currently under construction and its contents should not be used until further notice.
{{% /notice %}}

- [Overview](#Overview)
- [Request endpoint](#RequestEndpoint)
- [Request settings](#RequestSettings)
- [Request filters](#RequestFilters)
- [Request sorts](#RequestSorts)
- [Successful response](#SuccessfulResponse)
- &nbsp;&nbsp;&nbsp;&nbsp;[Format](#SuccessfulResponseFormat)
- &nbsp;&nbsp;&nbsp;&nbsp;[Schema](#SuccessfulResponseSchema)
- [Request example(s)](#RequestExamples)
- [Response example(s)](#ResponseExamples)

---
<!-- end comment block (when active)-------------------- -->

## Overview {#Overview}

This topic describes the **Credit Memo Export** API which is used to export credit memo information from CHQ.

See [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for a description on how export requests are made and on the standard request and response formats used. The API-Specific successful response format for this API will be described below.

---

## Request endpoint {#RequestEndpoint}

Method: **POST**  
Synchronous URL: <span class="fg-brown">***\<your-chq-url\>***</span>**/chqapi/export/credit-memo**  
Asynchronous URL: <span class="fg-brown">***\<your-chq-url\>***</span>**/chqapi/export/credit-memo/async**  
HTTP Headers: **Content-Type: application/json**  
HTTP Headers: **ApiKey:** <span class="fg-brown">***\<your-api-key\>***</span>

<span class="fg-brown">***\<your-chq-url\>***</span> is the URL of your CHQ as supplied by Teamwork.  
<span class="fg-brown">***\<your-api-key\>***</span> is your API key value. See [*How to manage API keys*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToManageApiKeys_6.41/) for further info.

In the Swagger UI the **/chqapi/export/credit-memo** endpoint is a member of the **StoredValues** endpoint group.

## Request settings {#RequestSettings}

Below are the settings which can be supplied in the **Settings** group of the export request to define which value (field) is to be used for a particular value class (see [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for additional info).

The **Key** column lists the names of the available settings. The **Supported Values** column lists the valid values which can be supplied for the setting. The **Default** column lists the default value for each setting if that setting is not supplied.

<span class="ir">?????????? THe below settings are documented in the API description page in Confluence, but they do not appear in the developer supplied JSON Schema. ??????????</span>

**Key** | **Supported Values** | **Default** | **Description** |
---- | ---- | ---- | ---- |
EmployeeIdentifierSetting | LoginName, FullName,TeamworkId | LoginName | An indicator of which value is to be used to identify employees. |
LocationIdentifierSetting | ExternalIdCode, Code, ExternalId, No, TeamworkId | ExternalIdCode | An indicator of which value is to be used to identify locations. |
SVSZoneIdentifierSetting | Name, TeamworkId | Name | An indicator of which value is to be used to identify SVS (Stored Values Service) zones. |
CurrencyIdentifierSetting | Code, Name, TeamworkId | Code | An indicator of which value is to be used to identify the currency used. |
CustomerIdentifierSetting | CustomerNo, MemberCode, Email, Phone, ExternalId, TeamworkId | CustomerNo | An indicator of which value is to be used to identify customers. |
CountryIdentifierSetting | Code, Name, TeamworkId | Code | An indicator of which value is to be used to identify countries. |

## Request filters {#RequestFilters}

Below are the filters which can be defined in the **Filters** group of the export request (see [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for additional info).

The **Field** column lists the names of the fields on which filtering can be done. The **Operators** column lists the filter operator values which are valid for the field. The **Value** column describes the value expected for the field.

<span class="ir">?????????? THe below filters are documented in the API description page in Confluence, but they do not appear in the developer supplied JSON Schema. ??????????</span>


**Field** | **Operators** | **Value** |
---- | ---- | ---- |
RecModified | "Greater than", "Greater than or equal", "Less than", "Less than or equal", "Equal" | Any valid string representing a *datetime* value. |
CreditMemoNo | "Equal", "Contains" | Any valid string representing a credit memo number for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. |
CustomerEmail | "Equal", "Contains" | Any valid string representing an email address for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. | 
CustomerNo | "Equal", "Contains" | Any valid string representing a customer number for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. |
CustomerPhone | "Equal", "Contains" | Any valid string representing a phone number for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. |
SVSZoneName | "Equal", "Contains" | Any valid string representing a stored values service zone name for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. | 
CreateDate | "Greater than or equal", "Less than or equal", "Equal" | Any valid string representing a *datetime* value. |
SalesOrderDTN | "Equal", "Contains" | Any valid string representing a device transaction number for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. |
SalesOrderNo | "Equal", "Contains" | Any valid string representing a sales order number for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. |
WebOrderNo | "Equal", "Contains" | Any valid string representing a web order number for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. |
Status |  "Equal", "Contains" | Any of the following status strings for the "Equal" operator, or a comma-separated list of such values for the "Contains" operator. The valid types are: "active", "deactivated", "zeroBalance", "expired". |

## Request sorts {#RequestSorts}

The information returned is automatically sorted by the **RecModified** field *ascending*. No other sorts can be requested.

---

## Successful response {#SuccessfulResponse}

### Format {#SuccessfulResponseFormat}

Below is the format of the successful response to the export request. See [*JSON Data Types*](https://twdocs.netlify.app/dev/API_Reference/Supporting_Information/JsonDataTypes_6.41/) for a description of the values which could appear in the **Data Type** column.

**Field Name** | **Data Type** | **Description** |
---- | ---- | ---- |
ApiDocumentId | string,guid | A unique identifier of the API document being used. |
Status | string, enum | The status of the response. The value will always be "Successful". |
ApiRequestType | string | <span class="ir">***????????***</span>
TotalRecords | int32 | The total number of submitted records processed. <span class="ir">***????????***</span> |
RecordsCount | int32 | The number of records returned. <span class="ir">***????????***</span> |
ElapsedTime | string, datetime | The time it took to execute the export request. |
StartDateTime | string, datetime | A timestamp of when the export request started executing. |
EndDateTime | string, datetime | A timestamp of when the export request stopped executing. |
<span class="api-gn">Response</span> | | <span class="api-gd">A group containing the following fields and groups.</span> |
<span class="api-gn">Response: CreditMemos</span> |  | <span class="api-gd">A group containing the following fields and groups. This group is an array with zero or more entries.</span> |
RecCreated | string, datetime | A timestamp of when the record was created. |
RecModified | string, datetime | A timestamp of when the record was last modified. |
CreditMemoId | string, guid | A unique identifier of the credit memo. |
CreditMemoNumber | string | An identifier of the credit memo. |
DeviceTransactionNumber | int64 | The credit memo's transaction number on the device used. |
InitialAmount | double | The credit memo's initial amount. |
CreditMemoBalance | double | The credit memo's current balance. |
Status | string, enum | An indicator of credit memo's current status. Its value must be one of the following: "active", "deactivated", "zeroBalance", "expired". |
CustomerIdentifier | string | An identifier of the credit memo's customer. |
SVSZoneIdentifier | string | An identifier of the credit memo's SVS (stored values service) zone. |
BaseCurrencyIdentifier | string | An identifier of the credit memo's base currency. |
CountryIdentifier  | string | An identifier of the credit memo's country. |
LocationIdentifier | string | An identifier of the credit memo's location. |
DEVId | string | An identifier of <span class="ir">??????????</span>. |
SalesOrderId | string, guid | A unique identifier of the credit memo's related sales order. |
SalesOrderNo | string | An identifier of the credit memo's related sales order. |
SalesOrderDTN | string | The credit memo's related sales order's transaction number on the device used. |
WebOrderNo | string | An identifier of the credit memo's related web order. |
IsManuallyDeactivated | boolean | An indicator as to whether or not <span class="ir">??????????</span>. |
ExpirationPolicy | int32 | <span class="ir">??????????</span> |
ExpirationPeriodDays | int32 | <span class="ir">??????????</span> |
ExpirationPeriodMonths | int32 | <span class="ir">??????????</span> |
ExpirationDate | string, datetime | A timestamp of when the credit memo expires. |
GracePeriodDays | int32 | The number of days in the credit memo's grace period. <span class="ir">??????????</span> |
GracePeriodDate | string, datetime | A timestamp of when the grace period began. <span class="ir">??????????</span> |
CreateDateTime | string, datetime | A timestamp of when the credit memo was created. |
LocalCreateDateTime | string, datetime | A local timestamp of when the credit memo was created. |
EditDateTime | string, datetime | A timestamp of when the credit memo was last modified (edited). |
DeactivateDateTime | string, datetime | A timestamp of when the credit memo was deactivated. |
CreateEmployeeIdentifier | string | An identifier of the employee who created the credit memo. |
EditEmployeeIdentifier | string | An identifier of the employee who last modified (edited) the credit memo. |
<span class="api-gs">---</span> | | <span class="api-gde">end of Response: CreditMemos</span> |
<span class="api-gs">---</span> | | <span class="api-gde">end of Response</span> |

### Schema {#SuccessfulResponseSchema}
 
Below is the JSON source for the schema of a successful response to the export request as described above.

~~~
{
  "CreditMemoExportToJson_get.ApiDocumentType": {
      "type": "object",
      "properties": {
        "ApiDocumentId": {
          "format": "uuid",
          "type": "string",
          "example": "00000000-0000-0000-0000-000000000000"
        },
        "Status": {
          "enum": [
            "Successful"
          ],
          "type": "string"
        },
        "ApiRequestType": {
          "type": "string"
        },
        "TotalRecords": {
          "format": "int32",
          "type": "integer"
        },
        "RecordsCount": {
          "format": "int32",
          "type": "integer"
        },
        "ElapsedTime": {
          "format": "date-time",
          "type": "string"
        },
        "StartDateTime": {
          "format": "date-time",
          "type": "string"
        },
        "EndDateTime": {
          "format": "date-time",
          "type": "string"
        },
        "Response": {
          "$ref": "#/definitions/CreditMemoExportToJson_get.ResponseType"
        }
      }
    },
  "CreditMemoExportToJson_get.ResponseType": {
      "type": "object",
      "properties": {
        "CreditMemos": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/CreditMemoExportToJson_get.CreditMemosType"
          }
        }
      }
    },
  "CreditMemoExportToJson_get.CreditMemosType": {
      "type": "object",
      "properties": {
        "RecCreated": {
          "format": "date-time",
          "type": "string"
        },
        "RecModified": {
          "format": "date-time",
          "type": "string"
        },
        "CreditMemoId": {
          "format": "uuid",
          "type": "string",
          "example": "00000000-0000-0000-0000-000000000000"
        },
        "CreditMemoNumber": {
          "type": "string"
        },
        "DeviceTransactionNumber": {
          "format": "int64",
          "type": "integer"
        },
        "InitialAmount": {
          "format": "double",
          "type": "number"
        },
        "CreditMemoBalance": {
          "format": "double",
          "type": "number"
        },
        "Status": {
          "enum": [
            "active",
            "deactivated",
            "zeroBalance",
            "expired"
          ],
          "type": "string"
        },
        "CustomerIdentifier": {
          "type": "string"
        },
        "SVSZoneIdentifier": {
          "type": "string"
        },
        "BaseCurrencyIdentifier": {
          "type": "string"
        },
        "CountryIdentifier": {
          "type": "string"
        },
        "LocationIdentifier": {
          "type": "string"
        },
        "DEVId": {
          "type": "string"
        },
        "SalesOrderId": {
          "format": "uuid",
          "type": "string",
          "example": "00000000-0000-0000-0000-000000000000"
        },
        "SalesOrderNo": {
          "type": "string"
        },
        "SalesOrderDTN": {
          "type": "string"
        },
        "WebOrderNo": {
          "type": "string"
        },
        "IsManuallyDeactivated": {
          "type": "boolean"
        },
        "ExpirationPolicy": {
          "format": "int32",
          "type": "integer"
        },
        "ExpirationPeriodDays": {
          "format": "int32",
          "type": "integer"
        },
        "ExpirationPeriodMonths": {
          "format": "int32",
          "type": "integer"
        },
        "ExpirationDate": {
          "format": "date-time",
          "type": "string"
        },
        "GracePeriodDays": {
          "format": "int32",
          "type": "integer"
        },
        "GracePeriodDate": {
          "format": "date-time",
          "type": "string"
        },
        "CreateDateTime": {
          "format": "date-time",
          "type": "string"
        },
        "LocalCreateDateTime": {
          "format": "date-time",
          "type": "string"
        },
        "EditDateTime": {
          "format": "date-time",
          "type": "string"
        },
        "DeactivateDateTime": {
          "format": "date-time",
          "type": "string"
        },
        "CreateEmployeeIdentifier": {
          "type": "string"
        },
        "EditEmployeeIdentifier": {
          "type": "string"
        }
      }
}
}
~~~

---

## Request Example(s) {#RequestExamples}

**Request Example #1:**

<span class="ir">need a request example</span>

~~~
~~~

---

## Response Example(s) {#ResponseExamples}

**Response Example #1: In Process**

<span class="ir">need an 'in process' response example</span>

~~~
~~~

**Response Example #2: Error**

<span class="ir">need an 'error' response example</span>

~~~
~~~

**Response Example #3: Success when requesting CreditMemoNo = '33'**

~~~
{
   "ApiDocument":{
      "ApiDocumentId":"E220C072-904F-405D-8D95-0C46FF5AFC3E",
      "Status":"Successful",
      "ApiRequestType":"credit-memo-export",
      "TotalRecords":1,
      "RecordsCount":1,
      "ElapsedTime":"00:00:00.0033333",
      "StartDateTime":"2021-01-28T13:33:02.373",
      "EndDateTime":"2021-01-28T13:33:02.377",
      "Response":{
         "CreditMemos":[
            {
               "RecCreated":"2021-01-27T18:41:14.183",
               "RecModified":"2021-01-28T13:32:52.970",
               "CreditMemoId":"68FA80BB-69AC-49D9-BE2C-39FF6AAF49B1",
               "CreditMemoNumber":"33",
               "DeviceTransactionNumber":1000000030,
               "InitialAmount":11.00000000000000000000,
               "CreditMemoBalance":11.00000000000000000000,
               "Status":"active",
               "CustomerIdentifier":"1000000412",
               "SVSZoneIdentifier":"FOR_CM",
               "BaseCurrencyIdentifier":"EUR",
               "CountryIdentifier":"AF",
               "LocationIdentifier":"TEST123",
               "SalesOrderId":"439EAD3A-98FD-460A-813C-C4A1A5C80288",
               "SalesOrderNo":"1008",
               "SalesOrderDTN":1000000864,
               "WebOrderNo":"1008",
               "IsManuallyDeactivated":false,
               "ExpirationPolicy":2,
               "ExpirationPolicyType":"PeriodDays",
               "ExpirationPeriodDays":1,
               "ExpirationDate":"2021-01-29T21:59:12.073",
               "GracePeriodDays":4,
               "GracePeriodDate":"2021-02-02T21:59:12.073",
               "CreateDateTime":"2021-01-27T18:41:12.073",
               "LocalCreateDateTime":"2021-01-27T18:41:12.073",
               "EditDateTime":"2021-01-28T13:32:52.937",
               "CreateEmployeeIdentifier":"AUTOMAT",
               "EditEmployeeIdentifier":"vodyanik2"
            }
         ]
      }
   }
}
~~~
