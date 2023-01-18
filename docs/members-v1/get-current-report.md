# Get Current Report

Gets the current report summary.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/members/{fid}/reports/current
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |
| fid | path | Yes | string (format: [FID](../definitions/fid.md)) | FID of the member. |

## Responses

| Name | Type | Description |
| - | - | - |
| 200 | [MemberReportSummary](../definitions/member-report-summary.md) | Success |
| 204 | | Report not available. |
| 400 | [ProblemDetails](../definitions/problem-details.md) | FID is invalid. |
| 404 | | Report not found. |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get an Alerted Report

Get a report for a member who has one or more board actions.

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999915/reports/current
```

#### Sample Response

Status code: 200

```json
{
    "reportId": 2447717,
    "reportDateUtc": "2023-01-18T19:13:07Z",
    "reportGeneratedBy": "user.apiuser",
    "reportStatus": "Succeeded",
    "isComplete": true,
    "boardActionStatus": "Alerted"
}
```

### Get a Cleared Report

Get a report for a member who has no board actions.

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999907/reports/current
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
