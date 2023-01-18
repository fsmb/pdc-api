# Get Report PDF

Gets a report as a PDF.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/members/{fid}/reports/{reportId}/pdf
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |
| fid | path | Yes | string (format: [FID](../definitions/fid.md)) | FID of the member. |
| reportId | path | Yes | integer (format: int64) | ID of the report. |

## Responses

| Name | Type | Description |
| - | - | - |
| 200 | string (format: binary) | Success |
| 204 | | Report not available. |
| 400 | [ProblemDetails](../definitions/problem-details.md) | FID is invalid. |
| 404 | | Report not found. |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get a Report

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999915/reports/2447717/pdf
```

#### Sample Response

Status code: 200

PDF is provided as response body.

### Get a Report With an Invalid ID

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999915/reports/12345/pdf
```

#### Sample Response

Status code: 404

```json
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "traceId": "00-23a668b19e91df4f17ba470400123e01-531e56cc9e4e4714-00"
}
```
