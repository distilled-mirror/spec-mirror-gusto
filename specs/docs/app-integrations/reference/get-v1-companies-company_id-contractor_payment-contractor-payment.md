---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a single contractor payment

Returns a single contractor payment.

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
      "Contractor-Payment": {
        "description": "The representation of a single contractor payment.",
        "type": "object",
        "x-examples": {
          "success_status": {
            "uuid": "04552eb9-7829-4b18-ae96-6983552948df",
            "contractor_uuid": "bc57832c-d8bc-43a7-ae99-3a03380ff037,",
            "bonus": "20.0",
            "date": "2020-10-19",
            "hours": "40.0",
            "payment_method": "Direct Deposit",
            "reimbursement": "100.0",
            "hourly_rate": "18.0",
            "may_cancel": true,
            "status": "Funded",
            "wage": "0.0",
            "wage_type": "Hourly",
            "wage_total": "740.00"
          },
          "example": {
            "uuid": "04552eb9-7829-4b18-ae96-6983552948df",
            "contractor_uuid": "bc57832c-d8bc-43a7-ae99-3a03380ff037",
            "bonus": "20.0",
            "date": "2020-10-19",
            "hours": "40.0",
            "payment_method": "Direct Deposit",
            "reimbursement": "100.0",
            "hourly_rate": "18.0",
            "may_cancel": false,
            "status": "Funded",
            "wage": "0.0",
            "wage_type": "Hourly",
            "wage_total": "740.00"
          }
        },
        "title": "Contractor Payment",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The unique identifier of the contractor payment in Gusto.",
            "readOnly": true
          },
          "contractor_uuid": {
            "type": "string",
            "description": "The UUID of the contractor.",
            "readOnly": true
          },
          "bonus": {
            "type": "string",
            "format": "float",
            "description": "The bonus amount in the payment.",
            "readOnly": true
          },
          "date": {
            "type": "string",
            "description": "The payment date.",
            "readOnly": true
          },
          "hours": {
            "type": "string",
            "format": "float",
            "description": "The number of hours worked for the payment.",
            "readOnly": true
          },
          "payment_method": {
            "type": "string",
            "description": "The payment method.",
            "enum": [
              "Direct Deposit",
              "Check",
              "Historical Payment",
              "Correction Payment"
            ],
            "readOnly": true
          },
          "reimbursement": {
            "type": "string",
            "format": "float",
            "description": "The reimbursement amount in the payment.",
            "readOnly": true
          },
          "status": {
            "type": "string",
            "description": "Contractor payment status",
            "enum": [
              "Funded",
              "Unfunded"
            ]
          },
          "hourly_rate": {
            "type": "string",
            "format": "float",
            "description": "The rate per hour worked for the payment.",
            "readOnly": true
          },
          "may_cancel": {
            "type": "boolean",
            "description": "Determine if the contractor payment can be cancelled.",
            "readOnly": true
          },
          "wage": {
            "type": "string",
            "format": "float",
            "description": "The fixed wage of the payment, regardless of hours worked.",
            "readOnly": true
          },
          "wage_type": {
            "type": "string",
            "description": "The wage type for the payment.",
            "enum": [
              "Hourly",
              "Fixed"
            ],
            "readOnly": true
          },
          "wage_total": {
            "type": "string",
            "format": "float",
            "description": "(hours * hourly_rate) + wage + bonus",
            "readOnly": true
          },
          "invoice_number": {
            "type": [
              "string",
              "null"
            ],
            "description": "An optional invoice number associated with this contractor payment. This will be visible to the contractor on their paystub. Maximum 25 characters.",
            "readOnly": true
          },
          "memo": {
            "type": [
              "string",
              "null"
            ],
            "description": "An optional note or memo for this contractor payment. This will be visible to the contractor on their paystub.",
            "readOnly": true
          }
        },
        "x-tags": [
          "Contractor Payments"
        ],
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
    "/v1/companies/{company_id}/contractor_payments/{contractor_payment_id}": {
      "get": {
        "summary": "Get a single contractor payment",
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
            "required": true,
            "description": "The UUID of the company",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "contractor_payment_id",
            "in": "path",
            "required": true,
            "description": "The UUID of the contractor payment",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-contractor_payment-contractor-payment",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a single contractor payment.\n\nscope: `payrolls:read`",
        "tags": [
          "Contractor Payments"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Contractor-Payment/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Contractor-Payment"
                }
              }
            }
          },
          "404": {
            "description": "Not Found\n\nThe requested resource does not exist. Make sure the provided ID/UUID is valid.\n",
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
