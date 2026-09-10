---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all recovery cases for a company

Fetch all recovery cases for a company.

scope: `recovery_cases:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Recovery Cases"
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
      "Recovery-Case": {
        "type": "object",
        "x-examples": {
          "example": {
            "uuid": "e83d273e-4ae9-4b61-9c71-4030c2f73093",
            "company_uuid": "c5e3e3e9-732f-4762-849e-20b5cec9036f",
            "status": "open",
            "latest_error_code": "R01",
            "original_debit_date": "2023-10-11",
            "check_date": "2023-10-13",
            "payroll_uuid": "210f2034-fb4a-4059-b109-6c3b5efe499d",
            "contractor_payment_uuids": null,
            "amount_outstanding": 10499.43,
            "event_total_amount": 5912.07
          },
          "recovery_case_index_item": {
            "uuid": "e83d273e-4ae9-4b61-9c71-4030c2f73093",
            "company_uuid": "c5e3e3e9-732f-4762-849e-20b5cec9036f",
            "status": "open",
            "latest_error_code": "R01",
            "original_debit_date": "2023-10-11",
            "check_date": "2023-10-13",
            "payroll_uuid": "210f2034-fb4a-4059-b109-6c3b5efe499d",
            "contractor_payment_uuids": null,
            "amount_outstanding": "10499.43",
            "event_total_amount": "5912.07"
          }
        },
        "description": "Representation of a recovery case",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of an recovery case"
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company to which the recovery case belongs"
          },
          "status": {
            "type": "string",
            "description": "Status of the recovery case",
            "enum": [
              "open",
              "redebit_initiated",
              "wire_initiated",
              "recovered",
              "lost"
            ]
          },
          "latest_error_code": {
            "type": [
              "string",
              "null"
            ],
            "description": "The latest bank error code for the recovery case. See [this doc](https://docs.gusto.com/embedded-payroll/docs/ach-codes-and-transaction-types) for a list of common ACH return codes."
          },
          "original_debit_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "Date when funds were originally debited from the company's bank account"
          },
          "check_date": {
            "type": "string",
            "description": "Check date for the associated payroll or contractor payments"
          },
          "payroll_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The uuid of the associated payroll for which the recovery case was created. If the recovery case was created for a contractor payment, this field will be null."
          },
          "contractor_payment_uuids": {
            "type": [
              "array",
              "null"
            ],
            "description": "The uuids of the associated contractor payments for which the recovery case was created. If the recovery case was created for a payroll, this field will be null.",
            "items": {
              "type": "string"
            }
          },
          "amount_outstanding": {
            "type": "string",
            "description": "Amount outstanding for the recovery case"
          },
          "event_total_amount": {
            "type": "string",
            "description": "Total amount to be debited from the payroll or contractor payments"
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
    "/v1/companies/{company_uuid}/recovery_cases": {
      "get": {
        "summary": "Get all recovery cases for a company",
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
            "description": "The UUID of the company",
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
        "operationId": "get-recovery-cases",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetch all recovery cases for a company.\n\nscope: `recovery_cases:read`",
        "tags": [
          "Recovery Cases"
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
                  "recovery_case_index_item": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Recovery-Case/x-examples/recovery_case_index_item"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Recovery-Case"
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
