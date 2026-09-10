---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get the custom fields of a company

Returns a list of the custom fields of the company. Useful when you need to know the schema of custom fields for an entire company.

scope: `companies:read`

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
      "Custom-Field-Type": {
        "type": "string",
        "description": "Input type for the custom field.",
        "enum": [
          "text",
          "currency",
          "number",
          "date",
          "radio"
        ]
      },
      "Company-Custom-Field": {
        "type": "object",
        "description": "A custom field on a company",
        "x-tags": [
          "Custom Fields"
        ],
        "properties": {
          "uuid": {
            "type": "string",
            "description": "UUID of the company custom field"
          },
          "name": {
            "type": "string",
            "description": "Name of the company custom field"
          },
          "type": {
            "$ref": "#/components/schemas/Custom-Field-Type"
          },
          "description": {
            "type": [
              "string",
              "null"
            ],
            "description": "Description of the company custom field"
          },
          "selection_options": {
            "type": [
              "array",
              "null"
            ],
            "description": "An array of options for fields of type radio. Otherwise, null.",
            "items": {
              "type": "string"
            }
          }
        },
        "required": [
          "uuid",
          "name",
          "type"
        ]
      },
      "Company-Custom-Field-List": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "custom_fields": [
              {
                "uuid": "ea7e5d57-6abb-47d7-b654-347c142886c0",
                "name": "employee_level",
                "description": "Employee Level",
                "type": "text",
                "selection_options": null
              },
              {
                "uuid": "024ec137-6c92-43a3-b061-14a9720531d6",
                "name": "favorite fruit",
                "description": "Which is your favorite fruit?",
                "type": "radio",
                "selection_options": [
                  "apple",
                  "banana",
                  "orange"
                ]
              }
            ]
          }
        },
        "properties": {
          "custom_fields": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Company-Custom-Field"
            }
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
    "/v1/companies/{company_id}/custom_fields": {
      "get": {
        "summary": "Get the custom fields of a company",
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
        "operationId": "get-v1-companies-company_id-custom_fields",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a list of the custom fields of the company. Useful when you need to know the schema of custom fields for an entire company.\n\nscope: `companies:read`",
        "tags": [
          "Companies"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Company-Custom-Field-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Company-Custom-Field-List"
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
