---
updatedAt: 2026-07-31T20:26:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all reverse wire transactions for a company

Returns a paginated list of reverse wire (drawdown) transactions for a company. Reverse wires are debit transactions initiated by Gusto to pull funds from a partner's bank account to cover payroll or contractor payment obligations. Pagination is returned via the `x-page`, `x-per-page`, `x-total-count`, and `x-total-pages` response headers.

scope: `reverse_wire_transactions:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Reverse Wire Transactions"
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
      "Reverse-Wire-Transaction": {
        "type": "object",
        "description": "Representation of a reverse wire (drawdown) transaction. Reverse wires are debit transactions initiated by Gusto to pull funds from a partner's bank account to cover payroll or contractor payment obligations.",
        "x-examples": {
          "example": {
            "company_uuid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "amount": "107250.85",
            "status": "processed",
            "payment_direction": "debit",
            "bank_name": "Chase Payroll Incoming Wires",
            "payment_event_type": "Payroll",
            "payment_event_uuid": "f9e8d7c6-b5a4-3210-fedc-ba9876543210",
            "payment_event_check_date": "2024-01-15",
            "created_at": "2024-01-12"
          }
        },
        "properties": {
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company the reverse wire transaction belongs to"
          },
          "amount": {
            "type": "string",
            "format": "float",
            "description": "The amount of money moved by the reverse wire, as a decimal string. Always non-negative."
          },
          "status": {
            "type": "string",
            "description": "Current status of the reverse wire transaction.\n- `pending_processing`: The reverse wire has been initiated and is awaiting processing by the banking network.\n- `processed`: The reverse wire was successfully settled and funds have been received.\n- `rejected`: The reverse wire was rejected by the receiving bank (e.g. invalid account, insufficient funds).\n- `failed`: The reverse wire failed during processing due to a system or network error.\n",
            "enum": [
              "pending_processing",
              "processed",
              "rejected",
              "failed"
            ]
          },
          "payment_direction": {
            "type": "string",
            "description": "The direction of the payment. Reverse wires are always debits from the company's account.",
            "enum": [
              "debit"
            ]
          },
          "bank_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "Name of the receiving bank. Null when the bank is not known."
          },
          "payment_event_type": {
            "description": "The type of payment event this reverse wire is associated with. Null when the wire is not linked to a payroll or contractor payment.",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "Payroll",
                  "ContractorPayment"
                ]
              },
              {
                "type": "null"
              }
            ]
          },
          "payment_event_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "Unique identifier of the associated payroll or contractor payment. Null when the wire is not linked to a payment event."
          },
          "payment_event_check_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "The check date of the associated payment event. Null when the wire is not linked to a payment event."
          },
          "created_at": {
            "type": "string",
            "description": "The date the reverse wire record was created."
          }
        },
        "required": [
          "company_uuid",
          "amount",
          "status",
          "payment_direction",
          "created_at"
        ]
      },
      "Reverse-Wire-Transaction-List": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Reverse-Wire-Transaction"
        },
        "x-examples": {
          "example": [
            {
              "company_uuid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
              "amount": "107250.85",
              "status": "processed",
              "payment_direction": "debit",
              "bank_name": "Chase Payroll Incoming Wires",
              "payment_event_type": "Payroll",
              "payment_event_uuid": "f9e8d7c6-b5a4-3210-fedc-ba9876543210",
              "payment_event_check_date": "2024-01-15",
              "created_at": "2024-01-12"
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
    "/v1/companies/{company_uuid}/reverse_wire_transactions": {
      "get": {
        "summary": "Get all reverse wire transactions for a company",
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
            "name": "payroll_uuid",
            "in": "query",
            "required": false,
            "description": "Filter results to reverse wires associated with a specific payroll",
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
        "operationId": "get-reverse-wire-transactions",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a paginated list of reverse wire (drawdown) transactions for a company. Reverse wires are debit transactions initiated by Gusto to pull funds from a partner's bank account to cover payroll or contractor payment obligations. Pagination is returned via the `x-page`, `x-per-page`, `x-total-count`, and `x-total-pages` response headers.\n\nscope: `reverse_wire_transactions:read`",
        "tags": [
          "Reverse Wire Transactions"
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
                      "$ref": "#/components/schemas/Reverse-Wire-Transaction-List/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Reverse-Wire-Transaction-List"
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
