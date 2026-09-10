---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# List webhook subscriptions

Returns all webhook subscriptions associated with the provided Partner API token.

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
      "Webhook-Subscription": {
        "description": "The representation of webhook subscription.",
        "type": "object",
        "x-tags": [
          "Webhooks"
        ],
        "title": "",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the webhook subscription.",
            "readOnly": true
          },
          "url": {
            "type": "string",
            "description": "The webhook subscriber URL. Updates will be POSTed to this URL.",
            "readOnly": true
          },
          "status": {
            "type": "string",
            "enum": [
              "pending",
              "verified",
              "removed",
              "unreachable"
            ],
            "description": "The status of the webhook subscription.",
            "readOnly": true
          },
          "subscription_types": {
            "type": "array",
            "description": "Receive updates for these types.",
            "readOnly": false,
            "items": {
              "type": "string",
              "enum": [
                "BankAccount",
                "Company",
                "CompanyBenefit",
                "Contractor",
                "ContractorPayment",
                "Employee",
                "EmployeeBenefit",
                "EmployeeJobCompensation",
                "ExternalPayroll",
                "Form",
                "Location",
                "Notification",
                "Payroll",
                "PayrollSync",
                "PaySchedule",
                "Signatory",
                "TimeOffRequest"
              ]
            }
          }
        },
        "x-examples": {
          "Example": {
            "uuid": "c5fdae57-5483-4529-9aae-f0edceed92d4",
            "url": "https://partner-app.com/subscriber",
            "status": "verified",
            "subscription_types": [
              "BankAccount",
              "Company",
              "CompanyBenefit",
              "Contractor",
              "ContractorPayment",
              "Employee",
              "EmployeeBenefit",
              "EmployeeJobCompensation",
              "ExternalPayroll",
              "Form",
              "Location",
              "Notification",
              "Payroll",
              "PayrollSync",
              "PaySchedule",
              "Signatory"
            ]
          },
          "Pending": {
            "uuid": "a1b2c3d4-5678-90ab-cdef-1234567890ab",
            "url": "https://partner-app.com/webhooks",
            "status": "pending",
            "subscription_types": [
              "Company",
              "Employee"
            ]
          }
        },
        "required": [
          "uuid"
        ]
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
    "/v1/webhook_subscriptions": {
      "get": {
        "summary": "List webhook subscriptions",
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
        "operationId": "get-v1-webhook-subscriptions",
        "security": [
          {
            "SystemAccessAuth": []
          }
        ],
        "description": "Returns all webhook subscriptions associated with the provided Partner API token.\n\n📘 System Access Authentication\n\nThis endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)\n\nscope: `webhook_subscriptions:read`",
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
                  "Example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Webhook-Subscription/x-examples/Example"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Webhook-Subscription"
                  }
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
