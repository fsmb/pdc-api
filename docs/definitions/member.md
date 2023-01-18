# Member

Member information.

| Name | Type | Required | Description |
| - | - | - | - |
| fid | string (format: [FID](fid.md)) | Yes | FID of the member. |
| fullName | string (len: 100) | Yes | Full name of the member. |
| birthDate | string (format: date) | Yes | Date of birth. |
| boardActionStatus | string (format: [BoardActionStatus](board-action-status.md)) | Yes | Board action status. |
| currentReport | [MemberReportySummary](memory-report-summary.md) | Yes | Current report summary. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*
