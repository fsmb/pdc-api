# PhysicianSearchResult

Physician search results

| Field | Type | Required | Description |
| - | - | - | - |
| fid | string (format: digits, len: 9) | Y | FID of the physician |
| name | [PhysicianName](physician-name.md) | Y | Name of the physician |
| alternateNames | [PhysicianName[]](physician-name.md) | N | Alterate names |
| npi | string (format: digits, len: 10) | N | NPI number |
| medicalSchool | string (len: 100) | N | Medical School name |
| graduationYear | string (format: digits, len: 4) | N | Graduation year |
| practitionerType | string (len: 5) | N | Practitioner type |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*
