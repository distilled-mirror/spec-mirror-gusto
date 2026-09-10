---
updatedAt: 2026-04-20T21:24:14.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all Section 603 high earner statuses for an employee

Get all Section 603 high earner statuses for an employee across all years.

Section 603 of the SECURE 2.0 Act applies to employees aged 50 or older whose prior-year FICA wages exceed the IRS threshold.
These employees are classified as high earners, and their catch-up contributions to pre-tax retirement benefits must be designated as post-tax contributions.

scope: `employee_benefits:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employee Benefits"
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
      "Employee-Section603-High-Earner-Status-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
              "effective_year": 2026,
              "is_high_earner": false
            },
            {
              "id": "550e8400-e29b-41d4-a716-446655440000",
              "effective_year": 2027,
              "is_high_earner": true
            }
          ]
        },
        "items": {
          "$ref": "#/components/schemas/Employee-Section603-High-Earner-Status"
        }
      },
      "Employee-Section603-High-Earner-Status": {
        "type": "object",
        "description": "The representation of an employee's Section 603 high earner status for a specific year. Section 603 of the SECURE 2.0 Act requires employees aged 50 or older whose prior-year FICA wages exceed the IRS threshold to have their catch-up contributions to pre-tax retirement benefits designated as post-tax contributions.",
        "x-examples": {
          "success_status": {
            "id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
            "effective_year": 2026,
            "is_high_earner": false
          }
        },
        "properties": {
          "id": {
            "type": "string",
            "description": "The unique identifier of the Section 603 high earner status record",
            "readOnly": true
          },
          "effective_year": {
            "type": "integer",
            "description": "The year for which this high earner status applies",
            "readOnly": true
          },
          "is_high_earner": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether the employee is classified as a high earner for Section 603 purposes. Can be null if the status has not yet been determined.",
            "readOnly": true
          }
        },
        "required": [
          "id",
          "effective_year",
          "is_high_earner"
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
    "/v1/employees/{employee_uuid}/section603_high_earner_statuses": {
      "get": {
        "summary": "Get all Section 603 high earner statuses for an employee",
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
            "name": "employee_uuid",
            "in": "path",
            "description": "The UUID of the employee",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employees-employee_uuid-section603_high_earner_statuses",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get all Section 603 high earner statuses for an employee across all years.\n\nSection 603 of the SECURE 2.0 Act applies to employees aged 50 or older whose prior-year FICA wages exceed the IRS threshold.\nThese employees are classified as high earners, and their catch-up contributions to pre-tax retirement benefits must be designated as post-tax contributions.\n\nscope: `employee_benefits:read`",
        "tags": [
          "Employee Benefits"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful - with records",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Section603-High-Earner-Status-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Section603-High-Earner-Status-List"
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
