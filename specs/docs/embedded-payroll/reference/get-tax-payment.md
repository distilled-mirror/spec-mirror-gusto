---
updatedAt: 2026-08-19T18:54:10.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a tax payment for a company

Fetches a single tax payment by UUID, including the payroll tax liabilities that make up the payment.

scope: `tax_payments:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Tax Payments"
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
      "Tax-Payment": {
        "type": "object",
        "description": "Representation of a tax payment made by Gusto to a tax agency on behalf of a company",
        "x-examples": {
          "example": {
            "uuid": "44444444-4444-4444-4444-444444444444",
            "company_uuid": "f0e1d2c3-b4a5-6789-0fed-cba987654321",
            "agency_name": "Internal Revenue Service",
            "jurisdiction": "US",
            "period_start": "2026-01-01",
            "period_end": "2026-03-31",
            "due_date": "2026-04-30",
            "payment_sent_on": "2026-04-12",
            "amount": "1325.00",
            "amount_paid": "1325.00",
            "line_items": [
              {
                "payroll_uuid": "55555555-5555-5555-5555-555555555555",
                "unique_tax_id": "00-000-0000-FIT-000",
                "amount": "1325.00"
              }
            ]
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of the tax payment"
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company to which the tax payment belongs"
          },
          "agency_name": {
            "type": "string",
            "description": "The name of the tax agency this payment is submitted to"
          },
          "jurisdiction": {
            "type": "string",
            "description": "The tax jurisdiction this payment is for. A two-letter state code, or US for federal."
          },
          "period_start": {
            "type": "string",
            "format": "date",
            "description": "The start date of the period this payment covers"
          },
          "period_end": {
            "type": "string",
            "format": "date",
            "description": "The end date of the period this payment covers"
          },
          "due_date": {
            "type": "string",
            "format": "date",
            "description": "The date this payment is due"
          },
          "payment_sent_on": {
            "type": [
              "string",
              "null"
            ],
            "format": "date",
            "description": "The date Gusto submitted this payment to the tax agency. It is null until submitted, and also if the payment is returned or cancelled after being sent. It is not guaranteed to stay set once populated."
          },
          "amount": {
            "type": "string",
            "format": "float",
            "description": "Total amount owed for this tax payment. Can be negative for corrections, refunds, or credits."
          },
          "amount_paid": {
            "type": "string",
            "format": "float",
            "description": "Amount paid toward this tax payment so far, sourced from the payment's running balance. \"0.00\" until paid; equal to `amount` once fully paid."
          },
          "line_items": {
            "type": "array",
            "description": "The payroll tax liabilities that make up this payment. Empty array when the payment has no associated payroll taxes. Only included in the response of GET /v1/companies/{company_uuid}/tax_payments/{uuid}. It is omitted from the list endpoint response.",
            "items": {
              "$ref": "#/components/schemas/Tax-Payment-Line-Item"
            }
          }
        },
        "required": [
          "uuid",
          "company_uuid",
          "agency_name",
          "jurisdiction",
          "period_start",
          "period_end",
          "due_date",
          "amount",
          "amount_paid"
        ]
      },
      "Tax-Payment-Line-Item": {
        "type": "object",
        "description": "A single payroll tax liability rolled up into a tax payment",
        "properties": {
          "payroll_uuid": {
            "type": "string",
            "description": "Unique identifier of the payroll this liability came from"
          },
          "unique_tax_id": {
            "type": "string",
            "description": "Unique identifier of the tax type this liability is for"
          },
          "amount": {
            "type": "string",
            "format": "float",
            "description": "The amount of this liability included in the tax payment"
          }
        },
        "required": [
          "payroll_uuid",
          "unique_tax_id",
          "amount"
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
    "/v1/companies/{company_uuid}/tax_payments/{uuid}": {
      "get": {
        "summary": "Get a tax payment for a company",
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
            "name": "uuid",
            "in": "path",
            "required": true,
            "description": "The UUID of the tax payment",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-tax-payment",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetches a single tax payment by UUID, including the payroll tax liabilities that make up the payment.\n\nscope: `tax_payments:read`",
        "tags": [
          "Tax Payments"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Payment/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Tax-Payment"
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
