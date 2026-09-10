---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get payment method for an employee

Returns the payment method for an employee (e.g. Check or Direct Deposit with split configuration).

scope: `employee_payment_methods:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employee Payment Method"
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
      "Payment-Method-Bank-Account": {
        "type": "object",
        "description": "Representation of a bank account item",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The bank account ID"
          },
          "name": {
            "type": "string",
            "description": "The bank account name"
          },
          "hidden_account_number": {
            "type": "string",
            "description": "Masked bank account number"
          },
          "priority": {
            "type": "integer",
            "description": "The order of priority for each payment split, with priority 1 being the first bank account paid. Priority must be unique and sequential."
          },
          "split_amount": {
            "description": "If `split_by` is 'Amount', this is in cents (e.g., 500 for $5.00) and exactly one account must have a `split_amount` of `null` to capture the remainder. If `split_by` is 'Percentage', this is the percentage value (e.g., 60 for 60%).",
            "type": [
              "integer",
              "null"
            ]
          }
        },
        "required": [
          "uuid"
        ]
      },
      "Employee-Payment-Method": {
        "title": "Employee-Payment-Method",
        "type": "object",
        "x-examples": {
          "direct_deposit_percentage": {
            "version": "63859768485e218ccf8a449bb60f14ed",
            "type": "Direct Deposit",
            "split_by": "Percentage",
            "splits": [
              {
                "uuid": "4b35bebe-3445-4014-a748-1e264647d601",
                "name": "Cayman Island Checking",
                "hidden_account_number": "XXXX1234",
                "priority": 1,
                "split_amount": 100
              }
            ]
          },
          "Example-1": {
            "value": {
              "version": "63859768485e218ccf8a449bb60f14ed",
              "type": "Direct Deposit",
              "split_by": "Amount",
              "splits": [
                {
                  "uuid": "e88f9436-b74e-49a8-87e9-777b9bfe715e",
                  "name": "BoA Checking Account",
                  "priority": 1,
                  "split_amount": 50000
                },
                {
                  "uuid": "0d2b7f73-05d6-4184-911d-269edeecc30a",
                  "name": "Chase Checking Account",
                  "priority": 2,
                  "split_amount": 100000
                },
                {
                  "uuid": "1531e824-8d9e-4bd8-9f90-0d04608125d7",
                  "name": "US Bank Checking Account",
                  "priority": 3,
                  "split_amount": null
                }
              ]
            }
          },
          "Example-2": {
            "value": {
              "version": "63859768485e218ccf8a449bb60f14ed",
              "type": "Direct Deposit",
              "split_by": "Percentage",
              "splits": [
                {
                  "uuid": "e88f9436-b74e-49a8-87e9-777b9bfe715e",
                  "name": "BoA Checking Account",
                  "priority": 1,
                  "split_amount": 60
                },
                {
                  "uuid": "0d2b7f73-05d6-4184-911d-269edeecc30a",
                  "name": "Chase Checking Account",
                  "priority": 2,
                  "split_amount": 40
                }
              ]
            }
          },
          "Example-3": {
            "value": {
              "version": "63859768485e218ccf8a449bb60f14ed",
              "type": "Check"
            }
          }
        },
        "description": "",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "type": {
            "type": "string",
            "enum": [
              "Direct Deposit",
              "Check"
            ],
            "description": "The payment method type. If type is Check, then `split_by` and `splits` do not need to be populated. If type is Direct Deposit, `split_by` and `splits` are required."
          },
          "split_by": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "Amount",
                  "Percentage"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "Describes how the payment will be split. If `split_by` is Percentage, then the split amounts must add up to exactly 100. If `split_by` is Amount, then the last split `amount` must be `null` to capture the remainder."
          },
          "splits": {
            "type": [
              "array",
              "null"
            ],
            "items": {
              "$ref": "#/components/schemas/Payment-Method-Bank-Account"
            }
          }
        },
        "x-tags": [
          "Employee Payment Method"
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
    "/v1/employees/{employee_id}/payment_method": {
      "get": {
        "summary": "Get payment method for an employee",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employees-employee_id-payment_method",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns the payment method for an employee (e.g. Check or Direct Deposit with split configuration).\n\nscope: `employee_payment_methods:read`",
        "tags": [
          "Employee Payment Method"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Successful",
            "content": {
              "application/json": {
                "examples": {
                  "direct_deposit_percentage": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Payment-Method/x-examples/direct_deposit_percentage"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Payment-Method"
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
