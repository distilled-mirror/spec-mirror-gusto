---
updatedAt: 2026-04-20T21:25:53.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get time off balances for a company

Get time off balances for all employees in a company

scope: `time_off_requests:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Time Off Requests"
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
      "Embedded-Time-Off-Balance": {
        "type": "object",
        "description": "Time off balance for an employee, grouped by policy.",
        "x-examples": {
          "success_status": {
            "employee_uuid": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
            "balances": [
              {
                "policy_uuid": "c2d9b1bd-3f36-4c2d-a727-b2af057d6a7f",
                "balance_hours": "32.0",
                "accrued_hours": "40.0",
                "used_hours": "8.0",
                "pending_hours": "0.0"
              }
            ]
          }
        },
        "properties": {
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee.",
            "example": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
            "readOnly": true
          },
          "balances": {
            "type": "array",
            "description": "The employee's time off balances, one entry per policy.",
            "readOnly": true,
            "items": {
              "type": "object",
              "properties": {
                "policy_uuid": {
                  "type": "string",
                  "description": "The UUID of the time off policy.",
                  "example": "c2d9b1bd-3f36-4c2d-a727-b2af057d6a7f",
                  "readOnly": true
                },
                "balance_hours": {
                  "type": "string",
                  "description": "The employee's current available balance hours for this policy.",
                  "example": "32.0",
                  "readOnly": true
                },
                "accrued_hours": {
                  "type": "string",
                  "description": "The total hours accrued year-to-date for this policy.",
                  "example": "40.0",
                  "readOnly": true
                },
                "used_hours": {
                  "type": "string",
                  "description": "The total hours used year-to-date for this policy.",
                  "example": "8.0",
                  "readOnly": true
                },
                "pending_hours": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The total hours from pending time off requests for this policy.",
                  "example": "0.0",
                  "readOnly": true
                }
              }
            }
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
    "/v1/companies/{company_uuid}/time_off/balances": {
      "get": {
        "summary": "Get time off balances for a company",
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
            "name": "company_uuid",
            "in": "path",
            "description": "The UUID of the company",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "employee_uuids",
            "in": "query",
            "required": false,
            "description": "Filter by employee UUIDs (comma-separated)",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "policy_uuids",
            "in": "query",
            "required": false,
            "description": "Filter by time off policy UUIDs (comma-separated)",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "page",
            "in": "query",
            "required": false,
            "description": "The page that is requested",
            "schema": {
              "type": "integer"
            }
          },
          {
            "name": "per",
            "in": "query",
            "required": false,
            "description": "Number of objects per page",
            "schema": {
              "type": "integer"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_uuid-time_off-balances",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get time off balances for all employees in a company\n\nscope: `time_off_requests:read`",
        "tags": [
          "Time Off Requests"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Embedded-Time-Off-Balance/x-examples/success_status"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Embedded-Time-Off-Balance"
                  }
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
