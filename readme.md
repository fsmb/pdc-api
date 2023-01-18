# Physician Data Center API

This is the source for technical information for the Physician Data Center (PDC) API. This API can be used to

To learn more about FSMB APIs refer to the [Getting Started](https://github.com/fsmb/api-docs) guide. To learn more about this API and to begin using it in your code please contact [FSMB](mailto:pdc@fsmb.org).

- URL
  - Demo: `https://services-pdc-demo.fsmb.org`
  - Production: `https://services-pdc.fsmb.org`
- Authentication URL `{baseUrl}/connect/token`
- [Postman Workspace](https://www.postman.com/crimson-shadow-2749/workspace/public-fsmb/collection/1384052-02136600-b1c0-4c59-be37-8297eb08e185)
- [OpenAPI Specification](https://services-pdc-demo.fsmb.org/swagger/v1/swagger.json)

Are you migrating from the legacy PDC web service? If so then refer to the [Migrating from the PDC Web service](docs/migration-webservice.md) documentation for information on migrating to the new API.

## Change Log

| Version | Date | Release Notes |
| - | - | - |
| 1.0 | 18 Aug 2022 | Initial version |

## Security

### Scopes

| Scope | Description |
| - | - |
| pdc.member_read | Read member information including reports. |
| pdc.member_write | Update member information including generating reports. |
| pdc.search | Search for physicians. |

## Resources

- [Members](docs/members-v1/readme.md)
- [Search](docs/search-v1/readme.md)
