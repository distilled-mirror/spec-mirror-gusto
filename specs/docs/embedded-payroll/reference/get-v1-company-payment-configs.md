---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a company's payment configs

Get payment speed configurations for the company: payment speed (1-day, 2-day, or 4-day ACH), fast payment limit, partner-owned disbursement setting, and earned fast ACH blockers when applicable. 1-day is only available to partners that opt in.

### Related guides
- [Payroll Processing Speeds](doc:2-day-vs-4-day)

scope: `company_payment_configs:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Payment Configs"
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
      "Payment-Configs": {
        "title": "Payment-Configs",
        "type": "object",
        "properties": {
          "company_uuid": {
            "type": "string",
            "description": "Company uuid",
            "readOnly": true
          },
          "partner_uuid": {
            "type": "string",
            "description": "Partner uuid",
            "readOnly": true
          },
          "fast_payment_limit": {
            "type": [
              "string",
              "null"
            ],
            "description": "Payment limit for 1-day or 2-day payroll (string representation of decimal).",
            "readOnly": true
          },
          "payment_speed": {
            "type": "string",
            "enum": [
              "1-day",
              "2-day",
              "4-day"
            ],
            "description": "Payment speed. READ-ONLY.\n- `1-day`: Next-day ACH (only for partners that opt in).\n- `2-day`: Two-day ACH.\n- `4-day`: Standard ACH.\n",
            "readOnly": true
          },
          "partner_owned_disbursement": {
            "type": "boolean",
            "description": "Whether the company is configured to use the partner-owned disbursement payment rail",
            "readOnly": true
          },
          "earned_fast_ach_blockers": {
            "type": "array",
            "description": "Blockers preventing the company from earning fast ACH payments",
            "readOnly": true,
            "items": {
              "type": "object",
              "properties": {
                "blocker_type": {
                  "type": "string",
                  "description": "The type of blocker",
                  "enum": [
                    "minimum_days",
                    "minimum_funded_payments"
                  ],
                  "readOnly": true
                },
                "threshold": {
                  "type": "number",
                  "description": "The threshold needed to unblock",
                  "readOnly": true
                }
              }
            }
          }
        },
        "x-examples": {
          "typical_payment_config": {
            "company_uuid": "423dd616-6dbc-4724-938a-403f6217a933",
            "partner_uuid": "556f05d0-48e0-4c47-bce5-db9aea923043",
            "fast_payment_limit": "5000.0",
            "payment_speed": "2-day",
            "partner_owned_disbursement": false,
            "earned_fast_ach_blockers": []
          },
          "payment_config_with_blockers": {
            "company_uuid": "423dd616-6dbc-4724-938a-403f6217a933",
            "partner_uuid": "556f05d0-48e0-4c47-bce5-db9aea923043",
            "fast_payment_limit": null,
            "payment_speed": "2-day",
            "partner_owned_disbursement": false,
            "earned_fast_ach_blockers": [
              {
                "blocker_type": "minimum_days",
                "threshold": 15
              },
              {
                "blocker_type": "minimum_funded_payments",
                "threshold": 5
              }
            ]
          }
        },
        "x-tags": [
          "Payment Configs"
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
    "/v1/companies/{company_uuid}/payment_configs": {
      "get": {
        "summary": "Get a company's payment configs",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-company-payment-configs",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get payment speed configurations for the company: payment speed (1-day, 2-day, or 4-day ACH), fast payment limit, partner-owned disbursement setting, and earned fast ACH blockers when applicable. 1-day is only available to partners that opt in.\n\n### Related guides\n- [Payroll Processing Speeds](https://docs.gusto.com/embedded-payroll/docs/2-day-vs-4-day)\n\nscope: `company_payment_configs:read`",
        "tags": [
          "Payment Configs"
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
                  "typical_payment_config": {
                    "value": {
                      "$ref": "#/components/schemas/Payment-Configs/x-examples/typical_payment_config"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payment-Configs"
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
