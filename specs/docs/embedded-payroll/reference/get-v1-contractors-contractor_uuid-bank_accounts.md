---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all contractor bank accounts

Returns all contractor bank accounts.

scope: `contractor_payment_methods:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractor Payment Method"
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
      "Contractor-Bank-Account": {
        "title": "Contractor-Bank-Account",
        "type": "object",
        "x-examples": {
          "example": {
            "uuid": "1531e824-8d9e-4bd8-9f90-0d04608125d7",
            "contractor_uuid": "9fcf1b1d-8886-4691-9283-383d3bdd4fd9",
            "name": "BoA Checking Account",
            "routing_number": "266905059",
            "hidden_account_number": "XXXX1207",
            "account_type": "Checking"
          }
        },
        "x-tags": [
          "Contractor Payment Method"
        ],
        "properties": {
          "uuid": {
            "type": "string",
            "description": "UUID of the bank account"
          },
          "contractor_uuid": {
            "type": "string",
            "description": "UUID of the contractor"
          },
          "account_type": {
            "type": "string",
            "enum": [
              "Checking",
              "Savings"
            ],
            "description": "Bank account type"
          },
          "name": {
            "type": "string",
            "description": "Name for the bank account"
          },
          "routing_number": {
            "type": "string",
            "description": "The bank account's routing number"
          },
          "hidden_account_number": {
            "type": "string",
            "description": "Masked bank account number"
          }
        },
        "required": [
          "uuid",
          "contractor_uuid",
          "name",
          "routing_number",
          "hidden_account_number",
          "account_type"
        ]
      },
      "Contractor-Bank-Account-List": {
        "title": "Contractor-Bank-Account-List",
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Contractor-Bank-Account"
        },
        "x-examples": {
          "example": [
            {
              "uuid": "1531e824-8d9e-4bd8-9f90-0d04608125d7",
              "contractor_uuid": "9fcf1b1d-8886-4691-9283-383d3bdd4fd9",
              "name": "BoA Checking Account",
              "routing_number": "266905059",
              "hidden_account_number": "XXXX1207",
              "account_type": "Checking"
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
    "/v1/contractors/{contractor_uuid}/bank_accounts": {
      "get": {
        "summary": "Get all contractor bank accounts",
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
            "name": "contractor_uuid",
            "in": "path",
            "description": "The UUID of the contractor",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-contractors-contractor_uuid-bank_accounts",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns all contractor bank accounts.\n\nscope: `contractor_payment_methods:read`",
        "tags": [
          "Contractor Payment Method"
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
                      "$ref": "#/components/schemas/Contractor-Bank-Account-List/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Contractor-Bank-Account-List"
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
