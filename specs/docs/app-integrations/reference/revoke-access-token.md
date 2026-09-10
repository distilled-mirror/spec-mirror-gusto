---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Revoke access token

Revokes the given access token. After revoking, this token can no longer be used to make requests nor can it be refreshed.

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
    "securitySchemes": {
      "CompanyAccessAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "Company-level authentication"
      }
    }
  },
  "paths": {
    "/oauth/revoke": {
      "post": {
        "summary": "Revoke access token",
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
        "operationId": "revoke-access-token",
        "security": [],
        "description": "Revokes the given access token. After revoking, this token can no longer be used to make requests nor can it be refreshed.",
        "tags": [
          "Introspection"
        ],
        "x-gusto-integration-type": [
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "OK"
          }
        },
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "description": "",
                "required": [
                  "client_id",
                  "client_secret",
                  "token"
                ],
                "properties": {
                  "client_id": {
                    "type": "string",
                    "description": "Your client id"
                  },
                  "client_secret": {
                    "type": "string",
                    "description": "Your client secret"
                  },
                  "token": {
                    "type": "string",
                    "description": "The access token that will be revoked."
                  }
                }
              }
            }
          },
          "required": true
        }
      }
    }
  }
}
```
