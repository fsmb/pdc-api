# Migrating from the PDC Web Service

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

## Searching For a Physician

In the PDC web service clients submitted physician information to the service and waited for the physician to be matched. Matching was done out of process and could take a while.
Clients had to poll the web service to check the status of the match. If a physician was matched then they were added to the roster and a report was automatically generated.
If a physician was not matched then no report was generated. This process had a few issues.

- A unique "search ID" must be maintained by the client and passed to the web service. If the "search ID" was already used then the web service matches to the same physician.
- It was not possible to check the status of the match process without handling errors.

The PDC API approaches matching differently. A client may match a physician by providing similar data as provided in the web service. The matching happens immediately and either a success or failure is returned.
It is not necessary to poll the API for the match results. If a match occurs then the FID is returned that is needed for subsequent calls.

Unlike the web service, matching a physician does not automatically add the physician to the roster or generate a report. Since searching and adding to roster are different processes 
a client may search for any number of physicians without regard for the contents of the roster. Rosters are FID-based. If a client already has a FID for a physician, obtained using any FSMB API, then it is not necessary to search for a physician.

## Adding a Member

In the PDC web service clients added physicians to the roster by submitting a new member. In the PDC API any physician can be added to the roster provided the FID is known.
The FID can be obtained using any service provided by FSMB including searching using the PDC or MED APIs or via data exchanges with FSMB. Once a FID is acquired then use the [Add Member](members-v1/add.md) endpoint to add the physician to the roster.

Once a physician is added to a roster then a report is automatically generated for the member.

## Generating a New Report

To generate a new report for a member use the [Generate Report](members-v1/generate-report.md) endpoint. The only required data is the FID of the member. The FID must already be a member of the roster.
If a client is ensure whether the FID is already a member or not then call the [Get Member](members-v1/get.md) endpoint with the FID first.

Generating a report can take a while so the client must poll for the member status using the [Get Current Report](members-v1/get-current-report.md) endpoint, or similar.
Clients should check the `isComplete` or `reportStatus` fields to determine if the report is generated or not.

## Getting the Current Report

To get the current report for a member use the [Get Current Report](members-v1/get-current-report.md) endpoint. Check the `isComplete` or `reportStatus` fields to determine if the report has been generated.
If a report is being generated then clients should poll the API until the report is generated. This can take a few minutes so clients should delay before querying again.

If a report is available the endpoint returns a summary of the report. To get the PDF version of the report use the [Get Current Report PDF](members-v1/get-current-report-pdf.md) endpoint. At this time the PDC data is not available in a structured format.

