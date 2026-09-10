---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get termination pay periods for a company

When a payroll admin terminates an employee and selects "Dismissal Payroll" as the employee's final payroll, their last pay period will appear on the list.

This endpoint returns the unprocessed pay periods for past and future terminated employees in a given company.

scope: `payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Pay Schedules"
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
      "Unprocessed-Termination-Pay-Period": {
        "description": "The representation of an unprocessed termination pay period.",
        "type": "object",
        "properties": {
          "start_date": {
            "type": "string",
            "description": "The start date of the pay period.",
            "readOnly": true
          },
          "end_date": {
            "type": "string",
            "description": "The end date of the pay period."
          },
          "check_date": {
            "type": "string",
            "description": "The check date of the pay period.",
            "readOnly": true
          },
          "debit_date": {
            "type": "string",
            "description": "The debit date of the pay period."
          },
          "employee_name": {
            "type": "string",
            "description": "The full name of the employee."
          },
          "employee_uuid": {
            "type": "string",
            "description": "A unique identifier of the employee."
          },
          "pay_schedule_uuid": {
            "type": "string",
            "description": "A unique identifier of the pay schedule to which the pay period belongs."
          }
        },
        "x-examples": {
          "typical_unprocessed_termination_pay_period": {
            "start_date": "2023-01-11",
            "end_date": "2023-01-24",
            "check_date": "2023-01-28",
            "debit_date": "2023-01-26",
            "employee_name": "Mary Warner",
            "employee_uuid": "094f6ded-a790-4651-87e6-4a7f15dec7c6",
            "pay_schedule_uuid": "00ebc4a4-ec88-4435-8f45-c505bb63e501"
          }
        },
        "x-tags": [
          "Employee Employments"
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
    "/v1/companies/{company_id}/pay_periods/unprocessed_termination_pay_periods": {
      "get": {
        "summary": "Get termination pay periods for a company",
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
            "name": "company_id",
            "in": "path",
            "description": "The UUID of the company",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-unprocessed_termination_pay_periods",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "When a payroll admin terminates an employee and selects \"Dismissal Payroll\" as the employee's final payroll, their last pay period will appear on the list.\n\nThis endpoint returns the unprocessed pay periods for past and future terminated employees in a given company.\n\nscope: `payrolls:read`",
        "tags": [
          "Pay Schedules"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Successful",
            "content": {
              "application/json": {
                "examples": {
                  "typical_unprocessed_termination_pay_period": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Unprocessed-Termination-Pay-Period/x-examples/typical_unprocessed_termination_pay_period"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Unprocessed-Termination-Pay-Period"
                  }
                }
              }
            }
          },
          "404": {
            "description": "Not Found\n\nThe requested resource does not exist. Make sure the provided UUID is valid.\n",
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
