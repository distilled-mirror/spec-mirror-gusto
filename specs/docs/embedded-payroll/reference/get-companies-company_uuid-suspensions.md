---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get suspensions for this company

Get existing suspension records for this company. A company may have multiple suspension records if they have suspended their Gusto account more than once.

>📘 To check if company is already suspended
>
> To determine if a company is _currently_ suspended, use the `is_suspended` and `company_status` fields in the [Get a company](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies) endpoint.

scope: `company_suspensions:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Companies"
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
      "Company-Suspension": {
        "type": "object",
        "description": "Record representing the suspension of a company's Gusto account.",
        "x-examples": {
          "switching_provider": {
            "uuid": "ade4528c-6cc4-4bd5-917a-9d636317e7d6",
            "company_uuid": "3a0e3fb7-3d4b-4c7c-8ba0-9ce3c9f1f3be",
            "effective_date": "2025-07-23",
            "reason": "switching_provider",
            "leaving_for": "adp",
            "reconcile_tax_method": "refund_taxes",
            "file_yearly_forms": false,
            "file_quarterly_forms": false,
            "comments": null,
            "tax_refunds": []
          },
          "shutting_down": {
            "uuid": "5f04b8d0-1a41-40c6-9f5e-10b26ed89729",
            "company_uuid": "3a0e3fb7-3d4b-4c7c-8ba0-9ce3c9f1f3be",
            "effective_date": "2025-07-23",
            "reason": "shutting_down",
            "leaving_for": null,
            "reconcile_tax_method": "pay_taxes",
            "file_yearly_forms": true,
            "file_quarterly_forms": true,
            "comments": null,
            "tax_refunds": []
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier for this suspension."
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier for the company which is suspended."
          },
          "effective_date": {
            "type": "string",
            "description": "Date that the suspension took effect."
          },
          "leaving_for": {
            "type": [
              "string",
              "null"
            ],
            "description": "Which competitor the company is joining instead. Only required if `reason` is `'switching_provider'`."
          },
          "reason": {
            "type": "string",
            "description": "Explanation for why the company's account was suspended."
          },
          "reconcile_tax_method": {
            "type": "string",
            "description": "How Gusto will handle taxes already collected.",
            "enum": [
              "pay_taxes",
              "refund_taxes"
            ]
          },
          "file_quarterly_forms": {
            "type": "boolean",
            "description": "Should Gusto file quarterly tax forms on behalf of the company? The correct answer can depend on why the company is suspending their account, and how taxes are being reconciled.\n"
          },
          "file_yearly_forms": {
            "type": "boolean",
            "description": "Should Gusto file yearly tax forms on behalf of the company? The correct answer can depend on why the company is suspending their account, and how taxes are being reconciled.\n"
          },
          "comments": {
            "type": [
              "string",
              "null"
            ],
            "description": "User-supplied comments describing why they are suspending their account."
          },
          "tax_refunds": {
            "type": "array",
            "description": "Describes the taxes which are refundable to the company for this suspension. These may be refunded or paid by Gusto depending on the value in `reconcile_tax_method`.\n",
            "items": {
              "type": "object",
              "properties": {
                "amount": {
                  "type": "string",
                  "description": "Dollar amount."
                },
                "description": {
                  "type": "string",
                  "description": "What kind of tax this is."
                }
              }
            }
          }
        }
      },
      "Company-Suspension-List": {
        "type": "array",
        "description": "List of suspension records for a company.",
        "items": {
          "$ref": "#/components/schemas/Company-Suspension"
        },
        "x-examples": {
          "success_status": [
            {
              "uuid": "3bd0fa7c-071e-4e85-a6bf-f73a69797694",
              "company_uuid": "3a0e3fb7-3d4b-4c7c-8ba0-9ce3c9f1f3be",
              "effective_date": "2025-07-23",
              "reason": "shutting_down",
              "leaving_for": null,
              "reconcile_tax_method": "refund_taxes",
              "file_yearly_forms": false,
              "file_quarterly_forms": false,
              "comments": null,
              "tax_refunds": []
            },
            {
              "uuid": "2ad79a4e-2fbd-43ca-a77b-e9049e6cab15",
              "company_uuid": "3a0e3fb7-3d4b-4c7c-8ba0-9ce3c9f1f3be",
              "effective_date": "2025-07-23",
              "reason": "switching_provider",
              "leaving_for": "adp",
              "reconcile_tax_method": "refund_taxes",
              "file_yearly_forms": false,
              "file_quarterly_forms": false,
              "comments": "Company is transitioning to ADP for their payroll and HR needs",
              "tax_refunds": []
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
    "/v1/companies/{company_uuid}/suspensions": {
      "get": {
        "summary": "Get suspensions for this company",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-companies-company_uuid-suspensions",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get existing suspension records for this company. A company may have multiple suspension records if they have suspended their Gusto account more than once.\n\n>📘 To check if company is already suspended\n>\n> To determine if a company is _currently_ suspended, use the `is_suspended` and `company_status` fields in the [Get a company](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies) endpoint.\n\nscope: `company_suspensions:read`",
        "tags": [
          "Companies"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Successful response",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Company-Suspension-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Company-Suspension-List"
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
