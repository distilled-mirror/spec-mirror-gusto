---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all ACH transactions for a company

Fetches all ACH transactions for a company.

scope: `ach_transactions:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "ACH Transactions"
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
      "Ach-Transaction": {
        "type": "object",
        "x-examples": {
          "example": {
            "uuid": "123e4567-e89b-12d3-a456-426655440000",
            "company_uuid": "456e7890-e12b-34c5-d678-901234567890",
            "payment_event_type": "Payroll",
            "payment_event_uuid": "789e0123-e45f-67ab-c890-123456789012",
            "recipient_type": "Employee",
            "recipient_uuid": "012e3456-f78d-90ab-12cd-345678901234",
            "error_code": null,
            "transaction_type": "Credit employee pay",
            "payment_status": "submitted",
            "payment_direction": "credit",
            "payment_event_check_date": "2023-10-02",
            "payment_date": "2023-10-17",
            "amount": "123.00",
            "description": "PAY 380654"
          }
        },
        "description": "Representation of an ACH transaction",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of an ACH transaction"
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company to which the ACH transaction belongs"
          },
          "payment_event_type": {
            "type": "string",
            "description": "The type of payment event associated with the ACH transaction",
            "enum": [
              "Payroll",
              "ContractorPayment"
            ]
          },
          "payment_event_uuid": {
            "type": "string",
            "description": "Unique identifier for the payment event associated with the ACH transaction"
          },
          "recipient_type": {
            "description": "The type of recipient associated with the ACH transaction",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "Employee",
                  "Contractor"
                ]
              },
              {
                "type": "null"
              }
            ]
          },
          "recipient_uuid": {
            "type": "string",
            "description": "Unique identifier for the recipient associated with the ACH transaction"
          },
          "error_code": {
            "type": [
              "string",
              "null"
            ],
            "description": "The error code associated with the ACH transaction, if any. If there is no error on the ACH transaction, this field will be nil. See [this article](https://engineering.gusto.com/how-ach-works-a-developer-perspective-part-2/) for a complete list of ACH return codes."
          },
          "transaction_type": {
            "type": "string",
            "description": "The type of transaction associated with the ACH transaction"
          },
          "payment_status": {
            "type": "string",
            "description": "The status of the ACH transaction",
            "enum": [
              "unsubmitted",
              "submitted",
              "successful",
              "failed"
            ]
          },
          "payment_direction": {
            "type": "string",
            "description": "The direction of the payment",
            "enum": [
              "credit",
              "debit"
            ]
          },
          "payment_event_check_date": {
            "type": "string",
            "description": "The date of the payment event check associated with the ACH transaction"
          },
          "payment_date": {
            "type": "string",
            "description": "The date of the payment associated with the ACH transaction"
          },
          "amount": {
            "type": "string",
            "description": "The amount of money moved by the ACH transaction. This amount is always non-negative."
          },
          "description": {
            "type": "string",
            "description": "The description of the ACH transaction. Can be used to identify the ACH transaction on the recipient's bank statement."
          }
        },
        "required": [
          "uuid"
        ]
      },
      "Ach-Transaction-List": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Ach-Transaction"
        },
        "x-examples": {
          "example": [
            {
              "uuid": "123e4567-e89b-12d3-a456-426655440000",
              "company_uuid": "456e7890-e12b-34c5-d678-901234567890",
              "payment_event_type": "Payroll",
              "payment_event_uuid": "789e0123-e45f-67ab-c890-123456789012",
              "recipient_type": "Employee",
              "recipient_uuid": "012e3456-f78d-90ab-12cd-345678901234",
              "error_code": null,
              "transaction_type": "Credit employee pay",
              "payment_status": "submitted",
              "payment_direction": "credit",
              "payment_event_check_date": "2023-10-02",
              "payment_date": "2023-10-17",
              "amount": "123.00",
              "description": "PAY 380654"
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
    "/v1/companies/{company_uuid}/ach_transactions": {
      "get": {
        "summary": "Get all ACH transactions for a company",
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
            "required": true,
            "description": "The UUID of the company",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "contractor_payment_uuid",
            "in": "query",
            "required": false,
            "description": "The UUID of the contractor payment",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "payroll_uuid",
            "in": "query",
            "required": false,
            "description": "The UUID of the payroll",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "transaction_type",
            "in": "query",
            "required": false,
            "description": "Used to filter the ACH transactions to only include those with a specific transaction type, such as \"Credit employee pay\".",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "payment_direction",
            "in": "query",
            "required": false,
            "description": "Used to filter the ACH transactions to only include those with a specific payment direction, either \"credit\" or \"debit\".",
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
        "operationId": "get-ach-transactions",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetches all ACH transactions for a company.\n\nscope: `ach_transactions:read`",
        "tags": [
          "ACH Transactions"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Example response",
            "content": {
              "application/json": {
                "examples": {
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Ach-Transaction-List/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Ach-Transaction-List"
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
