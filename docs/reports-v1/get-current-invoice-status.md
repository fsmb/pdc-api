# Get Current Invoice Status

Gets the invoice status for the current report, if any.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/reports/{fid}/invoice
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |
| fid | path | Yes | string (format: FID) | FID of the physician. |

## Responses

| Name | Type | Description |
| - | - | - |
| 200 OK | [PaymentStatus](../definitions/payment-status.md) | Success |
| 204 No Content | | Report not available. Try again later. |
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
GET /v1/rosters/me/reports/999999915/invoice
```

#### Sample Response

Status code: 200

```json
{
    "isPaid": true
}
```
