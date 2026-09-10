---
updatedAt: 2026-04-20T21:24:14.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Check company migration readiness

Check if an existing Gusto customer is ready to be migrated to embedded payroll. This endpoint returns blockers and warnings associated with migrating the company and is recommended to be called before attempting to migrate a company.

scope: `partner_managed_companies:read`

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
      "Migration-Blocker": {
        "description": "Migration blocker that blocks company migration",
        "type": "object",
        "properties": {
          "errors": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "error_key": {
                  "type": "string",
                  "description": "Error key"
                },
                "category": {
                  "type": "string",
                  "description": "Error category"
                },
                "message": {
                  "type": "string",
                  "description": "Blocker message"
                },
                "metadata": {
                  "type": "object",
                  "properties": {
                    "key": {
                      "type": "string",
                      "description": "A categorization of the migration blocker, e.g. \"migrated_company\""
                    }
                  }
                }
              }
            }
          }
        }
      },
      "Migration-Warning": {
        "description": "Migration warning that does not block company migration",
        "type": "object",
        "properties": {
          "warnings": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "error_key": {
                  "type": "string",
                  "description": "Error key"
                },
                "category": {
                  "type": "string",
                  "description": "Error category"
                },
                "message": {
                  "type": "string",
                  "description": "Warning message"
                },
                "metadata": {
                  "type": "object",
                  "properties": {
                    "key": {
                      "type": "string",
                      "description": "A categorization of the migration warning, e.g. \"marijuana_related_business\""
                    }
                  }
                }
              }
            }
          }
        }
      },
      "Partner-Managed-Company-Migration-Readiness-Response": {
        "description": "",
        "allOf": [
          {
            "type": "object",
            "properties": {
              "ready_to_migrate": {
                "type": "boolean",
                "description": "Indicates if the company is ready to be migrated."
              },
              "company_uuid": {
                "type": "string",
                "description": "The company UUID"
              }
            }
          },
          {
            "$ref": "#/components/schemas/Migration-Blocker"
          },
          {
            "$ref": "#/components/schemas/Migration-Warning"
          }
        ],
        "x-examples": {
          "Example": {
            "ready_to_migrate": false,
            "company_uuid": "39abf9b9-650b-4e67-89a0-389dc6ee8a71",
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "The operation is already performed for this company.",
                "metadata": {
                  "key": "migrated_company"
                }
              }
            ],
            "warnings": []
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
    "/v1/partner_managed_companies/{company_uuid}/migration_readiness": {
      "get": {
        "summary": "Check company migration readiness",
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
        "operationId": "get-v1-partner-managed-companies-company-uuid-migration_readiness",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Check if an existing Gusto customer is ready to be migrated to embedded payroll. This endpoint returns blockers and warnings associated with migrating the company and is recommended to be called before attempting to migrate a company.\n\nscope: `partner_managed_companies:read`",
        "tags": [
          "Companies"
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
                      "$ref": "#/components/schemas/Partner-Managed-Company-Migration-Readiness-Response/x-examples/Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Partner-Managed-Company-Migration-Readiness-Response"
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
