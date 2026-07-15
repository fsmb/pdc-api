# Physician Data Center API

This is the source for technical information for the Physician Data Center (PDC) API. This API can be used to

To learn more about FSMB APIs refer to the [Getting Started](https://github.com/fsmb/api-docs) guide. To learn more about this API and to begin using it in your code please contact [FSMB](mailto:pdc@fsmb.org).

- URL
  - Demo: `https://services-pdc-demo.fsmb.org`
  - Production: `https://services-pdc.fsmb.org`
- Authentication URL `{baseUrl}/connect/token`
- [Postman Workspace](https://www.postman.com/crimson-shadow-2749/workspace/public-fsmb/collection/1384052-b6bdb300-274f-49a4-bfc3-007b0b8ce7e7?action=share&creator=1384052&active-environment=1384052-3b1223b5-7521-47cc-89fc-5aea17b8f878)
- [OpenAPI Specification](https://services-pdc-demo.fsmb.org/swagger/v1/swagger.json)

Are you migrating from the legacy PDC web service? If so then refer to the [Migrating from the PDC Web service](docs/migration-webservice.md) documentation for information on migrating to the new API.

## Change Log

| Date | Release Notes |
| - | - |
| July 2026  | Added Invoice Status and Search v2 endpoints |
| 16 Feb 2023 | Added PDC data |
| 18 Aug 2022 | Initial version |

## Security

### Scopes

| Scope | Description |
| - | - |
| pdc.member_read | Read member information including reports. |
| pdc.member_write | Update member information including generating reports. |
| pdc.search | Search for physicians. |

## Resources

- [Members](docs/members-v1/readme.md)
- [Search v2](docs/search-v2/readme.md)
- [(DEPRECATED) Search](docs/search-v1/readme.md) 
- [Reports](docs/reports-v1/readme.md)
