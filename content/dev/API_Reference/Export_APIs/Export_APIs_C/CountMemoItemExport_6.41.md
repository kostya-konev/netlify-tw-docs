---
title: "Count Memo Item Export API [6.41]"
date: 2023-03-23T09:32:00-05:00
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

This topic describes the **Count Memo Item Export** API which is used to export count memo item information from CHQ.

See [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for a description on how export requests are made and on the standard request and response formats used. The API-Specific sucessful response format for this API will be described below.

{{% notice note %}}
For this API, a **Device Transaction Number** (**DTN**) is a value of the *BigInteger* type (for example, *100011311*). A **Short Device Transaction Number** (**ShortDTN**) is a value of the *Base36* type (for example, *GJDPNA*).
{{% /notice %}}

---

## Request endpoint {#RequestEndpoint}

Method: **POST**  
Synchronous URL: <span class="fg-brown">***\<your-chq-url\>***</span>**/chqapi/export/countmemo-item**  
HTTP Headers: **Content-Type: application/json**  
HTTP Headers: **ApiKey:** <span class="fg-brown">***\<your-api-key\>***</span>

<span class="fg-brown">***\<your-chq-url\>***</span> is the URL of your CHQ as supplied by Teamwork.  
<span class="fg-brown">***\<your-api-key\>***</span> is your API key value. See [*How to manage API keys*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToManageApiKeys_6.41/) for further info.

In the Swagger UI the **/chqapi/export/countmemo-item** endpoint is a member of the **Catalog** endpoint group.

## Request settings {#RequestSettings}

Below are the settings which can be supplied in the **Settings** group of the export request to define which value (field) is to be used for a particular value class (see [*How to make an export API request*](https://twdocs.netlify.app/dev/API_Reference/How_Tos/HowToMakeAnExportRequest_6.41/) for additional info).

The **Key** column lists the names of the available settings. The **Supported Values** column lists the valid values which can be supplied for the setting. The **Default** column lists the default value for each setting if that setting is not supplied.

**Key** | **Supported Values** | **Default** | **Description** |
---- | ---- | ---- | ---- |
EmployeeIdentifierSetting | LoginName, FullName, TeamworkId | LoginName | An indicator of which value is to be used to identify employees. |
ShowCountMemoItemSetting | DTN, ShortDTN | DTN | An indicator as to which value is to be used to identify items. |
CountMemoItemSearchSetting | Plu, UPC, CLU, ExternalId | Plu | An indicator of which value is to be used to search for items. <span class="ir">??????????</span> |

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
ItemSearch | "Equal" | Any one of the following valid values: "Plu", "UPC", ,"CLU",  "ExternalId". |

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
<span class="api-gn">Response: CountMemoItems</span> | | <span class="api-gd">A group containing the following fields and groups. This group is an array with zero or more entries.</span> |
RecCreated | string, datetime | A timestamp of when the record was created. |
RecModified | string, datetime | A timestamp of when the record was last modified. |
CountMemoItemId | string | An identifier of the count memo item. |
CountMemoHeaderId | string, guid | A unique identifier of the count memo header. <span class="ir">***????????***</span> |
CountMemoId | string | An identifier of the count memo. <span class="ir">***????????***</span> |
LedgerQty | double | <span class="ir">????????</span> |
ScannedQty | double | <span class="ir">????????</span> |
OverrideQty | double | <span class="ir">????????</span> |
DifferenceQty | double | <span class="ir">????????</span> |
OverrideDateTime | string, dat-time | A timestamp of when the override occured. <span class="ir">????????</span> |
OverrideEmployeeIdentifier | string | An identifier of the employee who performed the override. <span class="ir">????????</span> |
Item.UPC | string | The item's universa product code. |
Item.CLU | string | The items's custom lookup number. |
Item.ExternalId | string | An identifier of the item used when interacting with an exgternal system. |
Item.Plu | int32 | The item's product lookup number. |
Item.Attribute1SetValueAlias1 - 2 | string | These two fields are aliases of the item's first attribute set value. |
Item.Attribute1Id | string, guid | A unique identifier of the item's first attribute. |
Item.Attribute1 | string | The item's first attribute. |
Item.Attribute2SetValueAlias1 - 2 | string | These two fields are aliases of the item's second attribute set value. |
Item.Attribute2Id | string, guid | A unique identifier of the item's second attribute. |
Item.Attribute2 | string | The item's second attribute. |
Item.Attribute3SetValueAlias1 - 2 | string | These two fields are aliases of the item's third attribute set value. |
Item.Attribute3Id | string, guid | A unique identifier of the item's third attribute. |
Item.Attribute3 | string | The item's third attribute. |
Item.Style.StyleNo | string | An identifier of the style which contains the item. |
Item.Style.Description1 - 4 | string | These four fields are descriptions of the item's style. <span class="ir">??????????</span> |
Item.Style.Attribute1SetId | string, guid | A unique identifier of the item's style's first attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute1SetCode | string | An identifier of the item's style's first attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute1SetDescription | string | A description of the item's style's first attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute1SetAlias | string | An alias (alternate identifier) of the item's style's first attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute2SetId | string, guid | A unique identifier of the item's style's second attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute2SetCode | string | An identifier of the item's style's second attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute2SetDescription | string | A description of the item's style's second attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute2SetAlias | string | An alias (alternate identifier) of the item's style's second attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute3SetId | string, guid | A unique identifier of the item's style's third attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute3SetCode | string | An identifier of the item's style's third attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute3SetDescription | string | A description of the item's style's third attribute set.  <span class="ir">??????????</span> |
Item.Style.Attribute3SetAlias | string | An alias (alternate identifier) of the item's style's third attribute set.  <span class="ir">??????????</span> |
Item.Style.BrandName | string | The name of the item's style's brand. <span class="ir">??????????</span> |
Item.Style.ManufactureName | string | The name of the item's style's manufacturer. <span class="ir">??????????</span> |
Item.Style.DepartmentName | string | The name of the item's style's department. <span class="ir">??????????</span> |
Item.Style.ClassName | string | The name of the item's style's class. <span class="ir">??????????</span> |
<span class="api-gs">---</span> | | <span class="api-gde">end of Response: CountMemoItems</span> |
<span class="api-gs">---</span> | | <span class="api-gde">end of Response</span> |

### Schema {#SuccessfulResponseSchema}
 
Below is the JSON source for the schema of a successful response to the export request as described above.

~~~
{
   "CountMemoItemExportToJson_get.ApiDocumentType":{
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
            "$ref":"#/definitions/CountMemoItemExportToJson_get.ResponseType"
         }
      }
   },
   "CountMemoItemExportToJson_get.ResponseType":{
      "type":"object",
      "properties":{
         "CountMemoItems":{
            "type":"array",
            "items":{
               "$ref":"#/definitions/CountMemoItemExportToJson_get.CountMemoItemsType"
            }
         }
      }
   },
   "CountMemoItemExportToJson_get.CountMemoItemsType":{
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
         "CountMemoId":{
            "type":"string"
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
         "Item.UPC":{
            "type":"string"
         },
         "Item.CLU":{
            "type":"string"
         },
         "Item.ExternalId":{
            "type":"string"
         },
         "Item.Plu":{
            "format":"int32",
            "type":"integer"
         },
         "Item.Attribute1SetValueAlias1":{
            "type":"string"
         },
         "Item.Attribute1SetValueAlias2":{
            "type":"string"
         },
         "Item.Attribute1Id":{
            "format":"uuid",
            "type":"string",
            "example":"00000000-0000-0000-0000-000000000000"
         },
         "Item.Attribute1":{
            "type":"string"
         },
         "Item.Attribute2SetValueAlias1":{
            "type":"string"
         },
         "Item.Attribute2SetValueAlias2":{
            "type":"string"
         },
         "Item.Attribute2Id":{
            "format":"uuid",
            "type":"string",
            "example":"00000000-0000-0000-0000-000000000000"
         },
         "Item.Attribute2":{
            "type":"string"
         },
         "Item.Attribute3SetValueAlias1":{
            "type":"string"
         },
         "Item.Attribute3SetValueAlias2":{
            "type":"string"
         },
         "Item.Attribute3Id":{
            "format":"uuid",
            "type":"string",
            "example":"00000000-0000-0000-0000-000000000000"
         },
         "Item.Attribute3":{
            "type":"string"
         },
         "Item.Style.StyleNo":{
            "type":"string"
         },
         "Item.Style.Description1":{
            "type":"string"
         },
         "Item.Style.Description2":{
            "type":"string"
         },
         "Item.Style.Description3":{
            "type":"string"
         },
         "Item.Style.Description4":{
            "type":"string"
         },
         "Item.Style.Attribute1SetId":{
            "format":"uuid",
            "type":"string",
            "example":"00000000-0000-0000-0000-000000000000"
         },
         "Item.Style.Attribute1SetCode":{
            "type":"string"
         },
         "Item.Style.Attribute1SetDescription":{
            "type":"string"
         },
         "Item.Style.Attribute1SetAlias":{
            "type":"string"
         },
         "Item.Style.Attribute2SetId":{
            "format":"uuid",
            "type":"string",
            "example":"00000000-0000-0000-0000-000000000000"
         },
         "Item.Style.Attribute2SetCode":{
            "type":"string"
         },
         "Item.Style.Attribute2SetDescription":{
            "type":"string"
         },
         "Item.Style.Attribute2SetAlias":{
            "type":"string"
         },
         "Item.Style.Attribute3SetId":{
            "format":"uuid",
            "type":"string",
            "example":"00000000-0000-0000-0000-000000000000"
         },
         "Item.Style.Attribute3SetCode":{
            "type":"string"
         },
         "Item.Style.Attribute3SetDescription":{
            "type":"string"
         },
         "Item.Style.Attribute3SetAlias":{
            "type":"string"
         },
         "Item.Style.BrandName":{
            "type":"string"
         },
         "Item.Style.ManufactureName":{
            "type":"string"
         },
         "Item.Style.DepartmentName":{
            "type":"string"
         },
         "Item.Style.ClassName":{
            "type":"string"
         }
      }
   }
}
~~~

---

## Request Example(s) {#RequestExamples}

**Request Example #1: Status = 'Finalized' with CountMemoItemSetting = 'DTN'**

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
          "Key":"CountMemoItemSetting",
          "Value":"DTN"
        },
		{
          "Key":"CountMemoItemSearchSetting",
          "Value":"Plu"
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

**Request Example #2: DeviceTransactionNumber = 'GJDGXX' with CountMemoItemSetting = 'ShortDTN'**

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
          "Key":"CountMemoItemSetting",
          "Value":"ShortDTN"
        },
		{
          "Key":"CountMemoItemSetting",
          "Value":"DTN"
        },
		{
          "Key":"CountMemoItemSearchSetting",
          "Value":"Plu"
        }  		  			
      ],
      "Filters":[
        {
          "Field":"DeviceTransactionNumber",
          "Operator":"Equal",
          "Value":"GJDGXX"
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

**Request Example #3: ItemSearch ='9786059' with CountMemoItemSearchSetting = 'Plu'**

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
          "Key":"CountMemoItemSetting",
          "Value":"ShortDTN"
        },
        {
          "Key":"CountMemoItemSearchSetting",
          "Value":"Plu"
        }
      ],
      "Filters":[
        {
          "Field":"ItemSearch",
          "Operator":"Equal",
          "Value":"9786059"
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

**Response Example #3: Success when requesting ItemSearch = '9786059' with CountMemoItemSearchSetting = 'Plu'**

~~~
{
  "ApiDocument":{
    "ApiDocumentId":"D0A917E7-F3FF-43C4-B28D-C89E801CDC0E",
    "Status":"Successful",
    "ApiRequestType":"countmemo-item-export",
    "TotalRecords":2,
    "RecordsCount":2,
    "ElapsedTime":"00:00:00.2000000",
    "StartDateTime":"2020-01-28T14:51:41.290",
    "EndDateTime":"2020-01-28T14:51:41.490",
    "Response":{
      "CountMemoItems":[
        {
          "RecCreated":"2020-01-16T13:59:47.703",
          "RecModified":"2020-01-16T13:59:47.703",
          "CountMemoItemId":"EA58E7D3-545D-4970-B1C8-341A60389F67",
          "CountMemoHeaderId":"E1B9D5BE-EC3C-418A-96AC-67B0C6C5BD20",
          "CountMemoId":"GJDGXT",
          "LedgerQty":0.00000000000000000000,
          "ScannedQty":0.00000000000000000000,
          "DifferenceQty":0.00000000000000000000,
          "Item":{
            "Plu":9786059,
            "Attribute1SetValueAlias1":"MIDNIGHT WASH",
            "Attribute1SetValueAlias2":"",
            "Attribute1Id":"9BEE07B7-9CB8-49BF-86CF-AADAAABBF4E5",
            "Attribute1":"MIDNIGHT WASH",
            "Attribute2SetValueAlias1":"",
            "Attribute2SetValueAlias2":"",
            "Attribute2Id":"B258A0C9-256F-461A-981A-9F9917967CE6",
            "Attribute2":"39 (4)",
            "Style":{
              "StyleNo":"4256",
              "Description1":"",
              "Description2":"",
              "Description3":"",
              "Description4":"Tanya's Test 4256",
              "Attribute1SetId":"C20A34DD-20CC-43CB-8377-CDE7ACF9E53F",
              "Attribute1SetCode":"COLOR",
              "Attribute1SetDescription":"color description",
              "Attribute1SetAlias":"C_ALIAS",
              "Attribute2SetId":"4C6EC8CF-0C06-4BB8-9F50-5D696EF23DE6",
              "Attribute2SetCode":"SIZE",
              "Attribute2SetDescription":"Size",
              "Attribute2SetAlias":"Size",
              "BrandName":"WANDLER",
              "ManufactureName":"new era"
            }
          }
        },
        {
          "RecCreated":"2020-01-27T14:19:02.520",
          "RecModified":"2020-01-27T14:19:02.520",
          "CountMemoItemId":"BE19C524-7308-4FEB-8AAD-7204812FC268",
          "CountMemoHeaderId":"E8D15E53-0FBE-4A2C-BF4A-30171803BA6F",
          "CountMemoId":"GJDGXX",
          "LedgerQty":0.00000000000000000000,
          "ScannedQty":0.00000000000000000000,
          "DifferenceQty":0.00000000000000000000,
          "Item":{
            "Plu":9786059,
            "Attribute1SetValueAlias1":"MIDNIGHT WASH",
            "Attribute1SetValueAlias2":"",
            "Attribute1Id":"9BEE07B7-9CB8-49BF-86CF-AADAAABBF4E5",
            "Attribute1":"MIDNIGHT WASH",
            "Attribute2SetValueAlias1":"",
            "Attribute2SetValueAlias2":"",
            "Attribute2Id":"B258A0C9-256F-461A-981A-9F9917967CE6",
            "Attribute2":"39 (4)",
            "Style":{
              "StyleNo":"4256",
              "Description1":"",
              "Description2":"",
              "Description3":"",
              "Description4":"Tanya's Test 4256",
              "Attribute1SetId":"C20A34DD-20CC-43CB-8377-CDE7ACF9E53F",
              "Attribute1SetCode":"COLOR",
              "Attribute1SetDescription":"color description",
              "Attribute1SetAlias":"C_ALIAS",
              "Attribute2SetId":"4C6EC8CF-0C06-4BB8-9F50-5D696EF23DE6",
              "Attribute2SetCode":"SIZE",
              "Attribute2SetDescription":"Size",
              "Attribute2SetAlias":"Size",
              "BrandName":"WANDLER",
              "ManufactureName":"new era"
            }
          }
        }
      ]
    }
  }
}
~~~
