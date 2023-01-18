# Search

Search for a physician.

```HTTP
POST {baseUrl}/v1/rosters/{customerKey}/search
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |

## Request Body

| Name | Type | Required | Description |
| - | - | - | - |
| name | string (len: 100) | Yes | Full name of the physician. |
| birthDate | string (format: date) | Yes | Date of birth. |
| ssnLastFour | string (format: digits, len: 4) | No | Last four of the SSN. Either `ssnLastFour` or `licenseNumber` is required. |
| licenseNumber | string (len: 16) | No | License number. Either `ssnLastFour` or `licenseNumber` is required. |
| graduationYear | string (format: digits, len: 4) | No | Year of graduation. Either `graduationYear` or `medicalSchool` is required. |
| medicalSchool | string (len: 80) | No | Medical school name. Either `graduationYear` or `medicalSchool` is required. |
| degree | string (len: 5) | No | Degree code. |
| npi | string (format: digits, len: 10) | No | NPI number. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*

## Responses

| Name | Type | Description |
| - | - | - |
| 200 OK | [SearchResult](../definitions/search-result.md) | Success |
| 204 No Content | | No match. |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | Bad request. Ensure that all search data is provided. |

## Remarks

The search uses the same rules as the PDC application. If a match is found then it is returned. A physician is not automatically added to the roster. To add a physician to the roster use the [Add Member](../members-v1/add.md) endpoint.

## Security

### Scopes

- `pdc.search`

## Examples

### Search by SSN Last Four

#### Sample Request

```HTTP
POST /v1/rosters/me/search
```

Request body

```json
{
  "name": "Alexa Wood Checkey",
  "birthDate": "1988-09-02",
  "ssnLastFour": "8888",
  "graduationYear": "2014",
  "degree": "MD"
}
```

#### Sample Response

Status code: 200

```json
{
    "fid": "999999907",
    "name": "Alexa Wood Checkey"
}
```

### Search by Medical School

#### Sample Request

```HTTP
POST /v1/rosters/me/search
```

Request body

```json
{
  "name": "Philip James Testman",
  "birthDate": "1978-08-08",
  "licenseNumber": "TEST2222",
  "medicalSchool": "West Virginia University School of Medicine",
  "degree": "MD"
}
```

#### Sample Response

Status code: 200

```json
{
    "fid": "999999915",
    "name": "Philip James Testman"
}
```

### Search with No Match

#### Sample Request

```HTTP
POST /v1/rosters/me/search
```

Request body

```json
{
  "name": "Robert Finaling",
  "birthDate": "1944-01-06",
  "ssnLastFour": "7777",
  "graduationYear": "1960",
  "degree": "MD"
}
```

#### Sample Response

Status code: 204
