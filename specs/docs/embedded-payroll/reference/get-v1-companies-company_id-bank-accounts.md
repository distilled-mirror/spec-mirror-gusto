---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all company bank accounts

Returns company bank accounts. Currently, we only support a single default bank account per company.

scope: `company_bank_accounts:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Bank Accounts"
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
      "Company-Bank-Account": {
        "description": "The company bank account",
        "type": "object",
        "x-examples": {
          "success_status": {
            "uuid": "1263eae5-4411-48d9-bd6d-18ed93082e65",
            "company_uuid": "e2c4c0ce-2986-48b9-86cf-ec27f6ed9a36",
            "account_type": "Checking",
            "routing_number": "851070439",
            "hidden_account_number": "XXXX4087",
            "verification_status": "verified",
            "verification_type": "bank_deposits",
            "name": "Employer Funding Account",
            "reverse_wire_enabled": false
          },
          "plaid_external_status": {
            "uuid": "1263eae5-4411-48d9-bd6d-18ed93082e65",
            "company_uuid": "e2c4c0ce-2986-48b9-86cf-ec27f6ed9a36",
            "account_type": "Checking",
            "routing_number": "851070439",
            "hidden_account_number": "XXXX4087",
            "verification_status": "verified",
            "verification_type": "plaid_external",
            "name": "Employer Funding Account",
            "reverse_wire_enabled": true
          }
        },
        "x-tags": [
          "Company Bank Accounts"
        ],
        "properties": {
          "uuid": {
            "type": "string",
            "description": "UUID of the bank account"
          },
          "company_uuid": {
            "type": "string",
            "description": "UUID of the company"
          },
          "account_type": {
            "type": "string",
            "description": "Bank account type",
            "enum": [
              "Checking",
              "Savings"
            ]
          },
          "routing_number": {
            "type": "string",
            "description": "The bank account's routing number"
          },
          "hidden_account_number": {
            "type": "string",
            "description": "Masked bank account number"
          },
          "verification_status": {
            "type": "string",
            "enum": [
              "awaiting_deposits",
              "ready_for_verification",
              "verified"
            ],
            "description": "The verification status of the bank account.\n\n'awaiting_deposits' means the bank account is just created and money is being transferred.\n'ready_for_verification' means the micro-deposits are completed and the verification process can begin by using the verify endpoint.\n'verified' means the bank account is verified."
          },
          "verification_type": {
            "type": "string",
            "enum": [
              "bank_deposits",
              "plaid",
              "plaid_external"
            ],
            "description": "The verification type of the bank account.\n\n'bank_deposits' means the bank account is connected by entering routing and accounting numbers and verifying through micro-deposits.\n'plaid' means the bank account is connected through Plaid."
          },
          "plaid_status": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "connected",
                  "disconnected"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The Plaid connection status of the bank account. Only applies when verification type is Plaid."
          },
          "last_cached_balance": {
            "type": [
              "string",
              "null"
            ],
            "description": "The last fetch balance for the bank account. Please be aware that this amount does not reflect the most up-to-date balance and only applies when the verification type is Plaid."
          },
          "balance_fetched_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "The balance fetch date associated with the last_cached_balance. Only applies when verification type is Plaid."
          },
          "name": {
            "type": "string",
            "description": "Name of bank account"
          },
          "reverse_wire_enabled": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether the company has at least one bank account with active reverse-wire\nfunding. The same value is returned on every bank-account row in this\nresponse."
          }
        },
        "required": [
          "uuid"
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
    "/v1/companies/{company_id}/bank_accounts": {
      "get": {
        "summary": "Get all company bank accounts",
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
        "operationId": "get-v1-companies-company_id-bank-accounts",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns company bank accounts. Currently, we only support a single default bank account per company.\n\nscope: `company_bank_accounts:read`",
        "tags": [
          "Bank Accounts"
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
                        "$ref": "#/components/schemas/Company-Bank-Account/x-examples/success_status"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Company-Bank-Account"
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
