# Get Invoice Status

Get the payment status for a PDC report invoice.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/reports/{reportId}/invoice
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |
| reportId | path | Yes | integer (format: int64) | ID of the report. |

## Responses

| Name | Type | Description |
| - | - | - |
| 200 OK | [PaymentStatus](../definitions/payment-status.md) | Success |
| 204 No Content | | Report not available. |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | Report ID is invalid. |
| 404 Not Found | | Report not found. |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get Invoice Status

#### Sample Request

```HTTP
GET /v1/rosters/me/reports/3182769/invoice
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
GET /v1/rosters/me/reports/3182760/invoice
```

#### Sample Response

Status code: 204 (No Content)
