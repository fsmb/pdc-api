# NPI

PDC NPI.

| Name | Type | Required | Description |
| - | - | - | - |
| npiNumber | string (len: 10) | Yes | NPI number. |
| entityType | string (len: 20) | Yes | Entity type (e.g. `Individual`, `Group`). |
| reportDate | string (date) | Yes | Report date. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*
