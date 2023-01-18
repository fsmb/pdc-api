# Problem Details

Problem details as defined by [RFC7807](https://www.rfc-editor.org/rfc/rfc7807).

| Name | Type | Required | Description |
| - | - | - | - |
| type | string | Yes | Error type. |
| title | string | Yes | Descriptive message. |
| status | string | No | Status code. |
| errors | * | No | Additional data related to error. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*
