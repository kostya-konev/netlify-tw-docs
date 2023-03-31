---
title: "Count Memo Export API [6.41]"
date: 2022-02-28T08:42:00-05:00
draft: false
weight: 1521
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

This topic describes the **Count Memo Export** API which is used to export count memo information from CHQ.

See [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for a description on how export requests are made and on the standard request and response formats used. The API-Specific sucessful response format for this API will be described below.

{{% notice note %}}
For this API, a **Device Transaction Number** (**DTN**) is a value of the *BigInteger* type (for example, *100011311*). A **Short Device Transaction Number** (**ShortDTN**) is a value of the *Base36* type (for example, *GJDPNA*).
{{% /notice %}}

---

## Request endpoint {#RequestEndpoint}

Method: **POST**  
Synchronous URL: <span class="fg-brown">***\<your-chq-url\>***</span>**/chqapi/export/countmemo**  
HTTP Headers: **Content-Type: application/json**  
HTTP Headers: **ApiKey:** <span class="fg-brown">***\<your-api-key\>***</span>

<span class="fg-brown">***\<your-chq-url\>***</span> is the URL of your CHQ as supplied by Teamwork.  
<span class="fg-brown">***\<your-api-key\>***</span> is your API key value. See [*How to manage API keys*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToManageApiKeys_6.41/) for further info.

In the Swagger UI the **/chqapi/export/countmemo** endpoint is a member of the **Catalog** endpoint group.

## Request settings {#RequestSettings}

Below are the settings which can be supplied in the **Settings** group of the export request to define which value (field) is to be used for a particular value class (see [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for additional info).

The **Key** column lists the names of the available settings. The **Supported Values** column lists the valid values which can be supplied for the setting. The **Default** column lists the default value for each setting if that setting is not supplied.

**Key** | **Supported Values** | **Default** | **Description** |
---- | ---- | ---- | ---- |
LocationIdentifierSetting | ExternalIdCode, Code, ExternalId, No, TeamworkId | ExternalIdCode | An indicator of which value is to be used to identify locations. |
EmployeeIdentifierSetting | LoginName, FullName, TeamworkId | LoginName | An indicator of which value is to be used to identify employees. |
AdjustmentIdentifierSetting | No, DTN, TeamworkId | No | An indicator of which value is to be used to identify adjustments. |
CountMemoHeaderIdSetting | DTN, ShortDTN | DTN | An indicator of which value is to be used to identify count memo headers. |
ShowCountMemoItemsSetting | true, false | false | An indicator as to whether or not count memo items will be exported. |

## Request filters {#RequestFilters}

<span class="ir">????????</span> <span class="fg-crimson">**The API documentation in Confluence contains the following filter info; however, the schema source doesn't contain a *Filters* section.**</span> <span class="ir">????????</span> 

Below are the filters which can be defined in the **Filters** group of the export request (see [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for additional info).

The **Field** column lists the names of the fields on which filtering can be done. The **Operators** column lists the filter operator values which are valid for the field. The **Value** column describes the value expected for the field.

**Field** | **Operators** | **Value** |
---- | ---- | ---- |
RecModified | "Greater than", "Greater than or equal", "Less than", "Less than or equal", "Equal" | Any valid string representing a *datetime* value. |
DeviceTransactionNumber | "Equal", "Contains" | Any valid value representing a device transaction number (as described above) for the "Equal" operator or a comma-separated list of such values for the "Contains" operator. |
Status | "Equal", "Contains" | Any one of the following valid values for the "Equal" operator or a comma-separated list of such values for the "Contains" operator. The valid values are: "Open", "Finalized", "Adjusted". |
IsArchived | "Equal" | Any valid boolean value. |

## Request sorts {#RequestSorts}

The information returned is automatically sorted by the **RecModified** field *ascending*. No other sorts can be requested.

---

## Successful response {#SuccessfulResponse}

### Format {#SuccessfulResponseFormat}

Below is the format of the successful response to the export request. See [*JSON Data Types*](https://twdocs.netlify.app/dev/API_Reference/Supporting_Information/JsonDataTypes_6.41/) for a description of the values which could appear in the **Data Type** column.

**Field Name** | **Data Type** | **Description** |
---- | ---- | ---- |
ApiDocumentId | string, guid | A unique identifier of the API document being used. |
Status | string, enum | The status of the response. The value will always be "Successful". |
ApiRequestType | string | <span class="ir">***????????***</span> |
TotalRecords | int32 | The total number of records processed. |
RecordsCount | int32 | The number of records exported. |
ElapsedTime | string, datetime | The time it took to execute the API. |
StartDateTime | string, datetime | A timestamp of when the API began executing. |
EndDateTime | string, datetime | A timestamp of when the API completed. |
<span class="api-gn">Response</span> | | <span class="api-gd">A group containing the following fields and groups.</span> |
<span class="api-gn">Response: CountMemos</span> | | <span class="api-gd">A group containing the following fields and groups. This group is an array with zero or more entries.</span> |
RecCreated | string, datetime | A timestamp of when the record was created. |
RecModified | string, datetime | A timestamp of when the record was last modified. |
CountMemoHeaderId | string, guid | A unique identifier of the count memo header. <span class="ir">***????????***</span> |
CountMemoId | string | An identifier of the count memo. <span class="ir">***????????***</span> |
ExternalId | string | An identifier of the count memo used when interacting with an external system. |
CountDateTime | string, date-time | A timestamp of when the count was taken. <span class="ir">***????????***</span> |
CountLocationDateTime | string, date-time A timestamp of when <span class="ir">***????????***</span> |
LocationIdentifier | string | An identifier of the location where the count was taken. |
DeviceTransactionNumber | int64 | An identifier of the transaction on the device used for the count. |
ShortDTN | string | A short identifier of the transaction on the device used for the count. |
Status | string, enum | An indicator of the count memos status. Its value must be one of the following: "Open", "Finalized", "Adjusted". |
Notes | string | Misc. notes about the count memo. |
CreateDateTime | string, date-time | A timestamp of when the count memo was created. |
CreateEmployeeIdentifier | string | An identifier of the employee who created the count memo. |
EditDateTime | string, date-time | A timestamp of when the count memo was last edited (modified). |
EditEmployeeIdentifier | string | An identifier of the employee who last edited (modified) the count memo. |
AdjustDateTime | string, date-time | A timestamp of when the count memo was last adjusted. |
AdjustEmployeeIdentifier | string | An identifier of the employee who last adjusted the count memo. |
AdjustmentIdentifier | string | An identifier of the last adjustment. <span class="ir">***????????***</span> |
FinalizedDateTime | string, date-time | A timestamp of when the count memo was finalized. |
FinalizedEmployeeIdentifier | string | An identifier of the employee who finalized the count memo. |
IsArchived | boolean | An indicator as to whether or not the count memo has been archived. |
TotalItemsInMemo | int32 | The total number of items in the count memo. |
TotalItemsCounted | int32 | The total number of items which were counted. |
TotalQty | int32 | The total item quantity. |
ItemWithDifferences | int32 | The item difference between the items in the memo and the items counted. <span class="ir">????????</span> |
QtyDifferencesOver | double | The item quantity differences over. <span class="ir">????????</span> |
QtyDifferencesShor | double | The item quantity differences short. <span class="ir">???????? This field name is misspelled! ????????</span>|
UnrecognizedItems | int32 | The number of unrecognized items. <span class="ir">????????</span> |
CustomDate1 - 2 | string, datetime | These two fields are customizable dates for the count memo. |
CustomFlag1 - 2 | boolean |  These two fields are customizable flags for the count memo.
CustomNumber1 - 2 | double | These two fields are customizable integer values for the count memo. <span class="ir">???????? This data type is wrong. 'Number' fields are always a type of 'integer'! ????????</span>|
CustomDecimal1 - 2 | double | These two fields are customizable floating-point values for the count memo. |
CustomText1 - 4 | string | These four fields are customizable text values for the count memo. |
CustomLookup1 - 4 | string | These four fields are customizable lookup values for the count memo. |
<span class="api-gn">Response: CountMemos: CountMemoItems</span> | | <span class="api-gd">A group containing the following fields and groups. This group is an array with zero or more entries.</span> |
RecCreated | string, datetime | A timestamp of when the record was created. |
RecModified | string, datetime | A timestamp of when the record was last modified. |
CountMemoItemId | string, guid | A unique identifier of the item in the count memo. <span class="ir">????????</span> |
CountMemoHeaderId | string, guid | A unique identifier of the count memo header. <span class="ir">????????</span> |
LedgerQty | double | <span class="ir">????????</span> |
ScannedQty | double | <span class="ir">????????</span> |
OverrideQty | double | <span class="ir">????????</span> |
DifferenceQty | double | <span class="ir">????????</span> |
OverrideDateTime | string, dat-time | A timestamp of when the override occured. <span class="ir">????????</span> |
OverrideEmployeeIdentifier | string | An identifier of the employee who performed the override. <span class="ir">????????</span> |
UPC | string | The item's universal product code. |
CLU | string | The items's custom lookup number. |
ExternalId | string | An identifier of the item used when interacting with an exgternal system. |
Plu | int32 | The item's product lookup number. |
StyleNo | string | An identifier of the style which contains the item. |
Description1 - 4 | string | These four fields are descriptions of the item. |
Attribute1SetId | string, guid | A unique identifier of the item's first attribute set. |
Attribute1SetCode | string | An identifier of the item's first attribute set. |
Attribute1SetDescription | string | A description of the item's first attribute set. |
Attribute1SetAlias | string | An alias (alternate identifier) of the item's first attribute set. |
Attribute1SetValueAlias1 - 2 | string | These two fields are aliases of the item's first attribute set value. |
Attribute1Id | string, guid | A unique identifier of the item's first attribute. |
Attribute1 | string | The item's first attribute. |
Attribute2SetId | string, guid | A unique identifier of the item's second attribute set. |
Attribute2SetCode | string | An identifier of the item's second attribute set. |
Attribute2SetDescription | string | A description of the item's second attribute set. |
Attribute2SetAlias | string | An alias (alternate identifier) of the item's second attribute set. |
Attribute2SetValueAlias1 - 2 | string | These two fields are aliases of the item's second attribute set value. |
Attribute2Id | string, guid | A unique identifier of the item's second attribute. |
Attribute2 | string | The item's second attribute. |
Attribute3SetId | string, guid | A unique identifier of the item's second attribute set. |
Attribute3SetCode | string | An identifier of the item's third attribute set. |
Attribute3SetDescription | string | A description of the item's third attribute set. |
Attribute3SetAlias | string | An alias (alternate identifier) of the item's third attribute set. |
Attribute3SetValueAlias1 - 2 | string | These two fields are aliases of the item's third attribute set value. |
Attribute3Id | string, guid | A unique identifier of the item's third attribute. |
Attribute3 | string | The item's third attribute. |
BrandName | string | The name of the item's brand. |
ManufactureName | string | The name of the item's manufacturer. |
DepartmentName | string | The name of the item's department. |
ClassName | string | The name of the item's class. |
<span class="api-gs">---</span> | | <span class="api-gde">end of Response: CountMemos: CountMemoItems</span> |
<span class="api-gs">---</span> | | <span class="api-gde">end of Response: CountMemos</span> |
<span class="api-gs">---</span> | | <span class="api-gde">end of Response</span> |

### Schema {#SuccessfulResponseSchema}
 
Below is the JSON source for the schema of a successful response to the export request as described above.

~~~
{
    "CountMemoExportToJson_get.ApiDocumentType":{
       "type":"object",
       "properties":{
          "ApiDocumentId":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "Status":{
             "enum":[
                "Successful"
             ],
             "type":"string"
          },
          "ApiRequestType":{
             "type":"string"
          },
          "TotalRecords":{
             "format":"int32",
             "type":"integer"
          },
          "RecordsCount":{
             "format":"int32",
             "type":"integer"
          },
          "ElapsedTime":{
             "format":"date-time",
             "type":"string"
          },
          "StartDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "EndDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "Response":{
             "$ref":"#/definitions/CountMemoExportToJson_get.ResponseType"
          }
       }
    },
    "CountMemoExportToJson_get.ResponseType":{
       "type":"object",
       "properties":{
          "CountMemos":{
             "type":"array",
             "items":{
                "$ref":"#/definitions/CountMemoExportToJson_get.CountMemosType"
             }
          }
       }
    },
    "CountMemoExportToJson_get.CountMemosType":{
       "type":"object",
       "properties":{
          "RecCreated":{
             "format":"date-time",
             "type":"string"
          },
          "RecModified":{
             "format":"date-time",
             "type":"string"
          },
          "CountMemoHeaderId":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "CountMemoId":{
             "type":"string"
          },
          "ExternalId":{
             "type":"string"
          },
          "CountDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "CountLocationDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "LocationIdentifier":{
             "type":"string"
          },
          "DeviceTransactionNumber":{
             "format":"int64",
             "type":"integer"
          },
          "ShortDTN":{
             "type":"string"
          },
          "Status":{
             "enum":[
                "Open",
                "Finalized",
                "Adjusted"
             ],
             "type":"string"
          },
          "Notes":{
             "type":"string"
          },
          "CreateDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "CreateEmployeeIdentifier":{
             "type":"string"
          },
          "EditDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "EditEmployeeIdentifier":{
             "type":"string"
          },
          "AdjustedDate":{
             "format":"date-time",
             "type":"string"
          },
          "AdjustedEmployeeIdentifier":{
             "type":"string"
          },
          "AdjustmentIdentifier":{
             "type":"string"
          },
          "FinalizedDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "FinalizedEmployeeIdentifier":{
             "type":"string"
          },
          "IsArchived":{
             "type":"boolean"
          },
          "TotalItemsInMemo":{
             "format":"int32",
             "type":"integer"
          },
          "TotalItemsCounted":{
             "format":"int32",
             "type":"integer"
          },
          "TotalQty":{
             "format":"int32",
             "type":"integer"
          },
          "ItemWithDifferences":{
             "format":"int32",
             "type":"integer"
          },
          "QtyDifferencesOver":{
             "format":"double",
             "type":"number"
          },
          "QtyDifferencesShor":{
             "format":"double",
             "type":"number"
          },
          "UnrecognizedItems":{
             "format":"int32",
             "type":"integer"
          },
          "CustomDate1":{
             "format":"date-time",
             "type":"string"
          },
          "CustomDate2":{
             "format":"date-time",
             "type":"string"
          },
          "CustomFlag1":{
             "type":"boolean"
          },
          "CustomFlag2":{
             "type":"boolean"
          },
          "CustomNumber1":{
             "format":"double",
             "type":"number"
          },
          "CustomNumber2":{
             "format":"double",
             "type":"number"
          },
          "CustomDecimal1":{
             "format":"double",
             "type":"number"
          },
          "CustomDecimal2":{
             "format":"double",
             "type":"number"
          },
          "CustomText1":{
             "type":"string"
          },
          "CustomText2":{
             "type":"string"
          },
          "CustomText3":{
             "type":"string"
          },
          "CustomText4":{
             "type":"string"
          },
          "CustomLookup1":{
             "type":"string"
          },
          "CustomLookup2":{
             "type":"string"
          },
          "CustomLookup3":{
             "type":"string"
          },
          "CustomLookup4":{
             "type":"string"
          },
          "CountMemoItems":{
             "type":"array",
             "items":{
                "$ref":"#/definitions/CountMemoExportToJson_get.CountMemoItemsType"
             }
          }
       }
    },
    "CountMemoExportToJson_get.CountMemoItemsType":{
       "type":"object",
       "properties":{
          "RecCreated":{
             "format":"date-time",
             "type":"string"
          },
          "RecModified":{
             "format":"date-time",
             "type":"string"
          },
          "CountMemoItemId":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "CountMemoHeaderId":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "LedgerQty":{
             "format":"double",
             "type":"number"
          },
          "ScannedQty":{
             "format":"double",
             "type":"number"
          },
          "OverrideQty":{
             "format":"double",
             "type":"number"
          },
          "DifferenceQty":{
             "format":"double",
             "type":"number"
          },
          "OverrideDateTime":{
             "format":"date-time",
             "type":"string"
          },
          "OverrideEmployeeIdentifier":{
             "type":"string"
          },
          "UPC":{
             "type":"string"
          },
          "CLU":{
             "type":"string"
          },
          "ExternalId":{
             "type":"string"
          },
          "Plu":{
             "format":"int32",
             "type":"integer"
          },
          "StyleNo":{
             "type":"string"
          },
          "Description1":{
             "type":"string"
          },
          "Description2":{
             "type":"string"
          },
          "Description3":{
             "type":"string"
          },
          "Description4":{
             "type":"string"
          },
          "Attribute1SetId":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "Attribute1SetCode":{
             "type":"string"
          },
          "Attribute1SetDescription":{
             "type":"string"
          },
          "Attribute1SetAlias":{
             "type":"string"
          },
          "Attribute1SetValueAlias1":{
             "type":"string"
          },
          "Attribute1SetValueAlias2":{
             "type":"string"
          },
          "Attribute1Id":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "Attribute1":{
             "type":"string"
          },
          "Attribute2SetId":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "Attribute2SetCode":{
             "type":"string"
          },
          "Attribute2SetDescription":{
             "type":"string"
          },
          "Attribute2SetAlias":{
             "type":"string"
          },
          "Attribute2SetValueAlias1":{
             "type":"string"
          },
          "Attribute2SetValueAlias2":{
             "type":"string"
          },
          "Attribute2Id":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "Attribute2":{
             "type":"string"
          },
          "Attribute3SetId":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "Attribute3SetCode":{
             "type":"string"
          },
          "Attribute3SetDescription":{
             "type":"string"
          },
          "Attribute3SetAlias":{
             "type":"string"
          },
          "Attribute3SetValueAlias1":{
             "type":"string"
          },
          "Attribute3SetValueAlias2":{
             "type":"string"
          },
          "Attribute3Id":{
             "format":"uuid",
             "type":"string",
             "example":"00000000-0000-0000-0000-000000000000"
          },
          "Attribute3":{
             "type":"string"
          },
          "BrandName":{
             "type":"string"
          },
          "ManufactureName":{
             "type":"string"
          },
          "DepartmentName":{
             "type":"string"
          },
          "ClassName":{
             "type":"string"
          }
       }
    }
 }
 ~~~

---

## Request Example(s) {#RequestExamples}

**Request Example #1: Status = 'Finalized' with CountMemoHeaderIdSetting = 'DTN'**

~~~
{
  "Source":"Integrator",
  "Data":{
    "ApiDocumentId":"907B65C7-8F2C-45FB-AEB2-68C5577D6162",
    "Request":{
      "Settings":[
        {
          "Key":"EmployeeIdentifierSetting",
          "Value":"LoginName"
        },
        {
          "Key":"LocationIdentifierSetting",
          "Value":"ExternalIdCode"
        },
        {
          "Key":"AdjustmentIdentifierSetting",
          "Value":"No"
        },
  		{
          "Key":"CountMemoHeaderIdSetting",
          "Value":"DTN"
        },
  		{
          "Key":"ShowCountMemoItemsSetting",
          "Value":"0"
        }   	
      ],
      "Filters":[
        {
          "Field":"Status",
          "Operator":"Equal",
          "Value":"Finalized"
        }
      ],
      "SortDescriptions":[
        {
          "Direction":"Ascending",
          "Name":"RecModified"
        }
      ],
      "Top":10,
      "Skip":0
    }
  }
}
~~~

**Request Example #2: DeviceTransactionNumber = 'GJDPNZ' with CountMemoHeaderIdSetting = 'ShortDTN'**

~~~
{
  "Source":"Integrator",
  "Data":{
    "ApiDocumentId":"907B65C7-8F2C-45FB-AEB2-68C5577D6162",
    "Request":{
      "Settings":[
        {
          "Key":"EmployeeIdentifierSetting",
          "Value":"LoginName"
        },
        {
          "Key":"LocationIdentifierSetting",
          "Value":"ExternalIdCode"
        },
        {
          "Key":"AdjustmentIdentifierSetting",
          "Value":"No"
        },
        {
          "Key":"CountMemoHeaderIdSetting",
          "Value":"ShortDTN"
        },
        {
          "Key":"ShowCountMemoItemsSetting",
          "Value":"0"
        }   		
      ],
      "Filters":[
        {
          "Field":"DeviceTransactionNumber",
          "Operator":"Equal",
          "Value":"GJDPNZ"
        }
      ],
      "SortDescriptions":[
        {
          "Direction":"Ascending",
          "Name":"RecModified"
        }
      ],
      "Top":10,
      "Skip":0
    }
  }
}
~~~

**Request Example #3: With ShowCountMemoItemsSetting = '1' (to receive count memos with their items)**

~~~
{
  "Source":"Integrator",
  "Data":{
    "ApiDocumentId":"907B65C7-8F2C-45FB-AEB2-68C5577D6162",
    "Request":{
      "Settings":[
        {
          "Key":"EmployeeIdentifierSetting",
          "Value":"LoginName"
        },
        {
          "Key":"LocationIdentifierSetting",
          "Value":"ExternalIdCode"
        },
        {
          "Key":"AdjustmentIdentifierSetting",
          "Value":"No"
        },
        {
          "Key":"CountMemoHeaderIdSetting",
          "Value":"ShortDTN"
        },
        {
          "Key":"ShowCountMemoItemsSetting",
          "Value":"1"
        }
   		
      ],
      "SortDescriptions":[
        {
          "Direction":"Ascending",
          "Name":"RecModified"
        }
      ],
      "Top":10,
      "Skip":0
    }
  }
}
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

**Response Example #3: Success when requesting DeviceTransactionNumber = '1000002'**

~~~
{
  "ApiDocument":{
    "ApiDocumentId":"F0B60FBD-80D3-4672-974C-7B2350D00D96",
    "Status":"Successful",
    "ApiRequestType":"countmemo-export",
    "TotalRecords":1,
    "RecordsCount":1,
    "ElapsedTime":"00:00:00.1100000",
    "StartDateTime":"2020-01-21T14:26:13.107",
    "EndDateTime":"2020-01-21T14:26:13.217",
    "Response":{
      "CountMemos":[
        {
          "RecCreated":"2020-01-21T13:16:18.707",
          "RecModified":"2020-01-21T13:16:18.707",
          "CountMemoHeaderId":"F9A7D12A-DFE0-40D2-80C3-04EEEFF0E478",
          "CountMemoId":"42492A51-1B4D-4AFF-BDC8-BEB97A5888BA",
          "ExternalId":"test ExternalId 3",
          "CountDateTime":"2020-01-21T13:16:18.707",
          "CountLocationDateTime":"2020-01-21T13:16:18.707",
          "LocationIdentifier":"HQ",
          "DeviceTransactionNumber":1000002,
          "ShortDTN":"LFLU",
          "Status":"Adjusted",
          "CreateDateTime":"2020-01-21T13:16:18.707",
          "CreateEmployeeIdentifier":"AUTOMAT",
          "EditDateTime":"2020-01-21T13:16:18.707",
          "EditEmployeeIdentifier":"AUTOMAT",
          "IsArchived":false,
          "TotalItemsInMemo":1010,
          "TotalItemsCounted":1010,
          "TotalQty":1010,
          "CustomFlag1":false,
          "CustomFlag2":false,
          "CustomNumber1":1020,
          "CustomNumber2":1030,
          "CustomDecimal1":10110.34000000000000000000,
          "CustomDecimal2":7080.78000000000000000000,
          "CountMemoItems":[
            {
              "RecCreated":"2020-01-21T13:19:30.220",
              "RecModified":"2020-01-21T13:19:30.220",
              "CountMemoItemId":"9DFFC73D-58CC-479E-83DD-2FABE6AC9259",
              "CountMemoHeaderId":"F9A7D12A-DFE0-40D2-80C3-04EEEFF0E478",
              "LedgerQty":10.00000000000000000000,
              "ScannedQty":10.00000000000000000000,
              "OverrideQty":11.00000000000000000000,
              "DifferenceQty":1.00000000000000000000,
              "OverrideDateTime":"2020-01-21T13:19:30.220",
              "OverrideEmployeeIdentifier":"AUTOMAT",
              "Item": {
                "UPC": "885398159208",
                "ExternalId": "885398159208",
                "Plu": 5370,
                "Attribute1SetValueAlias1": "",
                "Attribute1SetValueAlias2": "",
                "Attribute1Id": "9B15FF24-7FA5-4D18-893D-8F7CE6E88F4D",
                "Attribute1": "DEEP INDIGO",
                "Attribute2SetValueAlias1": "",
                "Attribute2SetValueAlias2": "",
                "Attribute2Id": "5A1D7C70-16FB-4F6B-8157-FAA499798516",
                "Attribute2": "36",
                "Attribute3SetValueAlias1": "",
                "Attribute3SetValueAlias2": "",
                "Attribute3Id": "972F9BD1-FA73-409E-B749-ADEB7591BDDB",
                "Attribute3": "32",
                "Style": {
                  "StyleNo": "315",
                  "Description1": "R00J9699",
                  "Description2": "",
                  "Description3": "",
                  "Description4": "\"R PLUS LOOSE FIT\" CORE JEAN",
                  "Attribute1SetId": "C20A34DD-20CC-43CB-8377-CDE7ACF9E53F",
                  "Attribute1SetCode": "COLOR",
                  "Attribute1SetDescription": "Color",
                  "Attribute1SetAlias": "",
                  "Attribute2SetId": "E3C0FA97-262B-4B53-9D6C-CDC49A1D6C1B",
                  "Attribute2SetCode": "MBOTSIZE",
                  "Attribute2SetDescription": "Mens Bottom Size",
                  "Attribute2SetAlias": "",
                  "Attribute3SetId": "E1B3474B-6D53-4BB4-98FC-7DABAE484AE7",
                  "Attribute3SetCode": "INSEAM",
                  "Attribute3SetDescription": "Inseam",
                  "Attribute3SetAlias": "",
                  "ManufactureName": "Rocawear"
                }
              }
            },
            {
              "RecCreated":"2020-01-21T13:19:30.220",
              "RecModified":"2020-01-21T13:19:30.220",
              "CountMemoItemId":"58BE45B4-F1D5-456A-88D0-9351600A3876",
              "CountMemoHeaderId":"F9A7D12A-DFE0-40D2-80C3-04EEEFF0E478",
              "LedgerQty":10.00000000000000000000,
              "ScannedQty":10.00000000000000000000,
              "OverrideQty":11.00000000000000000000,
              "DifferenceQty":1.00000000000000000000,
              "OverrideDateTime":"2020-01-21T13:19:30.220",
              "OverrideEmployeeIdentifier":"AUTOMAT",
              "Item": {
                "UPC": "885398458479",
                "ExternalId": "885398458479",
                "Plu": 4046,
                "Attribute1SetValueAlias1": "",
                "Attribute1SetValueAlias2": "",
                "Attribute1Id": "718288B8-CD22-40B9-8CA0-3238D3746E3D",
                "Attribute1": "NUTELLA",
                "Attribute2SetValueAlias1": "",
                "Attribute2SetValueAlias2": "",
                "Attribute2Id": "B803BDEF-90EE-4A27-A23C-87BD84D00380",
                "Attribute2": "2XL",
                "Style": {
                  "StyleNo": "290",
                  "Description1": "R0012W527",
                  "Description2": "",
                  "Description3": "",
                  "Description4": "S/S \"VOLUME 1\" SHIRT",
                  "Attribute1SetId": "C20A34DD-20CC-43CB-8377-CDE7ACF9E53F",
                  "Attribute1SetCode": "COLOR",
                  "Attribute1SetDescription": "Color",
                  "Attribute1SetAlias": "",
                  "Attribute2SetId": "2166921E-BEDA-4EFB-812F-75C31E69DB7B",
                  "Attribute2SetCode": "MTOPSIZE",
                  "Attribute2SetDescription": "Mens Top Size",
                  "Attribute2SetAlias": "",
                  "ManufactureName": "Rocawear"
                }
              }
            }
          ]
        }
      ]
    }
  }
}
~~~
