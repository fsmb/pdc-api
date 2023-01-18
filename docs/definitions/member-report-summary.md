# Member Report Summary

Report summary.

| Name | Type | Required | Description |
| - | - | - | - |
| reportId | integer (format: int64) | Yes | ID of the report. |
| reportDateUtc | string (format: date-time) | Yes | Date and time of the report in UTC. Available once the report is generated. |
| reportStatus | string (format: [ReportStatus](report-status.md)) | Yes | Status of the report. |
| isComplete | boolean | Yes | Determines if the report has been generated. |
| boardActionStatus | string (format: [BoardActionStatus](board-action-status.md)) | Yes | Board action status once the report is generated. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*
