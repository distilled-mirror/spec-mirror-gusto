---
updatedAt: 2026-05-26T23:09:16.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# List contractor payment details

Get payment details for contractors in a company. This endpoint returns a list of all contractors
associated with the specified company, including their payment methods and bank account details
if they are paid via direct deposit.

For contractors paid by direct deposit, the response includes their bank account information
with sensitive data masked for security. The payment details also include information about
how their payments are split if they have multiple bank accounts configured.

For contractors paid by check, only the basic payment method information is returned.

### Response Details
- For direct deposit contractors:
  - Bank account details (masked)
  - Payment splits configuration
  - Routing numbers
  - Account types
- For check payments:
  - Basic payment method designation

### Common Use Cases
- Fetching contractor payment information for payroll processing
- Verifying contractor payment methods
- Reviewing payment split configurations

`encrypted_account_number` is available only with the additional scope `contractor_payment_methods:read:account_numbers`.

scope: `contractor_payment_methods:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractors"
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
      "Contractor-Payment-Details-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "contractor_uuid": "e3d9487a-4ecb-49a3-b6ff-cf03ba7278b6",
              "first_name": "Yael",
              "last_name": "Kuvalis",
              "payment_method": "Check",
              "split_by": null,
              "splits": null
            },
            {
              "contractor_uuid": "577b6307-66e9-4926-a769-91f5c8b578aa",
              "first_name": "Autumn",
              "last_name": "Connelly",
              "payment_method": "Direct Deposit",
              "split_by": "Percentage",
              "splits": [
                {
                  "bank_account_uuid": "0aca4500-8ba4-48fc-adce-677fe7926b7b",
                  "name": "Cayman Island Checking",
                  "hidden_account_number": "XXXX1545",
                  "account_number": null,
                  "encrypted_account_number": null,
                  "routing_number": "055003201",
                  "priority": 1,
                  "split_amount": 100,
                  "account_type": "Checking"
                }
              ]
            }
          ]
        },
        "items": {
          "type": "object",
          "properties": {
            "contractor_uuid": {
              "type": "string"
            },
            "payment_method": {
              "type": "string",
              "enum": [
                "Direct Deposit",
                "Check"
              ]
            },
            "first_name": {
              "type": "string"
            },
            "last_name": {
              "type": "string"
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
              "description": "Describes how the payment will be split. If split_by is Percentage, then the split amounts must add up to exactly 100. If split_by is Amount, then the amount represents cents and the last split amount must be `null` to capture the remainder."
            },
            "splits": {
              "type": [
                "array",
                "null"
              ],
              "items": {
                "type": "object",
                "properties": {
                  "bank_account_uuid": {
                    "type": "string"
                  },
                  "name": {
                    "type": "string"
                  },
                  "hidden_account_number": {
                    "type": "string",
                    "description": "An obfuscated version of the account number which can be used for display purposes."
                  },
                  "encrypted_account_number": {
                    "type": [
                      "string",
                      "null"
                    ],
                    "description": "Ciphertext containing the full bank account number, which must be decrypted using a key provided by Gusto. Only visible with the `contractor_payment_methods:read:account_number` scope."
                  },
                  "routing_number": {
                    "type": "string"
                  },
                  "priority": {
                    "type": "integer",
                    "description": "The order of priority for each payment split, with priority 1 being the first bank account paid. Priority must be unique and sequential."
                  },
                  "split_amount": {
                    "type": [
                      "number",
                      "null"
                    ],
                    "description": "If `split_by` is 'Amount', this is in cents (e.g., 500 for $5.00) and exactly one account must have a `split_amount` of `null` to capture the remainder. If `split_by` is 'Percentage', this is the percentage value (e.g., 60 for 60%)."
                  },
                  "account_type": {
                    "type": "string"
                  }
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
    "/v1/companies/{company_id}/contractors/payment_details": {
      "get": {
        "summary": "List contractor payment details",
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
            "description": "The UUID of the company. This identifies the company whose contractor payment details you want to retrieve.",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "contractor_uuid",
            "in": "query",
            "required": false,
            "description": "Optional filter to get payment details for a specific contractor. When provided, the response will only include payment details for this contractor.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "contractor_payment_group_uuid",
            "in": "query",
            "required": false,
            "description": "Optional filter to get payment details for contractors in a specific payment group. When provided, the response will only include payment details for contractors in this group.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-contractors-payment_details",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get payment details for contractors in a company. This endpoint returns a list of all contractors\nassociated with the specified company, including their payment methods and bank account details\nif they are paid via direct deposit.\n\nFor contractors paid by direct deposit, the response includes their bank account information\nwith sensitive data masked for security. The payment details also include information about\nhow their payments are split if they have multiple bank accounts configured.\n\nFor contractors paid by check, only the basic payment method information is returned.\n\n### Response Details\n- For direct deposit contractors:\n  - Bank account details (masked)\n  - Payment splits configuration\n  - Routing numbers\n  - Account types\n- For check payments:\n  - Basic payment method designation\n\n### Common Use Cases\n- Fetching contractor payment information for payroll processing\n- Verifying contractor payment methods\n- Reviewing payment split configurations\n\n`encrypted_account_number` is available only with the additional scope `contractor_payment_methods:read:account_numbers`.\n\nscope: `contractor_payment_methods:read`",
        "tags": [
          "Contractors"
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
                    "value": {
                      "$ref": "#/components/schemas/Contractor-Payment-Details-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Contractor-Payment-Details-List"
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
