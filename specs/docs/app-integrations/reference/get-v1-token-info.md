---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get info about the current access token

Returns scope and resource information associated with the current access token. Use this endpoint to verify the following for the current access token:
* Resource (company, employee, contractor, or application) and resource owner
* Access level

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Introspection"
    }
  ],
  "info": {
    "title": "Gusto API",
    "version": "2026-06-15",
    "termsOfService": "https://gusto.com/about/terms/developer-terms-of-service",
    "description": "Welcome to Gusto's Embedded Payroll API documentation!",
    "contact": {
      "name": "Developer Relations",
      "email": "developer@gusto.com"
    },
    "x-release-status": "stable"
  },
  "servers": [
    {
      "url": "https://api.gusto-demo.com",
      "description": "Demo",
      "x-speakeasy-server-id": "demo"
    }
  ],
  "security": [
    {
      "CompanyAccessAuth": []
    }
  ],
  "components": {
    "schemas": {
      "Token-Info": {
        "type": "object",
        "properties": {
          "scope": {
            "type": "string",
            "description": "Space-separated list of OAuth scopes granted to this access token.\n",
            "example": "companies:read public"
          },
          "resource": {
            "type": [
              "object",
              "null"
            ],
            "description": "The resource associated with this access token. Null when\nthe token has no associated resource.\n",
            "properties": {
              "type": {
                "type": "string",
                "description": "The type of resource associated with the access token, e.g. `Company` for a company-level token or `Oauth::Application` for a system-level token.\n",
                "example": "Company"
              },
              "uuid": {
                "type": "string",
                "format": "uuid",
                "description": "The UUID of the associated resource",
                "example": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a"
              }
            }
          },
          "resource_owner": {
            "type": [
              "object",
              "null"
            ],
            "description": "The resource owner (user) who authorized this access token. Null for\nsystem-level tokens or when the owner cannot be determined.\n",
            "properties": {
              "type": {
                "type": "string",
                "enum": [
                  "CompanyAdmin",
                  "Employee",
                  "Contractor"
                ],
                "description": "The type of resource owner:\n- `CompanyAdmin`: A company administrator\n- `Employee`: An employee\n- `Contractor`: A contractor\n",
                "example": "CompanyAdmin"
              },
              "uuid": {
                "type": "string",
                "format": "uuid",
                "description": "The UUID of the resource owner",
                "example": "8fdc31f0-a8a7-4872-a9f1-dcb5e6f876e3"
              }
            }
          }
        },
        "x-examples": {
          "company_admin_token": {
            "scope": "companies:read public",
            "resource": {
              "type": "Company",
              "uuid": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a"
            },
            "resource_owner": {
              "type": "CompanyAdmin",
              "uuid": "8fdc31f0-a8a7-4872-a9f1-dcb5e6f876e3"
            }
          },
          "system_token": {
            "scope": "partner_managed_companies:create public",
            "resource": {
              "type": "Oauth::Application",
              "uuid": "9c2a1b3d-4e5f-6789-abcd-ef0123456789"
            },
            "resource_owner": null
          }
        }
      }
    },
    "securitySchemes": {
      "CompanyAccessAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "Company-level authentication"
      }
    }
  },
  "paths": {
    "/v1/token_info": {
      "get": {
        "summary": "Get info about the current access token",
        "parameters": [
          {
            "name": "X-Gusto-API-Version",
            "in": "header",
            "schema": {
              "type": "string",
              "enum": [
                "2026-06-15"
              ],
              "default": "2026-06-15"
            },
            "description": "Determines the date-based API version associated with your API call. If none is provided, your application's [minimum API version](https://docs.gusto.com/embedded-payroll/docs/api-versioning#minimum-api-version) is used."
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-token-info",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns scope and resource information associated with the current access token. Use this endpoint to verify the following for the current access token:\n* Resource (company, employee, contractor, or application) and resource owner\n* Access level",
        "tags": [
          "Introspection"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "company_admin_token": {
                    "value": {
                      "$ref": "#/components/schemas/Token-Info/x-examples/company_admin_token"
                    }
                  },
                  "system_token": {
                    "value": {
                      "$ref": "#/components/schemas/Token-Info/x-examples/system_token"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Token-Info"
                }
              }
            }
          }
        }
      }
    }
  }
}
```
