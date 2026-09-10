---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get the webhooks health status

Returns the health status (`healthy`, `unhealthy`, or `unknown`) of the webhooks system based on the last ten minutes of activity.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `webhook_subscriptions:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Webhooks"
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
      "Webhooks-Health-Check-Status": {
        "description": "The representation of a webhooks health check response",
        "type": "object",
        "x-examples": {
          "success_status": {
            "status": "healthy",
            "last_checked_at": "2025-09-08T21:21:38.000Z"
          }
        },
        "properties": {
          "status": {
            "type": "string",
            "description": "Latest health status of the webhooks system",
            "readOnly": true,
            "enum": [
              "healthy",
              "unhealthy",
              "unknown"
            ]
          },
          "last_checked_at": {
            "type": "string",
            "format": "date-time",
            "readOnly": true,
            "description": "ISO8601 timestamp of the last successful health check with millisecond precision"
          }
        }
      }
    },
    "securitySchemes": {
      "CompanyAccessAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "Company-level authentication"
      },
      "SystemAccessAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "System-level authentication"
      }
    }
  },
  "paths": {
    "/v1/webhooks/health_check": {
      "get": {
        "summary": "Get the webhooks health status",
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
        "operationId": "get-v1-webhooks-health_check",
        "security": [
          {
            "SystemAccessAuth": []
          }
        ],
        "description": "Returns the health status (`healthy`, `unhealthy`, or `unknown`) of the webhooks system based on the last ten minutes of activity.\n\n📘 System Access Authentication\n\nThis endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)\n\nscope: `webhook_subscriptions:read`",
        "tags": [
          "Webhooks"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Webhooks-Health-Check-Status/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Webhooks-Health-Check-Status"
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
