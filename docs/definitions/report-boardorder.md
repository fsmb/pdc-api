# Board Order 

Board order.

| Name | Type | Required | Description |
| - | - | - | - |
| orderId | integer (format: int64) | Yes | Order ID. |
| usmleId | string (len: 8) | No | USMLE ID. |
| issueDate | string (date) | Yes | Issue date. |
| effectiveDate | string (date) | No | Effective date. |
| appealDate | string (date) | No | Appeal date. |
| disciplinaryEntity | [BoardOrderEntity](report-boardorder-entity.md) | Yes | Disciplinary entity. |
| actions | [BoardOrderAction](report-boardorder-action.md)[] | Yes | Actions |
| actionForm | [BoardOrderActionForm](report-boardorder-action-form.md) | No | Action form. |
| bases | [BoardOrderBasis](report-boardorder-basis.md)[] | No | Bases |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*