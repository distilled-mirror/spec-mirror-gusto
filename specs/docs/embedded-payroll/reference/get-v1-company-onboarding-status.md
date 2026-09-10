---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get company onboarding status

Retrieves a company's onboarding status, including whether onboarding is complete and the list of
required onboarding steps with their respective completion state.

scope: `company_onboarding_status:read`

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
      "Company-Onboarding-Status": {
        "description": "The representation of a company's onboarding status",
        "type": "object",
        "title": "",
        "x-examples": {
          "Example": {
            "uuid": "c44d66dc-c41b-4a60-9e25-5e93ff8583f2",
            "onboarding_completed": false,
            "onboarding_steps": [
              {
                "title": "Add Your Company's Addresses",
                "id": "add_addresses",
                "required": true,
                "completed": true,
                "completed_at": "2025-02-18T10:00:00Z",
                "skippable": false,
                "requirements": []
              },
              {
                "title": "Enter Your Federal Tax Information",
                "id": "federal_tax_setup",
                "required": true,
                "completed": true,
                "completed_at": "2025-02-18T10:00:00Z",
                "skippable": false,
                "requirements": []
              },
              {
                "title": "Select Industry",
                "id": "select_industry",
                "required": true,
                "completed": true,
                "completed_at": "2025-02-18T10:00:00Z",
                "skippable": false,
                "requirements": []
              },
              {
                "title": "Add Your Bank Account",
                "id": "add_bank_info",
                "required": true,
                "completed": true,
                "completed_at": "2025-02-18T10:00:00Z",
                "skippable": false,
                "requirements": []
              },
              {
                "title": "Add Your Employees",
                "id": "add_employees",
                "required": true,
                "completed": true,
                "completed_at": "2025-02-18T10:00:00Z",
                "skippable": true,
                "requirements": [
                  "add_addresses"
                ]
              },
              {
                "title": "Enter Your State Tax Information",
                "id": "state_setup",
                "required": true,
                "completed": false,
                "completed_at": null,
                "skippable": false,
                "requirements": [
                  "add_addresses",
                  "add_employees"
                ]
              },
              {
                "title": "Select a Pay Schedule",
                "id": "payroll_schedule",
                "required": true,
                "completed": false,
                "completed_at": null,
                "skippable": false,
                "requirements": []
              },
              {
                "title": "Sign Documents",
                "id": "sign_all_forms",
                "required": true,
                "completed": false,
                "completed_at": null,
                "skippable": false,
                "requirements": [
                  "add_employees",
                  "federal_tax_setup",
                  "state_setup",
                  "add_bank_info",
                  "payroll_schedule"
                ]
              },
              {
                "title": "Verify Your Bank Account",
                "id": "verify_bank_info",
                "required": true,
                "completed": false,
                "completed_at": null,
                "skippable": false,
                "requirements": [
                  "add_bank_info"
                ]
              }
            ]
          }
        },
        "x-tags": [
          "Companies"
        ],
        "properties": {
          "uuid": {
            "type": "string",
            "description": "the UUID of the company"
          },
          "onboarding_completed": {
            "type": "boolean",
            "description": "a boolean flag for the company's onboarding status"
          },
          "onboarding_steps": {
            "type": "array",
            "description": "a list of company onboarding steps",
            "items": {
              "title": "Onboarding step",
              "type": "object",
              "properties": {
                "title": {
                  "type": "string",
                  "description": "The display name of the onboarding step"
                },
                "id": {
                  "type": "string",
                  "description": "The string identifier for each onboarding step",
                  "enum": [
                    "add_addresses",
                    "federal_tax_setup",
                    "select_industry",
                    "add_bank_info",
                    "add_employees",
                    "state_setup",
                    "payroll_schedule",
                    "sign_all_forms",
                    "verify_bank_info",
                    "external_payroll"
                  ]
                },
                "required": {
                  "type": "boolean",
                  "description": "The boolean flag indicating whether the step is required or optional"
                },
                "completed": {
                  "type": "boolean",
                  "description": "The boolean flag indicating whether the step is completed or not."
                },
                "completed_at": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The ISO 8601 timestamp indicating when the onboarding step was completed."
                },
                "skippable": {
                  "type": "boolean",
                  "description": "The boolean flag indicating whether the step can be skipped or not."
                },
                "requirements": {
                  "type": "array",
                  "description": "A list of onboarding steps that are required to be completed in order to proceed with the current onboarding step.",
                  "items": {
                    "type": "string",
                    "enum": [
                      "add_addresses",
                      "federal_tax_setup",
                      "select_industry",
                      "add_bank_info",
                      "add_employees",
                      "state_setup",
                      "payroll_schedule",
                      "sign_all_forms",
                      "verify_bank_info",
                      "external_payroll"
                    ]
                  }
                }
              }
            }
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
    "/v1/companies/{company_uuid}/onboarding_status": {
      "get": {
        "summary": "Get company onboarding status",
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
            "example": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "additional_steps",
            "in": "query",
            "required": false,
            "example": "external_payroll",
            "description": "Comma-delimited string of additional onboarding steps to include. Currently only supports the value \"external_payroll\".",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-company-onboarding-status",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieves a company's onboarding status, including whether onboarding is complete and the list of\nrequired onboarding steps with their respective completion state.\n\nscope: `company_onboarding_status:read`",
        "tags": [
          "Companies"
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
                  "Example": {
                    "value": {
                      "$ref": "#/components/schemas/Company-Onboarding-Status/x-examples/Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Company-Onboarding-Status"
                }
              }
            }
          },
          "404": {
            "description": "Not Found",
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
