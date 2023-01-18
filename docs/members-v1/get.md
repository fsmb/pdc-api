# Get

Get a member in the roster.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/members/{fid}
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
| 200 | [Member](../definitions/member.md) | Success |
| 404 | | Member not found |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get a Member with a Board Action

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999915
```

#### Sample Response

Status code: 200

```json
{
    "fid": "999999915",
    "fullName": "Philip James Testermancho",
    "birthDate": "1978-08-08",
    "boardActionStatus": "Alerted",
    "currentReport": {
        "reportId": 2447717,
        "reportDateUtc": "2023-01-18T19:13:07Z",
        "reportGeneratedBy": "apiuser",
        "reportStatus": "Succeeded",
        "isComplete": true,
        "boardActionStatus": "Alerted"
    }
}
```

### Get a Member with No Board Actions

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999907
```

#### Sample Response

Status code: 200

```json
{
    "fid": "999999907",
    "fullName": "Alexa Wood Checkey",
    "birthDate": "1988-09-02",
    "boardActionStatus": "Cleared",
    "currentReport": {
        "reportId": 2447718,
        "reportDateUtc": "2023-01-18T19:23:07Z",
        "reportGeneratedBy": "apiuser",
        "reportStatus": "Succeeded",
        "isComplete": true,
        "boardActionStatus": "Cleared"
    }
}
```
