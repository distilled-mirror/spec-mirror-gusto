---
updatedAt: 2026-05-26T23:06:58.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a recurring reimbursement

Get a specific recurring reimbursement.

scope: `reimbursements:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Reimbursements"
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
      "Not-Found-Error-Object": {
        "description": "Not Found \n  \nThe requested resource does not exist. Make sure the provided ID/UUID is valid.",
        "type": "object",
        "required": [
          "errors"
        ],
        "properties": {
          "errors": {
            "type": "array",
            "items": {
              "type": "object",
              "required": [
                "error_key",
                "category"
              ],
              "properties": {
                "error_key": {
                  "type": "string",
                  "description": "Specifies where the error occurs. Typically this key identifies the attribute/parameter related to the error."
                },
                "category": {
                  "type": "string",
                  "description": "Specifies the type of error. The category provides error groupings and can be used to build custom error handling in your integration."
                },
                "message": {
                  "type": "string",
                  "description": "Provides details about the error - generally this message can be surfaced to an end user."
                }
              }
            }
          }
        },
        "x-examples": {
          "not_found": {
            "errors": [
              {
                "error_key": "request",
                "category": "not_found",
                "message": "The requested resource was not found."
              }
            ]
          },
          "deprecated_accept_terms_of_service": {
            "errors": [
              {
                "error_key": "request",
                "category": "deprecated_endpoint",
                "message": "The requested endpoint is no longer supported in the requested API version. Use POST /v1/partner_managed_companies/:company_uuid/terms_of_service instead"
              }
            ]
          },
          "deprecated_retrieve_terms_of_service": {
            "errors": [
              {
                "error_key": "request",
                "category": "deprecated_endpoint",
                "message": "The requested endpoint is no longer supported in the requested API version. Use PUT /v1/partner_managed_companies/:company_uuid/terms_of_service instead"
              }
            ]
          }
        }
      },
      "Recurring-Reimbursement": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "uuid": "b739f253-b028-443b-b6cf-97a555c3d493",
            "employee_uuid": "346e1409-1c97-4524-9ebb-0c0c169e35cb",
            "version": "cf9b64404e63d325c762aaad20ca7a39",
            "description": "Office supplies",
            "created_at": "2025-11-03T09:03:24.000-08:00",
            "updated_at": "2025-11-03T09:03:24.000-08:00",
            "amount": "75.50"
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The unique identifier of this recurring reimbursement.",
            "readOnly": true
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee.",
            "readOnly": true
          },
          "description": {
            "type": "string",
            "description": "The description of the reimbursement."
          },
          "amount": {
            "type": "string",
            "description": "The dollar amount of the reimbursement."
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "created_at": {
            "type": "string",
            "description": "The timestamp when this reimbursement was created.",
            "readOnly": true
          },
          "updated_at": {
            "type": "string",
            "description": "The timestamp when this reimbursement was last updated.",
            "readOnly": true
          }
        },
        "required": [
          "uuid",
          "employee_uuid",
          "description",
          "amount",
          "version"
        ]
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
    "/v1/recurring_reimbursements/{id}": {
      "get": {
        "summary": "Get a recurring reimbursement",
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
          },
          {
            "name": "id",
            "in": "path",
            "description": "The UUID of the reimbursement",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-recurring_reimbursements",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get a specific recurring reimbursement.\n\nscope: `reimbursements:read`",
        "tags": [
          "Reimbursements"
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
                      "$ref": "#/components/schemas/Recurring-Reimbursement/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Recurring-Reimbursement"
                }
              }
            }
          },
          "404": {
            "description": "Not Found",
            "content": {
              "application/json": {
                "examples": {
                  "not_found": {
                    "value": {
                      "$ref": "#/components/schemas/Not-Found-Error-Object/x-examples/not_found"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Not-Found-Error-Object"
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
