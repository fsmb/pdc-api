# Migrating from the PDC Web Service

- [Scenarios](#scenarios)
  - [Searching for a Physician](#searching-for-a-physician) 
  - [Adding a Member](#adding-a-member)
  - [Generating a New Report](#generating-a-new-report)
  - [Getting the Current Report](#getting-the-current-report)
  - [Determining If a Member Has Board Actions](#determining-if-a-member-has-board-actions)
- [Mapping XML to JSON](#mapping-xml-to-json)
  - [General Guidelines](#general-guidelines)
  - [Types](#types)
  - [Casing](#casing)
  - [Default Values](#default-values)
  
Migrating from the PDC web service to the PDC API will require some significant changes to client code. The following lists some of the larger changes that will need to be made.

- Protocol: The PDC web service was a SOAP service that relied on a binary transfer protocol. The PDC API is a REST API that uses the standard HTTPS protocol.
- Data Format: The PDC web service used XML as a data format. The PDC API uses the modern JSON data format.
- Security: The PDC web service used an API key model for authentication. The PDC API uses the standard [OAuth2](https://github.com/fsmb/api-docs/blob/master/docs/authentication.md) client credentials authentication.
- Caller Provided Data: The PDC web service required that clients maintain a unique search ID for each physician. The PDC API is FID based like other FSMB APIs.

The PDC API provides the following benefits over the older PDC web service.

- Works on any platform and with any language that supports HTTP (the web browsing protocol) without the need for complex code or proxies.
- Supports standard HTTP features like consistent responses, server caching and redirects.
- Uses a simple HTTP-based convention for working with clients.
- Uses OAuth2 to allow for "least privilege" access to data.
- Uses JSON which is an easy to read and write data format that is more concise than XML and more flexible.
- Is accessible over the standard HTTP(S) ports so no additional firewall rules are needed.

Refer to the [Getting Started](https://github.com/fsmb/api-docs) documentation on how to get started using FSMB APIs.

*Note: At this time not all features of the PDC web service are available in the PDC API. New features will be added until the PDC API has equivalent functionality to the PDC web service, when appropriate.*

## Scenarios

### Searching For a Physician

In the PDC web service clients submitted physician information to the service and waited for the physician to be matched. Matching was done out of process and could take a while.
Clients had to poll the web service to check the status of the match. If a physician was matched then they were added to the roster and a report was automatically generated.
If a physician was not matched then no report was generated. This process had a few issues.

- A unique "search ID" must be maintained by the client and passed to the web service. If the "search ID" was already used then the web service matches to the same physician.
- It was not possible to check the status of the match process without handling errors.

The PDC API approaches matching differently. A client may match a physician by providing similar data as provided in the web service. The matching happens immediately and either a success or failure is returned.
It is not necessary to poll the API for the match results. If a match occurs then the FID is returned that is needed for subsequent calls.

Unlike the web service, matching a physician does not automatically add the physician to the roster or generate a report. Since searching and adding to roster are different processes 
a client may search for any number of physicians without regard for the contents of the roster. Rosters are FID-based. If a client already has a FID for a physician, obtained using any FSMB API, then it is not necessary to search for a physician.

### Adding a Member

In the PDC web service clients added physicians to the roster by submitting a new member. In the PDC API any physician can be added to the roster provided the FID is known.
The FID can be obtained using any service provided by FSMB including searching using the PDC or MED APIs or via data exchanges with FSMB. Once a FID is acquired then use the [Add Member](members-v1/add.md) endpoint to add the physician to the roster.

Once a physician is added to a roster then a report is automatically generated for the member.

### Generating a New Report

To generate a new report for a member use the [Generate Report](members-v1/generate-report.md) endpoint. The only required data is the FID of the member. The FID must already be a member of the roster.
If a client is ensure whether the FID is already a member or not then call the [Get Member](members-v1/get.md) endpoint with the FID first.

Generating a report can take a while so the client must poll for the member status using the [Get Current Report](members-v1/get-current-report.md) endpoint, or similar.
Clients should check the `isComplete` or `reportStatus` fields to determine if the report is generated or not.

### Getting the Current Report

To get the current report for a member use the [Get Current Report](members-v1/get-current-report.md) endpoint. Check the `isComplete` or `reportStatus` fields to determine if the report has been generated.
If a report is being generated then clients should poll the API until the report is generated. This can take a few minutes so clients should delay before querying again.

If a report is available the endpoint returns a summary of the report. To get the PDF version of the report use the [Get Current Report PDF](members-v1/get-current-report-pdf.md) endpoint. At this time the PDC data is not available in a structured format.

### Determining If a Member Has Board Actions

To determine if a member has a board action use the [Get Current Report](members-v1/get-current-report.md) endpoint to get the current report, if any. The `boardActionStatus` field indicates whether the member has any board actions or not. Refer to the documentation on [BoardActionStatus](definitions/board-action-status.md) for the possible values and their meaning.

The [MemberReportSummary](definitions/member-report-summary.md) type also includes when the report was generated. It is recommended that a new report be generated if the current report is too old, as defined by the client.

## Mapping XML to JSON

The biggest challenge for migrating from the web service to the API is mapping the existing XML elements to their JSON equivalent. This section will discuss the general mapping between XML and JSON. Note that not every XML element has a corresponding JSON object. Furthermore the meaning and value of JSON objects may differ from their XML counterparts.

### Types

JSON is not a typed language. The JSON definitions are logical types used to make it easier to discuss the layout of the data. The definition names have no meaning in JSON nor do they show up in any data sent or received. This is in contrast to XML where the "types" are defined by the XML element names. 

Some types warrant additional guidelines.

#### Dates

In JSON dates are represented using the format `yyyy-mm-dd`. All endpoints accepting or returning dates uses this format. 

#### Enumerations

In JSON enumerated values are represented using strings. This allows for enumerations to change over time without breaking the object. However clients need to ensure they properly handle enumerated values they do not recognize.

#### Strings

In JSON strings are freeform text values. Unless otherwise stated string lengths are not enforced in JSON. Any documentation providing string lengths should be taken as an upper bound that could change over time.

### Casing

Like XML, case matters in JSON. In XML Pascal casing is generally used. In JSON camel casing is always used. Pay careful attention to casing when writing code.

### Default Values

In XML elements are generally provided even if they are empty. In JSON objects and values are generally only included if there is a valid. Clients should assume that missing values have their default value (empty string for strings, 0 for numbers, etc). It is also possible in JSON to get more fields than documented. Client code should only process fields that are relevant to them and ignore any other fields. It is not a breaking change to add new fields to an existing JSON object.

