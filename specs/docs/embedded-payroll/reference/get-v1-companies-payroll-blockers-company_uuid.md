---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all payroll blockers for a company

Returns a list of reasons that prevent the company from running payrolls. See the [Payroll Blockers guide](doc:payroll-blockers) for a complete list of reasons. The list is empty if there are no payroll blockers.

scope: `payrolls:run`

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
      "Payroll-Blocker": {
        "type": "object",
        "required": [
          "key",
          "message"
        ],
        "properties": {
          "key": {
            "type": "string",
            "description": "A unique identifier for the payroll blocker reason. For a complete list of blockers and their meanings, see the [Payroll Blockers guide](https://docs.gusto.com/embedded-payroll/docs/payroll-blockers).",
            "enum": [
              "company_ownership_required",
              "contractor_only_company",
              "eftps_in_error",
              "geocode_error",
              "geocode_needed",
              "invalid_signatory",
              "missing_addresses",
              "missing_bank_info",
              "missing_bank_verification",
              "missing_employee_setup",
              "missing_federal_tax_setup",
              "missing_forms",
              "missing_industry_selection",
              "missing_pay_schedule",
              "missing_signatory",
              "missing_state_tax_setup",
              "needs_approval",
              "needs_onboarding",
              "pay_schedule_setup_not_complete",
              "pending_information_request",
              "pending_payroll_review",
              "pending_recovery_case",
              "soft_suspended",
              "suspended"
            ],
            "example": "needs_approval"
          },
          "message": {
            "type": "string",
            "description": "A human-readable message describing the payroll blocker and what action is needed to resolve it.",
            "example": "Company needs to be approved to run payroll."
          }
        },
        "x-examples": {
          "blockers_list": {
            "key": "needs_approval",
            "message": "Company needs to be approved to run payroll."
          },
          "empty_blockers_list": []
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
    "/v1/companies/{company_uuid}/payrolls/blockers": {
      "get": {
        "summary": "Get all payroll blockers for a company",
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
        "operationId": "get-v1-companies-payroll-blockers-company_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a list of reasons that prevent the company from running payrolls. See the [Payroll Blockers guide](https://docs.gusto.com/embedded-payroll/docs/payroll-blockers) for a complete list of reasons. The list is empty if there are no payroll blockers.\n\nscope: `payrolls:run`",
        "tags": [
          "Payrolls"
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
                  "blockers_list": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Payroll-Blocker/x-examples/blockers_list"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Payroll-Blocker"
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
