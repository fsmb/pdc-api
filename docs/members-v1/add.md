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
| fid | string (format: [FID](../definitions/fid.md)) | Yes | FID of the physician. |
| ignoreExisting | boolean | No | Ignore any existing member with the same FID. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*

The request contains the FID of the physician to add. If the physician is already a member of the roster then a 409 is returned unless `ignoreExisting` is set to `true`.

After a member is added to the roster then a report is generated for the new member. It is not necessary to generate the report using the API.

## Responses

| Name | Type | Description |
| - | - | - |
| 200 OK | [Member](../definitions/member.md) | Success |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | FID is invalid or the request has bad data. |
| 409 Conflict | | Member already exists and `ignoreExisting` is not set. |

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
