# Search

Search for a physician.

```HTTP
POST {baseUrl}/v2/rosters/{customerKey}/search
```

## URI Parameters

| Name | In | Required | Type | Description |
| - | - | - | - | - |
| baseUrl | path | Yes | string | The API URL. |
| customerKey | path | Yes | string | The customer key or `me`. |

## Request Body

| Name | Type | Required | Description |
| - | - | - | - |
| name | string (len: 160, minLen: 3) | Yes | Physician name |
| birthDate | string (date, format: yyyy-mm-dd) | * | Date of birth (One required: BirthDate, Npi, LicenseNumber) |
| npi | string (len: 10, format: digits) | * | NPI number (One required: BirthDate, Npi, LicenseNumber) |
| licenseNumber | string (len: 16) | * | License number (One required: BirthDate, Npi, LicenseNumber) |
| licenseState | string (len: 25) | No | State of licensure (use the full name such as `Texas`) |
| medicalSchool | string (len: 100) | No | Medical school name |
| graduationYear | string (len: 4, format: digits) | No | Graduation year |
| practitionerType | string (len: 5) | No | Practitioner type (one of: MD, DO, PA) |

Name and at least one of the following fields are required:

- `birthDate`
- `npi`
- `licenseNumber`

Clients should pass as much information as possible to improve the changes of finding a physician.

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*

## Responses

| Name | Type | Description |
| - | - | - |
| 200 OK | [PagedList](../definitions/paged-list.md) of [PhysicianSearchResult](definitions/paged-physician-search-result.md) | Success |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | Bad request. Ensure that all search data is provided. |

## Remarks

The search uses the same rules as the PDC application. The response is a list of physicians that potentially match the search request. Passing in all available information will improve the odds of getting a good match.
The API will not return all matches in all cases. The number of matches returned is specified by the `pageSize` in the response's paging metadata.

A physician is not automatically added to the roster. To add a physician to the roster use the [Add Member](../members-v1/add.md) endpoint.

## Security

### Scopes

- `pdc.search`

## Examples

### Search by Birth Date

#### Sample Request

```HTTP
POST /v2/rosters/me/search
```

Request body

```json
{
  "name": "Alexa Wood Checkey",
  "birthDate": "1988-09-02"
  "graduationYear": "2014",
  "practitionerType": "MD"
}
```

#### Sample Response

Status code: 200

```json
{
   "metadata": {
      "page": 1,
      "pageSize": 25,
      "totalItems": 1
   },
   "items": [
   {
      "fid": "999999907",
      "name": "Alexa Wood Checkey",
      "graduationYear": "2014",
      "practitionerType": "MD"
   }
   ]
}
```

### Search by License Number

#### Sample Request

```HTTP
POST /v2/rosters/me/search
```

Request body

```json
{
  "name": "Philip James Testman",  
  "licenseNumber": "TEST2222",
  "medicalSchool": "West Virginia University School of Medicine",
  "practitionerType": "MD"
}
```

#### Sample Response

Status code: 200

```json
{
   "metadata": {
      "page": 1,
      "pageSize": 25,
      "totalItems": 1
   },
   "items": [
   {
      "fid": "999999915",
      "name": "Philip James Testman",
      "medicalSchool": "West Virginia University School of Medicine",
      "practitionerType": "MD"
   }
   ]
}
```

### Search with No Match

#### Sample Request

```HTTP
POST /v2/rosters/me/search
```

Request body

```json
{
  "name": "Robert Finaling",
  "birthDate": "1944-01-06",
  "graduationYear": "1960",
  "practitionerType": "MD"
}
```

#### Sample Response

Status code: 200

```json
{
   "metadata": {
      "page": 1,
      "pageSize": 25,
      "totalItems": 0
   },
   "items": []
}
```
