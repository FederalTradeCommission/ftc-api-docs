# Do Not Call (DNC) Reported Calls Data
The Do Not Call (DNC) Reported Calls Data API endpoint provides data every weekday about Do Not Call and robocall complaints reported to the Federal Trade Commission. This data consists of information [reported by consumers](https://www.donotcall.gov/), including the telephone number originating the unwanted call, the date the complaint was created, the time the call was made, the consumer's city and state locations reported, the subject of the call, and whether the call was a robocall. None of the information about the reported calls is verified. This data is typically updated each weekday by about noon Eastern time. Weekend data is updated on Monday and holiday data is updated on the next business day. Recent weekly data is also available in [CSV format](https://www.ftc.gov/site-information/open-government/data-sets/do-not-call-data).

For official aggregate Do Not Call data, please see the FTC's [Tableau Public dashboard](https://public.tableau.com/profile/federal.trade.commission#!/vizhome/DoNotCallComplaints/Robocalls) and the annual [National Do Not Call Registry Data Book](https://www.ftc.gov/enforcement/consumer-sentinel-network/reports#DNC).

More information about FTC APIs is on the [FTC for Developers](https://www.ftc.gov/developer) page.

***

## List all DNC Complaints
    
<pre>GET /v0/dnc-complaints</pre>

### Request

#### Path Parameters

_(none)_

#### Query Parameters

| **Parameter**  | **Type** | **Value** |
| :---          | :---          | :---          |
| `api_key`  | _(string)_ | _Required (unless provided in X-Api-Key header field)._ A valid api.data.gov API key. You can request an API key at [API Key Signup Form](https://api.data.gov/signup). |
| `created_date`    | _(string)_ | _Optional._ Filter records by a specific date that complaints were created during.<br /><br />For example, show all complaints created on February 26, 2020:<br />_Example:_ `?created_date="2020-02-26"`<br /><br />Note: Date value must be enclosed in double-quotes. |
| `created_date_from<br />created_date_to` | _(string)_ | _Optional._ Filter records by a range of dates/times that complaints were created. These filters must be used together. Can be combined with any one these filters: `state`, `area_code`, or `is_robocall`. When combined with the `state` filter, an optional `city` filter can be added.<br /><br />For example, show all complaints created between February 26, 2020 and February 27, 2020:<br />`?created_date_from="2020-02-26"&created_date_to="2020-02-27"`<br /><br />Note: Date/time values must be enclosed in double-quotes. If only date values are provided, data will be filtered from midnight on `created_date_from` to 11:59:59pm on `created_date_to`. Time values can be specified using ISO-8601 format: "YYYY-MM-DD HH:MM:SS".|
| `violation_date` | _(string)_ | _Optional._ Filter records by a specific date that unwanted calls were received during.<br /><br />For example, show all unwanted calls received on February 26, 2020:<br />`?violation_date="2020-02-26"`<br /><br />Note: Date value must be enclosed in double-quotes.|
| `violation_date_from<br />violation_date_to` | _(string)_ | _Optional._ Filter records by a range of dates/times that unwanted calls were received during.<br /><br />For example, show all unwanted calls received between February 26, 2020 and February 27, 2020:<br />`?violation_date_from="2020-02-26"&violation_date_to="2020-02-27"`<br /><br />Note: Date/time values must be enclosed in double-quotes. If only date values are provided, data will be filtered from midnight on `violation_date_from` to 11:59:59pm on `violation_date_to`. Time values can be specified using ISO-8601 format: "YYYY-MM-DD HH:MM:SS".|
| `state` | _(string)_ | _Optional._ Filter records by a state that complaints originated from. Can be combined with the `city` and `created_date_from` / `created_date_to` filters.<br /><br />For example, show all complaints originating from Idaho:<br />`?state="Idaho"`<br /><br />Note: Value that include spaces must be enclosed in double-quotes.|
| `city` | _(string)_ | _Optional._ Filter records by a city that complaints originated from. This filter must be used together with the `state` filter. Can be combined with the `created_date_from` / `created_date_to`  filters.<br /><br />For example, show all complaints originating from Phoenix, Arizona:<br />`?state="Arizona"&city="Phoenix"`<br /><br />Note: Value that include spaces must be enclosed in double-quotes.|
| `area_code` | _(integer)_ | _Optional._ Filter records by the area code that complaints originated from. Can be combined with the `created_date_from` / `created_date_to` filters.<br /><br />For example, show all complaints originating from the 360 area code:<br />`?area_code=360`|
| `is_robocall` | _(string)_ | _Optional._ Filter by whether the unwanted call was a recorded message / robocall or not. Value must be either "true" or "false". Can be combined with the `created_date_from` / `created_date_to` filters.<br /><br />For example, only show complaints that were recorded messages / robocalls:<br />`?is_robocall=true`|
| `sort_order` | _(string)_ | _Optional._ Sort direction to use with the sort_by parameter.<br />DESC = Sort in descending order (default)<br />ASC = Sort in ascending order.<br />Example: `?sort_order=`|
| `items_per_page` | _(integer)_ | _Optional._ Maximum number of records to include in JSON response. By default, the endpoint displays a maximum of 50 records per request - this is also the maximum value allowed. All non-empty responses include pagination metadata, which can be used to iterate over a large number of records, by sending a GET request for each page of records.<br />Example: `?items_per_page=10` |
| `offset` | _(integer)_ | _Optional._ Offset by a number of records, allowing a particular section of paginated results to be requested (use with the items_per_page parameter).<br />Example: `?offset=10` |

### Response Parameters
Response parameters are described at the end of this page.

### Response Format
All responses are in JSON format. The JSON object structure loosely adheres to the [jsonapi.org](http://jsonapi.org/) spec. Possible responses:
 
| HTTP&nbsp;Status&nbsp;Code | Type | Description | 
| :---             | :--- | :---        |
| 200 | OK | List of DNC Complaint records (in JSON format).|
| 400 | Error | Request URL does not use HTTPS (which is required for all API requests). |
| 403 | Error | API key is missing or invalid. See api.data.gov [General Web Service Errors](https://api.data.gov/docs/errors/) for further details. |
| 404 | Error | The API endpoint requested could not be found. |
| 429 | Error | The rate limit has been exceeded for the API key provided. |

### Example

List all DNC Complaints created on February 27, 2020, between 4:10am and 4:30am (showing most recent items first):  
[https://api.ftc.gov/v0/dnc-complaints?api_key=DEMO_KEY&created_date_from="2020-02-27 04:10:00"&created_date_to="2020-02-27 04:30:00"](https://api.ftc.gov/v0/dnc-complaints?api_key=DEMO_KEY&amp;created_date_from=%222020-02-27%2004:10:00%22&amp;created_date_to=%222020-02-27%2004:30:00%22)

<pre>
{
  data: [
    {
      type: "dnc_complaint",
      id: "2dae54c3d3c06d1960689139d39c3138",
      attributes: {
        company-phone-number: "6785050054",
        created-date: "2020-02-27 04:23:11",
        violation-date: "2020-02-26 16:00:00",
        consumer-city: "Earlysville",
        consumer-state: "Virginia",
        consumer-area-code: "434",
        subject: "Computer & technical support",
        recorded-message-or-robocall: "N"
      },
      relationships: [ ],
      meta: [ ],
      links: {
        self: "https://api.ftc.gov/v0/dnc-complaints/2dae54c3d3c06d1960689139d39c3138"
      }
    },
    {
      type: "dnc_complaint",
      id: "2dae54c3d3c06d1960689139d39c2fb3",
      attributes: {
        company-phone-number: "5162681355",
        created-date: "2020-02-27 04:13:57",
        violation-date: "2020-02-25 00:00:00",
        consumer-city: "Marion",
        consumer-state: "Illinois",
        consumer-area-code: "618",
        subject: "Lotteries, prizes & sweepstakes",
        recorded-message-or-robocall: "N"
      },
      relationships: [ ],
      meta: [ ],
      links: {
        self: "https://api.ftc.gov/v0/dnc-complaints/2dae54c3d3c06d1960689139d39c2fb3"
      }
    }
  ],
  meta: {
    records-this-page: 2,
    record-total: 2
  },
  links: {
    self: "https://api.ftc.gov/v0/dnc-complaints?created_date_from=%222020-02-27%2004:10:00%22&created_date_to=%222020-02-27%2004:30:00%22"
  }
}
</pre>

***

## Get a single DNC Complaint

<pre>GET /v0/dnc-complaints/<strong>{id}</strong></pre>

### Request

#### Path Parameters
| **Path&nbsp;Parameter**  | **Type** | **Value** |
| :---          | :---          | :---          |
| `{id}`  | _(integer)_ | _Required._ A valid ID for a DNC Complaint record. |

#### Query Parameters
| **Parameter**  | **Type** | **Value** |
| :---          | :---          | :---          |
| `api_key`  | _(string)_ | _Required (unless provided in X-Api-Key header field)._ A valid api.data.gov API key. You can request an API key at [API Key Signup Form](https://api.data.gov/signup). |

### Response Parameters
Response parameters are described at the end of this page.

### Response Format
All responses are in JSON format. The JSON object structure loosely adheres to the [jsonapi.org](http://jsonapi.org/) spec. Possible responses:
 
| HTTP&nbsp;Status&nbsp;Code | Type | Description | 
| :---             | :--- | :---        |
| 200 | OK | List of DNC Complaint records (in JSON format).|
| 400 | Error | Request URL does not use HTTPS (which is required for all API requests). |
| 403 | Error | API key is missing or invalid. See api.data.gov [General Web Service Errors](https://api.data.gov/docs/errors/) for further details. |
| 404 | Error | The API endpoint requested could not be found. |
| 429 | Error | The rate limit has been exceeded for the API key provided. |

### Example

List DNC Complaints for ID = "2dae54c3d3c06d1960689139d39c3138" :
[https://api.ftc.gov/v0/dnc-complaints/2dae54c3d3c06d1960689139d39c3138?api_key=DEMO_KEY](https://api.ftc.gov/v0/dnc-complaints/2dae54c3d3c06d1960689139d39c3138?api_key=DEMO_KEY)

<pre>
{
  data: [
    {
      type: "dnc_complaint",
      id: "2dae54c3d3c06d1960689139d39c3138",
      attributes: {
        company-phone-number: "6785050054",
        created-date: "2020-02-27 04:23:11",
        violation-date: "2020-02-26 16:00:00",
        consumer-city: "Earlysville",
        consumer-state: "Virginia",
        consumer-area-code: "434",
        subject: "Computer & technical support",
        recorded-message-or-robocall: "N"
      },
      relationships: [ ],
      meta: [ ],
      links: {
        self: "https://api.ftc.gov/v0/dnc-complaints/2dae54c3d3c06d1960689139d39c3138"
      }
    }
  ],
  meta: {
    records-this-page: 1,
    record-total: 1
  },
  links: {
    self: "https://api.ftc.gov/v0/dnc-complaints/2dae54c3d3c06d1960689139d39c3138?api_key=DEMO_KEY"
  }
}
</pre>

***

## Response Parameters

| **Parameter&nbsp;Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**  | **Type** | **Value** |
| :---                | :---     | :---      |
| `data`    | _(array)_ | An array of DNC Complaint record objects. |
| \|- `type`  | _(string)_  | The record type (for this endpoint, the `type` is "dnc_complaint"). |
| \|- `id`    | _(string)_ | The record ID. |
| \|- `attributes`    | _(object)_ | An object containing the main data for this record. |
| \|---- `company-phone-number`    | _(string)_ | _Optional (may be empty)._ The telephone number the unwanted call orignated from. |
| \|---- `created-date`    | _(string)_ | The date/time the complaint was created. Timestamp format is [ISO 8601](https://www.w3.org/TR/NOTE-datetime).<br />Example: `1997-07-16T19:20:30+01:00` |
| \|---- `violation-date`     | _(string)_ | The date/time the unwanted call was received. Timestamp format is [ISO 8601](https://www.w3.org/TR/NOTE-datetime). |
| \|---- `consumer-city`     | _(string)_ | _Optional (may be empty)._ The city reported by the consumer who created the complaint. |
| \|---- `consumer-state`    | _(string)_ | _Optional (may be empty)._ The state reported by the consumer who created the complaint. |
| \|---- `consumer-area-code`       | _(string)_ | _Optional (may be empty)._ The area code of the consumer that created the complaint. |
| \|---- `subject`    | _(string)_ | _Optional (may be empty)._ The subject of the unwanted call. |
| \|---- `recorded-message-or-robocall`    | _(string)_ | _Optional (may be empty)._ Indicates whether the unwanted call was a recorded message / robocall ("Y"), or not ("N"). |
| \|- `relationships` | _(array)_ | An array of other records related to this record. |
| \|- `meta`    | _(array)_ | An array of metadata for this record. |
| \|- `links`   | _(object)_ | An object containing links pertaining to this record. |
| \|---- `self`  | _(url)_  | The URL for this record. |
| `meta`     | _(object)_  | An object containing metadata for the request itself, including pagination data. |
| \|- `page`    | _(string)_  | The page number for the list of records in this response. |
| \|- `pages-total`       | _(string)_  | The total number of result pages for the request. |
| \|- `records-this-page` | _(string)_  | The number of records included in this response. |
| \|- `records-total`     | _(string)_  | The total number of records found for the request. |
| `links`    | _(object)_  | An object containing links pertaining to the request itself. |
| \|- `self`    | _(url)_  | The URL of the request. |

***

## Changelog

_None (as of 4/3/20)_