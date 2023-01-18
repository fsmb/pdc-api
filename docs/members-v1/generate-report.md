# Generate Report

Generates a new report.

```HTTP
POST {baseUrl}/v1/rosters/{customerKey}/members/{fid}/reports
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
| 200 OK | [Member](../definitions/member.md) | Success |
| 202 Accepted | | Request already pending. |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | FID is invalid. |

## Security

### Scopes

- `pdc.member_write`

## Examples

### Generate a Report

#### Sample Request

```HTTP
POST /v1/rosters/me/members/999999915/reports
```

#### Sample Response

Status code: 200

The response indicates the report is being generated.

```json
{
    "fid": "999999915",
    "fullName": "Philip James Testermancho",
    "birthDate": "1978-08-08",
    "boardActionStatus": "Unknown",
    "currentReport": {
        "reportId": 0,
        "reportDateUtc": "0001-01-01T06:00:00Z",
        "reportGeneratedBy": "",
        "reportStatus": "Pending",
        "isComplete": false,
        "boardActionStatus": "Unknown"
    }
}
```
