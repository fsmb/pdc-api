# Get Current Report Data

Gets the current report's data.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/members/{fid}/reports/current/data
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
| 200 OK | [PdcReport](../definitions/report.md) | Success |
| 204 No Content | | Report not available. |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | FID is invalid. |
| 404 Not Found | | Member or report not found. |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get a Report

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999915/reports/current/data
```

#### Sample Response

Status code: 200

### Get a Report for a Missing Member

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999949/reports/current/data
```

#### Sample Response

Status code: 400

```json
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-08bcb53430c7b05ba4c465974eafd4ef-0c5f7626d671a956-00"
}
```
