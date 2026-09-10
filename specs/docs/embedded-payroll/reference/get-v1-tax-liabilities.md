---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get tax liabilities

Get tax liabilities from aggregate external payrolls for a company.

scope: `external_payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "External Payrolls"
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
      "Tax-Liabilities-Selections": {
        "description": "The representation of tax liabilities selections.",
        "x-tags": [
          "External Payrolls"
        ],
        "title": "",
        "type": "object",
        "properties": {
          "tax_id": {
            "type": "integer",
            "description": "The ID of the tax.",
            "readOnly": true
          },
          "tax_name": {
            "type": "string",
            "description": "The name of the tax.",
            "readOnly": true
          },
          "description": {
            "type": [
              "string",
              "null"
            ],
            "description": "A description of the tax, providing additional detail about the tax type.",
            "readOnly": true
          },
          "last_unpaid_external_payroll_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of last unpaid external payroll.",
            "readOnly": true
          },
          "possible_liabilities": {
            "type": "array",
            "description": "Possible tax liabilities selections.",
            "readOnly": true,
            "items": {
              "type": "object",
              "properties": {
                "liability_amount": {
                  "type": "string",
                  "description": "Liability amount.",
                  "readOnly": true
                },
                "payroll_check_date": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The external payroll check date.",
                  "readOnly": true
                },
                "external_payroll_uuid": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The UUID of the external payroll.",
                  "readOnly": true
                }
              }
            }
          }
        },
        "x-examples": {
          "Example": {
            "tax_id": 1,
            "tax_name": "Federal Income Tax",
            "description": "Employee Federal Income Tax",
            "last_unpaid_external_payroll_uuid": null,
            "possible_liabilities": [
              {
                "liability_amount": "0.0",
                "payroll_check_date": null,
                "external_payroll_uuid": null
              },
              {
                "liability_amount": "3000.0",
                "payroll_check_date": "2022-06-01",
                "external_payroll_uuid": "1bf1efe1-72d4-4e6e-a181-611f3ea66435"
              }
            ]
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
    "/v1/companies/{company_uuid}/external_payrolls/tax_liabilities": {
      "get": {
        "summary": "Get tax liabilities",
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
        "operationId": "get-v1-tax-liabilities",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "tags": [
          "External Payrolls"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "description": "Get tax liabilities from aggregate external payrolls for a company.\n\nscope: `external_payrolls:read`",
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "Example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Tax-Liabilities-Selections/x-examples/Example"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Tax-Liabilities-Selections"
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
