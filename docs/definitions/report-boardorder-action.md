# Board Order Action

Board order action.

| Name | Type | Required | Description |
| - | - | - | - |
| actionCode | string (len: 5) | Yes | Action code. |
| actionDescription | string (len: 100) | Yes | Action description. |
| isPrejudicial | boolean | Yes | Is action prejudicial? |
| isIndefinite | boolean | Yes | Is action indefinite? |
| effectiveDate | string (date) | No | Action effective date. |
| expirationDate | string (date) | No | Action expiration date. |
| termYears | integer | No | Term years. |
| termMonths | integer | No | Term months. |
| termDays | integer | No | Term days. |
| actionStayed | [BoardOrderActionStayed](report-boardorder-action-stayed.md) | No | Action stayed. |
| comments | string (len: 1000) | No | Comments |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*