# PDC Report

PDC report.

| Name | Type | Required | Description |
| - | - | - | - |
| fid | string (format: digits, len: 9) | Yes | FID of the physician. |
| reportId | integer | Yes | Report ID |
| asOfDateTimeUtc | string (date-time) | Yes | Date and time the report was generated. |
| generatedByUser | string | No | User who generated the report. |
| boardActionStatus | string (len: 20) | Yes | Board action status. One of: `Cleared`, `Alerted` |
| boardOrders | [BoardOrder](report-boardorder.md)[] | No | Board orders, if any. |
| names | [Names](report-names.md) | Yes | Names. |
| birthDate | [BirthDate](report-birthdate.md) | No | Birth date. |
| medicalEducation | [MedicalEducation](report-medical-education.md) | No | Medical education. |
| licenses | [License](report-license.md)[] | No | License information. |
| npi | [Npi](report-npi.md)[] | No | NPI information. |
| abms | [Abms](report-abms.md) | No | ABMS information, if available. |
| aoa | [Aoa](report-aoa.md) | No | AOA information, if available. |
| dea | [Dea](report-dea.md) | No | DEA information, if available. |

*Note: Any fields marked as deprecated will be removed in a future version of the API. New code should not rely on these fields. Existing code should be updated to use alternative fields.*
