---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get approved payroll reversals

Returns all approved Payroll Reversals for a Company.

scope: `payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Payrolls"
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
      "Payroll-Reversal": {
        "type": "object",
        "properties": {
          "reversed_payroll_uuid": {
            "type": "string",
            "description": "The UUID for the payroll run being reversed."
          },
          "reversal_payroll_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the payroll where the reversal was applied."
          },
          "reason": {
            "type": "string",
            "description": "A reason provided by the admin who created the reversal."
          },
          "approved_at": {
            "type": [
              "string",
              "null"
            ],
            "description": "Timestamp of when the reversal was approved."
          },
          "category": {
            "type": [
              "string",
              "null"
            ],
            "description": "Category chosen by the admin who requested the reversal."
          },
          "reversed_employee_uuids": {
            "type": "array",
            "description": "Array of affected employee UUIDs.",
            "items": {
              "type": "string"
            }
          }
        },
        "x-examples": {
          "Example": {
            "reversed_payroll_uuid": "09505984-8d8c-41a3-adbe-5740322ae8e9",
            "reversal_payroll_uuid": "0424688e-0a2e-4cd0-ac86-42283e788fb3",
            "reason": "Customer Request",
            "approved_at": null,
            "category": "convert_check_ee_requested",
            "reversed_employee_uuids": [
              "5f036964-185e-4c85-bbf2-3873e1203b30"
            ]
          }
        }
      },
      "Payroll-Reversal-List": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Payroll-Reversal"
        },
        "x-examples": {
          "Example": [
            {
              "reversed_payroll_uuid": "09505984-8d8c-41a3-adbe-5740322ae8e9",
              "reversal_payroll_uuid": "0424688e-0a2e-4cd0-ac86-42283e788fb3",
              "reason": "Customer Request",
              "approved_at": null,
              "category": "convert_check_ee_requested",
              "reversed_employee_uuids": [
                "5f036964-185e-4c85-bbf2-3873e1203b30"
              ]
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
    "/v1/companies/{company_id}/payroll_reversals": {
      "get": {
        "summary": "Get approved payroll reversals",
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
        "operationId": "get-v1-companies-company_id-payroll_reversals",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns all approved Payroll Reversals for a Company.\n\nscope: `payrolls:read`",
        "tags": [
          "Payrolls"
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
                  "Example": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Reversal-List/x-examples/Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payroll-Reversal-List"
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
