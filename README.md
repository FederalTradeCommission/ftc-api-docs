FTC API
=======

This repository contains documentation for the FTC API and each of its endpoints. This documentation is also available on the FTC website at https://www.ftc.gov/developer.

The FTC API is read-only and allows various types of data to be requested, including the content that appears throughout the FTC website. Each type of data or content is accessible through a dedicated URL, commonly referred to as an "API endpoint". All API responses are in JSON format.

The URL path for the API is: `https://api.ftc.gov/v0`

The current API version is **v0**, indicating that the API is under active development - some aspects of the API may change, such as the filter syntax used in requests or the structure of response data.

Getting Started with the FTC API
--------------------------------

Access to the FTC API requires a Data.gov API key, which must be included in each API request. Register for a Data.gov API key using the API Key Signup Form at https://www.ftc.gov/developer.

The Data.gov API key can be included in an API request using either an **api_key** URL query parameter or with an `X-Api-Key` header. For example, here is a GET request to the HSR Early Termination Notices API endpoint (replace DEMO_KEY with your Data.gov API key):
[https://api.ftc.gov/v0/hsr-early-termination-notices?api_key=DEMO_KEY](https://api.ftc.gov/v0/hsr-early-termination-notices?api_key=DEMO_KEY)

Learn more about other FTC developer resources at https://www.ftc.gov/developer. The FTC also lists its API endpoints and public datasets on Data.gov at https://catalog.data.gov/organization/federal-trade-commission.