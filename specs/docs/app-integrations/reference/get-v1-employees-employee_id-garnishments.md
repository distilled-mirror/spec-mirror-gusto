---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get garnishments for an employee

Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.

scope: `garnishments:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Garnishments"
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
      "Garnishment": {
        "description": "Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the garnishment in Gusto.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee to which this garnishment belongs.",
            "readOnly": true
          },
          "active": {
            "type": "boolean",
            "default": true,
            "description": "Whether or not this garnishment is currently active."
          },
          "amount": {
            "type": "string",
            "format": "float",
            "readOnly": false,
            "description": "The amount of the garnishment. Either a percentage or a fixed dollar amount. Represented as a float, e.g. \"8.00\"."
          },
          "description": {
            "type": "string",
            "readOnly": false,
            "description": "The description of the garnishment."
          },
          "court_ordered": {
            "type": "boolean",
            "readOnly": false,
            "description": "Whether the garnishment is court ordered."
          },
          "times": {
            "type": [
              "integer",
              "null"
            ],
            "readOnly": false,
            "default": null,
            "description": "The number of times to apply the garnishment. Ignored if recurring is true."
          },
          "recurring": {
            "type": "boolean",
            "readOnly": false,
            "default": false,
            "description": "Whether the garnishment should recur indefinitely."
          },
          "annual_maximum": {
            "format": "float",
            "readOnly": false,
            "default": null,
            "description": "The maximum deduction per annum. A null value indicates no maximum. Represented as a float, e.g. \"200.00\".",
            "type": [
              "string",
              "null"
            ]
          },
          "total_amount": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "readOnly": false,
            "default": null,
            "description": "A maximum total deduction for the lifetime of this garnishment. A null value indicates no maximum."
          },
          "pay_period_maximum": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "default": null,
            "description": "The maximum deduction per pay period. A null value indicates no maximum. Represented as a float, e.g. \"16.00\"."
          },
          "deduct_as_percentage": {
            "type": "boolean",
            "readOnly": false,
            "default": false,
            "description": "Whether the amount should be treated as a percentage to be deducted per pay period."
          },
          "garnishment_type": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "child_support",
                  "federal_tax_lien",
                  "state_tax_lien",
                  "student_loan",
                  "creditor_garnishment",
                  "federal_loan",
                  "other_garnishment"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The specific type of garnishment for court ordered garnishments."
          },
          "child_support": {
            "$ref": "#/components/schemas/Garnishment-Child-Support"
          }
        },
        "required": [
          "uuid"
        ],
        "x-examples": {
          "Example": {
            "uuid": "4c7841a2-1363-497e-bc0f-664703c7484f",
            "version": "52b7c567242cb7452e89ba2bc02cb476",
            "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
            "active": true,
            "amount": "8.00",
            "description": "Company loan to employee",
            "court_ordered": false,
            "times": 5,
            "recurring": false,
            "annual_maximum": null,
            "total_amount": null,
            "pay_period_maximum": "100.00",
            "deduct_as_percentage": true,
            "garnishment_type": null,
            "child_support": null
          },
          "Create-Example": {
            "uuid": "4c7841a2-1363-497e-bc0f-664703c7484f",
            "version": "52b7c567242cb7452e89ba2bc02cb476",
            "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
            "active": true,
            "amount": "150.00",
            "description": "Back taxes",
            "court_ordered": true,
            "times": null,
            "recurring": true,
            "annual_maximum": null,
            "total_amount": null,
            "pay_period_maximum": null,
            "deduct_as_percentage": false,
            "garnishment_type": null,
            "child_support": null
          },
          "Child-Support-Example": {
            "uuid": "4c7841a2-1363-497e-bc0f-664703c7481a",
            "version": "52b7c567242cb7452e89ba2bc02cb383",
            "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
            "active": true,
            "amount": "40.00",
            "description": "Child support - AZ28319",
            "court_ordered": true,
            "times": null,
            "recurring": true,
            "annual_maximum": null,
            "total_amount": null,
            "pay_period_maximum": "400.00",
            "deduct_as_percentage": true,
            "garnishment_type": "child_support",
            "child_support": {
              "state": "AZ",
              "payment_period": "Monthly",
              "case_number": "AZ28319",
              "order_number": null,
              "remittance_number": null,
              "fips_code": "04000"
            }
          },
          "Garnishment-List": [
            {
              "uuid": "4c7841a2-1363-497e-bc0f-664703c7484f",
              "version": "52b7c567242cb7452e89ba2bc02cb476",
              "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
              "active": true,
              "amount": "8.00",
              "description": "Company loan to employee",
              "court_ordered": false,
              "times": 5,
              "recurring": false,
              "annual_maximum": null,
              "total_amount": null,
              "pay_period_maximum": "100.00",
              "deduct_as_percentage": true,
              "garnishment_type": null,
              "child_support": null
            },
            {
              "uuid": "4c7841a2-1363-497e-bc0f-664703c7481a",
              "version": "52b7c567242cb7452e89ba2bc02cb383",
              "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
              "active": true,
              "amount": "40.00",
              "description": "Child support - AZ28319",
              "court_ordered": true,
              "times": null,
              "recurring": true,
              "annual_maximum": null,
              "total_amount": null,
              "pay_period_maximum": "400.00",
              "deduct_as_percentage": true,
              "garnishment_type": "child_support",
              "child_support": {
                "state": "AZ",
                "payment_period": "Monthly",
                "case_number": "AZ28319",
                "order_number": null,
                "remittance_number": null,
                "fips_code": "04000"
              }
            }
          ]
        }
      },
      "Garnishment-Child-Support": {
        "description": "Additional child support order details",
        "type": [
          "object",
          "null"
        ],
        "properties": {
          "state": {
            "type": "string",
            "readOnly": false,
            "description": "The two letter state abbreviation for the state issuing the child support order. Agency data is available in the `GET /v1/garnishments/child_support` API."
          },
          "payment_period": {
            "type": "string",
            "readOnly": false,
            "enum": [
              "Every week",
              "Every other week",
              "Twice per month",
              "Monthly"
            ],
            "description": "How often the agency collects the withholding amount. e.g. $500 monthly -> `Monthly`."
          },
          "fips_code": {
            "type": "string",
            "description": "The FIPS code associated with the state or county agency issuing the child support order. Agency data is available in the `GET /v1/garnishments/child_support` API.",
            "nullable": false,
            "readOnly": false
          },
          "case_number": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false,
            "description": "Child Support Enforcement Case Number associated with this child support obligation - required for most states. Agency specific requirements are available in the `GET /v1/garnishments/child_support` API."
          },
          "order_number": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false,
            "description": "Order Identifier or Order ID associated with this child support obligation - required for some states. Agency specific requirements are available in the `GET /v1/garnishments/child_support` API."
          },
          "remittance_number": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false,
            "description": "Child Support Enforcement Remittance ID associated with this child support obligation - required for some states. Agency specific requirements are available in the `GET /v1/garnishments/child_support` API."
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
    "/v1/employees/{employee_id}/garnishments": {
      "get": {
        "summary": "Get garnishments for an employee",
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
            "description": "The UUID of the employee",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "page",
            "in": "query",
            "required": false,
            "description": "The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.",
            "schema": {
              "type": "integer"
            }
          },
          {
            "name": "per",
            "in": "query",
            "required": false,
            "description": "Number of objects per page. For majority of endpoints will default to 25",
            "schema": {
              "type": "integer"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employees-employee_id-garnishments",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.\n\nscope: `garnishments:read`",
        "tags": [
          "Garnishments"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Example response",
            "content": {
              "application/json": {
                "examples": {
                  "Garnishment-List": {
                    "value": {
                      "$ref": "#/components/schemas/Garnishment/x-examples/Garnishment-List"
                    }
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Garnishment"
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
