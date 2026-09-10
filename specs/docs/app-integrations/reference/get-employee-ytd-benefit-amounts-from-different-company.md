---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get year-to-date benefit amounts from a different company

Retrieves year-to-date benefit amounts that were contributed at a different company for the specified employee.
Returns benefit amounts for the requested tax year (defaults to current year if not specified).

This endpoint only supports retrieving outside contributions for 401(k) benefits.

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
      "Ytd-Benefit-Amounts-From-Different-Company": {
        "type": "object",
        "description": "Ytd Benefit Amounts From Different Company",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The unique identifier for this benefit amount record."
          },
          "benefit_type": {
            "type": "integer",
            "description": "The benefit type supported by Gusto. See [Benefit Types](https://docs.gusto.com/embedded-payroll/reference/get-v1-benefits) for more information."
          },
          "ytd_employee_deduction_amount": {
            "type": "string",
            "description": "The year-to-date employee deduction made outside the current company."
          },
          "ytd_company_contribution_amount": {
            "type": "string",
            "description": "The year-to-date company contribution made outside the current company."
          }
        },
        "required": [
          "uuid",
          "benefit_type",
          "ytd_employee_deduction_amount",
          "ytd_company_contribution_amount"
        ],
        "x-examples": {
          "Ytd-Benefit-Amounts-List": [
            {
              "uuid": "c5fdae57-5483-4529-9aae-f0edceed92d3",
              "benefit_type": 1,
              "ytd_employee_deduction_amount": "5000.00",
              "ytd_company_contribution_amount": "2500.00"
            },
            {
              "uuid": "1bfdb946-b2be-4909-ac46-9e7f73872d0a",
              "benefit_type": 5,
              "ytd_employee_deduction_amount": "2132.00",
              "ytd_company_contribution_amount": "3345.00"
            }
          ]
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
    "/v1/employees/{employee_id}/ytd_benefit_amounts_from_different_company": {
      "get": {
        "summary": "Get year-to-date benefit amounts from a different company",
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
            "name": "employee_id",
            "in": "path",
            "required": true,
            "description": "The UUID of the employee",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "tax_year",
            "in": "query",
            "required": false,
            "schema": {
              "type": "integer",
              "minimum": 2000,
              "maximum": 2999,
              "example": 2024
            },
            "description": "The tax year for which to retrieve YTD benefit amounts. Defaults to current year if not specified."
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-employee-ytd-benefit-amounts-from-different-company",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieves year-to-date benefit amounts that were contributed at a different company for the specified employee.\nReturns benefit amounts for the requested tax year (defaults to current year if not specified).\n\nThis endpoint only supports retrieving outside contributions for 401(k) benefits.\n\nscope: `employee_benefits:read`",
        "tags": [
          "Employee Benefits"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "examples": {
                  "Ytd-Benefit-Amounts-List": {
                    "value": {
                      "$ref": "#/components/schemas/Ytd-Benefit-Amounts-From-Different-Company/x-examples/Ytd-Benefit-Amounts-List"
                    }
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Ytd-Benefit-Amounts-From-Different-Company"
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
