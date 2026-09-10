---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Update employee onboarding documents config

Indicate whether to include the Form I-9 for an employee during the onboarding process.
If included, the employee will be prompted to complete Form I-9 as part of their onboarding.

## Related guides
- [Employee onboarding](doc:employee-onboarding)

scope: `employees:manage`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employees"
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
      "Employee-Onboarding-Document": {
        "type": "object",
        "description": "Configuration for which onboarding documents (e.g. Form I-9) are required for an employee during onboarding.",
        "properties": {
          "uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the onboarding documents config record. Null when no config has been saved yet.",
            "readOnly": true
          },
          "i9_document": {
            "type": "boolean",
            "description": "Whether to include Form I-9 for this employee during onboarding.\nWhen true, the employee will be prompted to complete Form I-9 as part of their onboarding.\n",
            "readOnly": true
          }
        },
        "x-examples": {
          "config_with_i9": {
            "uuid": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "i9_document": true
          },
          "config_without_i9": {
            "uuid": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "i9_document": false
          },
          "config_not_yet_saved": {
            "uuid": null,
            "i9_document": false
          }
        }
      },
      "Employee-Onboarding-Documents-Config-Request": {
        "type": "object",
        "description": "Request body for updating an employee's onboarding documents configuration.",
        "properties": {
          "i9_document": {
            "type": "boolean",
            "default": false,
            "description": "Whether to include Form I-9 for this employee during onboarding.\nWhen true, the employee will be prompted to complete Form I-9 as part of their onboarding.\n"
          }
        },
        "x-examples": {
          "enable_i9": {
            "i9_document": true
          },
          "disable_i9": {
            "i9_document": false
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
    "/v1/employees/{employee_id}/onboarding_documents_config": {
      "put": {
        "summary": "Update employee onboarding documents config",
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
            "name": "employee_id",
            "in": "path",
            "required": true,
            "description": "The UUID of the employee",
            "example": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "put-v1-employees-employee_id-onboarding_documents_config",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Indicate whether to include the Form I-9 for an employee during the onboarding process.\nIf included, the employee will be prompted to complete Form I-9 as part of their onboarding.\n\n## Related guides\n- [Employee onboarding](https://docs.gusto.com/embedded-payroll/docs/employee-onboarding)\n\nscope: `employees:manage`",
        "tags": [
          "Employees"
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
                  "config_with_i9": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Onboarding-Document/x-examples/config_with_i9"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Onboarding-Document"
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
        },
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Employee-Onboarding-Documents-Config-Request"
              }
            }
          }
        }
      }
    }
  }
}
```
