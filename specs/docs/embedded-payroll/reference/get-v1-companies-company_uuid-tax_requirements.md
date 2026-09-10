---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all tax requirements for a company

Retrieves all states for which a company has tax requirements, along with a boolean indicating whether tax setup
is complete for each state. Use this to determine which states still need tax setup during company onboarding.

scope: `company_tax_requirements:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Tax Requirements"
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
      "Tax-Requirement-States-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "state": "GA",
              "setup_status": "not_started",
              "default_rates_applied": false,
              "ready_to_run_payroll": false
            },
            {
              "state": "CA",
              "setup_status": "complete",
              "default_rates_applied": false,
              "ready_to_run_payroll": true
            }
          ]
        },
        "items": {
          "type": "object",
          "properties": {
            "state": {
              "$ref": "#/components/schemas/State"
            },
            "setup_status": {
              "type": "string",
              "enum": [
                "not_started",
                "in_progress",
                "complete"
              ],
              "description": "The current status of the state tax setup.\n- `not_started`: No requirements have been filled\n- `in_progress`: Some requirements have been filled, or default rates are applied\n- `complete`: All requirements have been filled without default rates\n"
            },
            "default_rates_applied": {
              "type": "boolean",
              "description": "Whether the state is using system-assigned default SUI rates rather than employer-specific rates."
            },
            "ready_to_run_payroll": {
              "type": "boolean",
              "description": "Whether the state tax setup is sufficiently complete for the company to run payroll."
            }
          }
        }
      },
      "State": {
        "title": "State",
        "type": "string",
        "example": "GA",
        "description": "One of the two-letter state abbreviations for the fifty United States and the District of Columbia (DC)"
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
    "/v1/companies/{company_uuid}/tax_requirements": {
      "get": {
        "summary": "Get all tax requirements for a company",
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
        "operationId": "get-v1-companies-company_uuid-tax_requirements",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieves all states for which a company has tax requirements, along with a boolean indicating whether tax setup\nis complete for each state. Use this to determine which states still need tax setup during company onboarding.\n\nscope: `company_tax_requirements:read`",
        "tags": [
          "Tax Requirements"
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
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Requirement-States-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Tax-Requirement-States-List"
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
