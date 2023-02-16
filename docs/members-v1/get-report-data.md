# Get Report Data

Gets the report data.

```HTTP
GET {baseUrl}/v1/rosters/{customerKey}/members/{fid}/reports/{reportId}/data
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
| 200 OK | [PdcReport](../definitions/report.md) | Success |
| 204 No Content | | Report not available. |
| 400 Bad Request | [ProblemDetails](../definitions/problem-details.md) | FID is invalid. |
| 404 Not Found | | Report not found. |

## Security

### Scopes

- `pdc.member_read`

## Examples

### Get a Report

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999915/reports/2447717/data
```

#### Sample Response

Status code: 200

```json
{
    "fid": "999999915",
    "reportId": 2447717,
    "asOfDateTimeUtc": "2023-01-18T19:13:07.03Z",
    "generatedByUser": "apiuser",
    "boardActionStatus": "Alerted",
    "names": {
        "legal": {
            "firstName": "Philip",
            "middleName": "James",
            "lastName": "Testermancho",
            "suffix": "",
            "reportDate": "2022-07-25T00:00:00"
        },
        "other": [
            {
                "firstName": "Philip",
                "middleName": "James",
                "lastName": "Testman",
                "suffix": "",
                "reportDate": "2011-11-11T00:00:00"
            }
        ]
    },
    "birthDate": {
        "month": "08",
        "day": "08",
        "year": "1978",
        "date": "1978-08-08T00:00:00",
        "reportDate": "2011-11-11T00:00:00"
    },
    "medicalEducation": {
        "school": {
            "name": "West Virginia University School of Medicine",
            "alternateNames": [],
            "cibisCode": "049030",
            "schoolTypeCode": "MD",
            "schoolTypeDescription": "Doctor of Medicine",
            "city": "Morgantown",
            "stateCode": "WV",
            "stateDescription": "West Virginia",
            "countryCode": "US",
            "countryDescription": "UNITED STATES",
            "isVerified": false,
            "reportDate": "2011-11-11T00:00:00"
        },
        "graduationDate": {
            "year": "2004",
            "isVerified": false,
            "reportDate": "2011-11-11T00:00:00"
        },
        "degree": {
            "code": "MD",
            "description": "Doctor of Medicine",
            "isVerified": false,
            "reportDate": "2011-11-11T00:00:00"
        }
    },
    "licenses": [
        {
            "reportDate": "2011-11-11T00:00:00",
            "licenseType": "Administrative",
            "issuerName": "ALABAMA",
            "issuerDescription": "Alabama State Board of Medical Examiners",
            "status": "Active",
            "licenseNumber": "TEST1111",
            "issueDate": "2010-07-01T00:00:00",
            "expirationDate": "2030-06-30T00:00:00"
        },
        {
            "reportDate": "2011-11-11T00:00:00",
            "licenseType": "Teaching",
            "issuerName": "ALASKA",
            "issuerDescription": "Alaska State Medical Board",
            "status": "Expired",
            "licenseNumber": "TEST2222",
            "issueDate": "2001-07-01T00:00:00",
            "expirationDate": "2012-06-30T00:00:00"
        },
        {
            "reportDate": "2011-11-11T00:00:00",
            "licenseType": "Full",
            "issuerName": "ARIZONA",
            "issuerDescription": "Arizona Medical Board",
            "status": "Active",
            "licenseNumber": "TEST3333",
            "issueDate": "2010-07-01T00:00:00",
            "expirationDate": "2030-06-30T00:00:00"
        },
        {
            "reportDate": "2011-11-11T00:00:00",
            "licenseType": "Full",
            "issuerName": "NEW HAMPSHIRE",
            "issuerDescription": "New Hampshire Board of Medicine",
            "status": "Active",
            "licenseNumber": "TEST555",
            "issueDate": "2004-07-01T00:00:00",
            "expirationDate": "2030-06-30T00:00:00"
        }
    ],
    "npi": [
        {
            "npiNumber": "1435537299",
            "entityType": "Individual",
            "reportDate": "2021-01-29T00:00:00"
        }
    ],
    "abms": {
        "certifications": [
            {
                "reportDate": "2022-02-28T00:00:00",
                "boardName": "American Board of Internal Medicine",
                "certificateName": "Internal Medicine",
                "isCertified": true,
                "certificateStatus": "Active",
                "certificateType": "General"
            },
            {
                "reportDate": "2022-02-28T00:00:00",
                "boardName": "American Board of Internal Medicine",
                "certificateName": "Cardiovascular Disease",
                "isCertified": true,
                "certificateStatus": "Active",
                "certificateType": "Subspecialty"
            }
        ]
    },
    "aoa": {
        "certifications": []
    }
}
```

### Get a Report With an Invalid ID

#### Sample Request

```HTTP
GET /v1/rosters/me/members/999999915/reports/12345/data
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
