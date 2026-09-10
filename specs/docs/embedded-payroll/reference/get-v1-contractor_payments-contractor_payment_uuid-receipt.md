---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a single contractor payment receipt

Returns a contractor payment receipt.

Notes:
* Receipts are only available for direct deposit payments and are only available once those payments have been funded.
* Payroll Receipt requests for payrolls which do not have receipts available (e.g. payment by check) will return a 404 status.
* Hour and dollar amounts are returned as string representations of numeric decimals.
* Dollar amounts are represented to the cent.
* If no data has yet be inserted for a given field, it defaults to “0.00” (for fixed amounts).

scope: `payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractor Payments"
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
      "Contractor-Payment-Receipt": {
        "type": "object",
        "x-examples": {
          "example": {
            "contractor_payment_uuid": "afccb970-357e-4013-81f5-85dafc74f9b6",
            "company_uuid": "c827aa0d-3928-4d5a-ab1f-400641a7d2b8",
            "name_of_sender": "Torp and Sons and Sons",
            "name_of_recipient": "Patricia Hamill",
            "debit_date": "2022-06-02",
            "totals": {
              "company_debit": "748.34"
            },
            "contractor_payments": [
              {
                "contractor_uuid": "f83d0bd8-7e20-43b9-834c-6d514ef6cb47",
                "contractor_first_name": "Patricia",
                "contractor_last_name": "Hamill",
                "contractor_business_name": "",
                "contractor_type": "Individual",
                "payment_method": "Direct Deposit",
                "wage": "448.34",
                "bonus": "248.00",
                "reimbursement": "100.00"
              }
            ],
            "licensee": {
              "name": "Gusto, Zenpayroll Inc.",
              "address": "525 20th St",
              "city": "San Francisco",
              "state": "CA",
              "postal_code": "94107",
              "phone_number": "4157778888"
            },
            "license": "Your payroll provider partners with Gusto Inc. for payments processing. Gusto Inc. is a licensed money transmitter. Learn more on our license page.",
            "license_uri": "https://gusto.com/about/licenses",
            "right_to_refund": "https://gusto.com/about/licenses",
            "liability_of_licensee": "https://gusto.com/about/licenses"
          }
        },
        "properties": {
          "contractor_payment_uuid": {
            "type": "string",
            "description": "A unique identifier of the contractor payment receipt."
          },
          "company_uuid": {
            "type": "string",
            "description": "A unique identifier of the company making the contractor payment."
          },
          "name_of_sender": {
            "type": "string",
            "description": "The name of the company making the contractor payment."
          },
          "name_of_recipient": {
            "type": "string",
            "description": "The individual or company name of the contractor receiving payment."
          },
          "debit_date": {
            "type": "string",
            "description": "The debit date for the contractor payment.",
            "format": "date",
            "example": "2022-05-30"
          },
          "license": {
            "type": "string",
            "description": "Always the fixed string \"Your payroll provider partners with Gusto Inc. for payments processing. Gusto Inc. is a licensed money transmitter. Learn more on our license page.\""
          },
          "license_uri": {
            "type": "string",
            "description": "URL for the license information for the licensed payroll processor. Always the fixed string \"https://gusto.com/about/licenses\""
          },
          "right_to_refund": {
            "type": "string",
            "description": "URL for information related to right to refund. Always the fixed string \"https://gusto.com/about/licenses\""
          },
          "liability_of_licensee": {
            "type": "string",
            "description": "URL for information related to right to liability of licensee. Always the fixed string \"https://gusto.com/about/licenses\""
          },
          "totals": {
            "type": "object",
            "description": "The subtotals for the contractor payment.",
            "properties": {
              "company_debit": {
                "type": "string",
                "description": "The total company debit for the contractor payment."
              }
            }
          },
          "contractor_payments": {
            "type": "array",
            "description": "An array of contractor payments for this contractor payment.",
            "items": {
              "type": "object",
              "properties": {
                "contractor_uuid": {
                  "type": "string",
                  "description": "The UUID of the contractor."
                },
                "contractor_first_name": {
                  "type": "string",
                  "description": "The first name of the contractor. Applies when `contractor_type` is `Individual`."
                },
                "contractor_last_name": {
                  "type": "string",
                  "description": "The last name of the contractor.  Applies when `contractor_type` is `Individual`."
                },
                "contractor_business_name": {
                  "type": "string",
                  "description": "The business name of the contractor. Applies when `contractor_type` is `Business`."
                },
                "contractor_type": {
                  "type": "string",
                  "description": "The type of contractor.\n\n`Individual` `Business`"
                },
                "payment_method": {
                  "type": "string",
                  "description": "The payment method.",
                  "enum": [
                    "Direct Deposit",
                    "Check",
                    "Historical Payment",
                    "Correction Payment"
                  ]
                },
                "wage": {
                  "type": "string",
                  "description": "The fixed wage of the payment, regardless of hours worked."
                },
                "bonus": {
                  "type": "string",
                  "description": "The bonus amount in the payment."
                },
                "reimbursement": {
                  "type": "string",
                  "description": "The reimbursement amount in the payment."
                }
              }
            }
          },
          "licensee": {
            "type": "object",
            "description": "The licensed payroll processor",
            "properties": {
              "name": {
                "type": "string",
                "description": "Always the fixed string \"Gusto, Zenpayroll Inc.\""
              },
              "address": {
                "type": "string",
                "description": "Always the fixed string \"525 20th St\""
              },
              "city": {
                "type": "string",
                "description": "Always the fixed string \"San Francisco\""
              },
              "state": {
                "type": "string",
                "description": "Always the fixed string \"CA\""
              },
              "postal_code": {
                "type": "string",
                "description": "Always the fixed string \"94107\""
              },
              "phone_number": {
                "type": "string",
                "description": "Always the fixed string \"4157778888\""
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
    "/v1/contractor_payments/{contractor_payment_uuid}/receipt": {
      "get": {
        "summary": "Get a single contractor payment receipt",
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
            "name": "contractor_payment_uuid",
            "in": "path",
            "required": true,
            "description": "The UUID of the contractor payment",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-contractor_payments-contractor_payment_uuid-receipt",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a contractor payment receipt.\n\nNotes:\n* Receipts are only available for direct deposit payments and are only available once those payments have been funded.\n* Payroll Receipt requests for payrolls which do not have receipts available (e.g. payment by check) will return a 404 status.\n* Hour and dollar amounts are returned as string representations of numeric decimals.\n* Dollar amounts are represented to the cent.\n* If no data has yet be inserted for a given field, it defaults to “0.00” (for fixed amounts).\n\nscope: `payrolls:read`",
        "tags": [
          "Contractor Payments"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "examples": {
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Contractor-Payment-Receipt/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Contractor-Payment-Receipt"
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
