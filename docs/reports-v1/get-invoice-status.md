# Get Invoice Status by ID

Gets the invoice status for a report.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/reports/{fid}/{reportId}/invoice
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |
| fid | path | Yes | string (format: FID) | FID of the physician. |
| reportId | path | Yes | integer (format: int64) | ID of the report. |

## Responses

| Name | Type | Description |
| - | - | - |
| 200 OK | [PaymentStatus](../definitions/payment-status.md) | Success |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | FID or report ID is invalid. |
| 401 Unauthorized | | |
| 404 Not Found | | Report not found. |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get Invoice Status

#### Sample Request

```HTTP
GET /v1/rosters/me/reports/999999915/3182769/invoice
```

#### Sample Response

Status code: 200

```json
{
    "isPaid": true
}
```

### Get Invoice Status With an Incorrect Report ID

#### Sample Request

```HTTP
GET /v1/rosters/me/reports/999999915/3182760/invoice
```

#### Sample Response

Status code: 404 (Not Found)
