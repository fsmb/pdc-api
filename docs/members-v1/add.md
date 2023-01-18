# Add

Add a member to the roster.

```HTTP
POST {baseUrl}/v1/rosters/{customerKey}/members
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |

## Request Body

| Name | Type | Required | Description |
| - | - | - | - |
| fid | string (format: [Fid](../definitions/fid.md)) | Yes | FID of the physician. |
| ignoreExisting | boolean | No | Ignore any existing member with the same FID. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*

## Responses

| Name | Type | Description |
| - | - | - |
| 200 | [Member](../definitions/member.md) | Success |
| 400 | [ProblemDetails](../definitions/problem-details.md) | FID is invalid or the request has bad data. |
| 409 | | Member already exists and `ignoreExisting` is not set. |

## Security

### Scopes

- `pdc.member_write`

## Examples

### Add a Member

#### Sample Request

```HTTP
POST /v1/rosters/me/members
```

Request body

```json
{
  "fid": "999999915",
  "ignoreExisting": true
}
```

#### Sample Response

Status code: 200

The response indicates a report is being generated.

```json
{
    "fid": "999999915",
    "fullName": "Philip James Testermancho",
    "birthDate": null,
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
