# Medical School

PDC medical school.

| Name | Type | Required | Description |
| - | - | - | - |
| name | string (len: 100) | Yes | School name. |
| alternateNames | string[] (len: 100) | No | Alternate school names. |
| cibisCode | string (len: 6) | Yes | CIBIS code. |
| schoolTypeCode | string (len: 5) | Yes | Type of school (e.g. MD, DO) |
| schoolTypeDescription | string (len: 100) | Yes | Description of the school type. |
| city | string (len: 50) | No | City. |
| stateCode | string (len: 3) | No | State or province code. |
| stateDescription | string (len: 100) | No | State or province description. |
| countryCode | string (len: 2) | No | ISO country code. |
| countryDescription | string (len: 100) | No | Country description. |
| isVerified | boolean | Yes | Is the school verified? |
| reportDate | string (date) | Yes | Report date. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*
