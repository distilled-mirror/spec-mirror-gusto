---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a department

Get a department given the UUID

scope: `departments:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Departments"
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
      "Versionable": {
        "type": "object",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          }
        }
      },
      "Department": {
        "type": "object",
        "allOf": [
          {
            "$ref": "#/components/schemas/Versionable"
          },
          {
            "type": "object",
            "properties": {
              "uuid": {
                "type": "string",
                "description": "The UUID of the department"
              },
              "company_uuid": {
                "type": "string",
                "description": "The UUID of the company"
              },
              "title": {
                "type": "string",
                "description": "Name of the department"
              },
              "employees": {
                "type": "array",
                "description": "Array of employees assigned to the department.",
                "items": {
                  "properties": {
                    "uuid": {
                      "type": "string"
                    }
                  }
                }
              },
              "contractors": {
                "type": "array",
                "description": "Array of contractors assigned to the department.",
                "items": {
                  "properties": {
                    "uuid": {
                      "type": "string"
                    }
                  }
                }
              }
            }
          }
        ],
        "x-examples": {
          "example": {
            "uuid": "56260b3d-c375-415c-b77a-75d99f717193",
            "company_uuid": "7087a288-8349-4632-b92e-bc94fb79f29e",
            "title": "Stage Hand",
            "version": "d90440dd464601d1c8f4e9e240dfb7a6",
            "employees": [
              {
                "uuid": "41199375-a999-4414-9f40-d9bf596b134d"
              }
            ],
            "contractors": [
              {
                "uuid": "3488549f-60e4-494f-a34a-9d8aad3aabf5"
              }
            ]
          },
          "example_created": {
            "uuid": "56260b3d-c375-415c-b77a-75d99f717193",
            "company_uuid": "7087a288-8349-4632-b92e-bc94fb79f29e",
            "title": "Stage Hand",
            "version": "d90440dd464601d1c8f4e9e240dfb7a6",
            "employees": [],
            "contractors": []
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
    "/v1/departments/{department_uuid}": {
      "get": {
        "summary": "Get a department",
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
            "name": "department_uuid",
            "in": "path",
            "description": "The UUID of the department",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-department",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get a department given the UUID\n\nscope: `departments:read`",
        "tags": [
          "Departments"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Department/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Department"
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
