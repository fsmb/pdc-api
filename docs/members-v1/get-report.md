# Get Report

Gets a report summary.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/members/{fid}/reports/{reportId}
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer Key or `me`. |
| fid | path | Yes | string (format: [FID](definitions/fid.md)) | FID of the member. |
| reportId | path | Yes | integer (format: int64) | ID of the report. |

## Responses

| Name | Type | Description |
| - | - | - |
| 200 | [MemberReportSummary](definitions/member-report-summary.md) | Success |
| 204 | | Report not available. |
| 400 | [ProblemDetails](problem-details.md) | FID is invalid. |
| 404 | | Report not found. |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get an Alerted Report

Get a report for a member who has one or more board actions.

#### Sample Request

```HTTP
GET {baseUrl}/v1/rosters/me/members/999999915/reports/2447717
```

#### Sample Response

Status code: 200

```json
{
    "reportId": 2447717,
    "reportDateUtc": "2023-01-18T19:13:07Z",
    "reportGeneratedBy": "apiuser",
    "reportStatus": "Succeeded",
    "isComplete": true,
    "boardActionStatus": "Alerted"
}
```

### Get a Cleared Report

Get a report for a member who has no board actions.

#### Sample Request

```HTTP
GET {baseUrl}/v1/rosters/me/members/999999907/reports/2447718
```

#### Sample Response

Status code: 200

```json
{
    "reportId": 2447718,
    "reportDateUtc": "2023-01-18T19:23:07Z",
    "reportGeneratedBy": "apiuser",
    "reportStatus": "Succeeded",
    "isComplete": true,
    "boardActionStatus": "Cleared"
}
```
