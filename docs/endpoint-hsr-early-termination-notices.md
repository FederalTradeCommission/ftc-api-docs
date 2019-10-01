# HSR Early Termination Notices
Under the Hart-Scott-Rodino (HSR) Act, parties to certain large mergers and acquisitions must file premerger notification and wait for government review. The parties may not close their deal until the waiting period outlined in the HSR Act has passed, or the government has granted **early termination** of the waiting period. The FTC provides daily updates of deals that receive early termination.
\- _Adapted from [Premerger Notification and the Merger Review Process](https://www.ftc.gov/tips-advice/competition-guidance/guide-antitrust-laws/mergers/premerger-notification-and-merger)._

***

## List all HSR Early Termination Notices
    
<pre>GET /v0/hsr-early-termination-notices</pre>

### Request

#### Path Parameters

_(none)_

#### Query Parameters

| **Parameter**  | **Type** | **Value** |
| :---          | :---          | :---          |
| `api_key`  | _(string)_ | _Required (unless provided in X-Api-Key header field)._ A valid api.data.gov API key. You can request an API key at [API Key Signup Form](https://api.data.gov/signup). |
| `keywords`    | _(string)_ | _Optional._ Filter records by keyword(s) that appear in the record title.<br /><br />Multiple keywords should be separated by plus (+) characters - this will return any record whose title contains one or more of the keywords provided (an OR operation).<br />_Example:_ `?keywords=Corporation+Incorporated`<br /><br />To match an explicit phrase, enclose it in double-quotes.<br />_Example:_ `?keywords="Health%20Plan"` |
| `transaction_number` | _(integer)_ | _Optional._ Filter records by transaction number.<br />_Example:_ `?transaction_number=20181111`|
| `last_updated` | _(integer)_ | _Optional._ Filter records by date/time the record was created or last updated. Filtering is based on a record&#39;s `created` and `updated` properties, and not its `date` property (the date the transaction was made).<br /><br />For example, show all records created/updated on or after March 27, 2018:<br />`?last_updated[value][month]=3&amp;last_updated[value][day]=27&amp;last_updated[value][year]=2018`<br /><br />Note: The [month], [day], and [year] parameters must all be included.|
| `sort_by` | _(string)_ | _Optional._ Sort records by various criteria.<br />created = Sort by when record was created<br />updated = Sort by when record was last updated<br />_Example:_ `?sort_by=created`|
| `sort_order` | _(string)_ | _Optional._ Sort direction to use with the `sort_by` parameter.<br />DESC = Sort in descending order (default)<br />ASC = Sort in ascending order.<br />_Example:_ `?sort_by=created&sort_order=ASC`|
| `items_per_page` | _(integer)_ | _Optional._ Maximum number of records to include in JSON response. All non-empty responses include pagination metadata, which can be used to iterate over a large number of records, by sending a GET request for each page of records.<br />_Example:_ `?items_per_page=10` |
| `offset` | _(integer)_ | _Optional._ Offset by a number of records, allowing a particular section of paginated results to be requested (use with the `items_per_page` parameter).<br />_Example:_ `?offset=10` |

### Response Parameters
Response parameters are described at the end of this page.

### Response Format
All responses are in JSON format. The JSON object structure loosely adheres to the [jsonapi.org](http://jsonapi.org/) spec. Possible responses:
 
| HTTP&nbsp;Status&nbsp;Code | Type | Description | 
| :---             | :--- | :---        |
| 200 | OK | List of HSR Early Termination Notice records (in JSON format).|
| 400 | Error | Request URL does not use HTTPS (which is required for all API requests). |
| 403 | Error | API key is missing or invalid. See api.data.gov [General Web Service Errors](https://api.data.gov/docs/errors/) for further details. |
| 404 | Error | The API endpoint requested could not be found. |
| 429 | Error | The rate limit has been exceeded for the API key provided. |

### Example

List all Early Termination Notices that include "Blockbuster" in the record title:  
[https://api.ftc.gov/v0/hsr-early-termination-notices?api_key=DEMO_KEY&keywords="Blockbuster"](https://api.ftc.gov/v0/hsr-early-termination-notices?api_key=DEMO_KEY&keywords="Blockbuster")

<pre>
{
    "data": [
        {
            "type": "early_termination_notice",
            "id": "128567",
            "attributes": {
                "title": "20110728: Charles W. Ergen; Blockbuster Inc. - Debtor-in-Possession",
                "transaction-number": "20110728",
                "acquired-entities": "Blockbuster Inc. - Debtor-in-Possession",
                "acquired-party": "Blockbuster Inc. - Debtor-in-Possession",
                "acquiring-party": "Charles W. Ergen",
                "date": "2011-04-08",
                "created": "2013-09-24 16:05:39",
                "updated": "2013-09-24 18:22:27",
                "tags": []
            },
            "relationships": [],
            "meta": [],
            "links": {
                "self": "http://www.ftc.gov/enforcement/premerger-notification-program/early-termination-notices/20110728"
            }
        },
        {
            "type": "early_termination_notice",
            "id": "128566",
            "attributes": {
                "title": "20110718: Carl C. Icahn; Blockbuster Inc. - Debtor-in-Possession",
                "transaction-number": "20110718",
                "acquired-entities": "Blockbuster Inc. - Debtor-in-Possession",
                "acquired-party": "Blockbuster Inc. - Debtor-in-Possession",
                "acquiring-party": "Carl C. Icahn",
                "date": "2011-04-11",
                "created": "2013-09-24 16:05:39",
                "updated": "2013-09-24 18:22:27",
                "tags": []
            },
            "relationships": [],
            "meta": [],
            "links": {
                "self": "http://www.ftc.gov/enforcement/premerger-notification-program/early-termination-notices/20110718"
            }
        }
    ],
    "meta": {
        "page": "1",
        "pages-total": "1",
        "records-this-page": "2",
        "records-total": "2"
    },
    "links": {
        "self": "http://api.ftc.gov/v0/hsr-early-termination-notices"
    }
}
</pre>

***

## Get a single HSR Early Termination Notice

<pre>GET /v0/hsr-early-termination-notices/<strong>{id}</strong></pre>

### Request

#### Path Parameters
| **Path&nbsp;Parameter**  | **Type** | **Value** |
| :---          | :---          | :---          |
| `{id}`  | _(integer)_ | _Required._ A valid ID for an HSR Early Termination Notice record. |

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
| 200 | OK | List of HSR Early Termination Notice records (in JSON format).|
| 400 | Error | Request URL does not use HTTPS (which is required for all API requests). |
| 403 | Error | API key is missing or invalid. See api.data.gov [General Web Service Errors](https://api.data.gov/docs/errors/) for further details. |
| 404 | Error | The API endpoint requested could not be found. |
| 429 | Error | The rate limit has been exceeded for the API key provided. |

### Example

List Early Termination Notices for ID = 128567 :  
[https://api.ftc.gov/v0/hsr-early-termination-notices/128567?api_key=DEMO_KEY](https://api.ftc.gov/v0/hsr-early-termination-notices/128567?api_key=DEMO_KEY)

<pre>
{
    "data": [
        {
            "type": "early_termination_notice",
            "id": "128567",
            "attributes": {
                "title": "20110728: Charles W. Ergen; Blockbuster Inc. - Debtor-in-Possession",
                "transaction-number": "20110728",
                "acquired-entities": "Blockbuster Inc. - Debtor-in-Possession",
                "acquired-party": "Blockbuster Inc. - Debtor-in-Possession",
                "acquiring-party": "Charles W. Ergen",
                "date": "2011-04-08",
                "created": "2013-09-24 16:05:39",
                "updated": "2013-09-24 18:22:27",
                "tags": []
            },
            "relationships": [],
            "meta": [],
            "links": {
                "self": "https://www.ftc.gov/enforcement/premerger-notification-program/early-termination-notices/20110728"
            }
        }
    ],
    "meta": {
        "page": "1",
        "pages-total": "1",
        "records-this-page": "1",
        "records-total": "1"
    },
    "links": {
        "self": "https://api.ftc.gov/v0/hsr-early-termination-notices/128567"
    }
}
</pre>

***

## Response Parameters

| **Parameter&nbsp;Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**  | **Type** | **Value** |
| :---                | :---     | :---      |
| `data`    | _(array)_ | An array of HSR Early Termination Notice record objects. |
| \|- `type`  | _(string)_  | The record type (for this endpoint, the `type` is "early_termination_notice"). |
| \|- `id`    | _(string)_ | The record ID. |
| \|- `attributes`    | _(object)_ | An object containing the main data for this record. |
| \|---- `title`    | _(string)_ | The record title. |
| \|---- `transaction-number`    | _(string)_ | The transaction number that corresponds to this record. |
| \|---- `acquired-entities`     | _(string)_ | The entities that were acquired. |
| \|---- `acquired-party`     | _(string)_ | The party that was acquired. |
| \|---- `acquiring-party`    | _(string)_ | The acquiring party. |
| \|---- `date`       | _(string)_ | The date the transaction was made. Timestamp format is [ISO 8601](https://www.w3.org/TR/NOTE-datetime).<br />Example: `1997-07-16T19:20:30+01:00`|
| \|---- `created`    | _(string)_ | The date/time the record was created. Timestamp format is [ISO 8601](https://www.w3.org/TR/NOTE-datetime). |
| \|---- `updated`    | _(string)_ | The date/time the record was last updated. Timestamp format is [ISO 8601](https://www.w3.org/TR/NOTE-datetime). |
| \|---- `tags`       | _(array)_ | An array of tags that have been applied to this record. |
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

_None (as of 4/23/18)_