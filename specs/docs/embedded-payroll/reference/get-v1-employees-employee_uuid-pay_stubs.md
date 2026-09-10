---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee's pay stubs

Get an employee's pay stubs.

Results are returned in reverse chronological order (newest first).

scope: `pay_stubs:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Payrolls"
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
      "Employee-Pay-Stubs-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "uuid": "d2cec746-caee-464a-bcaf-00d93f7049c9",
              "check_date": "2023-11-24",
              "gross_pay": "880.0",
              "net_pay": "541.02",
              "payroll_uuid": "a039cafb-745e-4af4-bf1e-935a86fc18e0",
              "check_amount": "500.2",
              "payment_method": "Direct Deposit"
            }
          ]
        },
        "items": {
          "description": "The representation of an employee pay stub information.",
          "type": "object",
          "properties": {
            "uuid": {
              "type": "string",
              "description": "The UUID of the employee pay stub.",
              "readOnly": true
            },
            "check_date": {
              "type": "string",
              "description": "The check date of the pay stub.",
              "readOnly": true
            },
            "gross_pay": {
              "type": "string",
              "description": "The gross pay amount for the pay stub.",
              "readOnly": true
            },
            "net_pay": {
              "type": "string",
              "description": "The net pay amount for the pay stub.",
              "readOnly": true
            },
            "payroll_uuid": {
              "type": "string",
              "description": "A unique identifier of the payroll to which the pay stub belongs.",
              "readOnly": true
            },
            "check_amount": {
              "type": "string",
              "description": "The check amount for the pay stub.",
              "readOnly": true
            },
            "payment_method": {
              "type": "string",
              "description": "The payment method for the pay stub.",
              "enum": [
                "Direct Deposit",
                "Check"
              ],
              "readOnly": true
            }
          },
          "x-tags": [
            "Payrolls"
          ],
          "required": [
            "uuid"
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
    "/v1/employees/{employee_id}/pay_stubs": {
      "get": {
        "summary": "Get an employee's pay stubs",
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
        "operationId": "get-v1-employees-employee_uuid-pay_stubs",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get an employee's pay stubs.\n\nResults are returned in reverse chronological order (newest first).\n\nscope: `pay_stubs:read`",
        "x-gusto-integration-type": [
          "embedded"
        ],
        "tags": [
          "Payrolls"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Pay-Stubs-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Pay-Stubs-List"
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
