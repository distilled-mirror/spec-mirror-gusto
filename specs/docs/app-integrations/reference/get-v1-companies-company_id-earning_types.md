---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all earning types for a company

A payroll item in Gusto is associated to an earning type to name the type of earning described by the payroll item.

#### Default Earning Type
Certain earning types are special because they have tax considerations. Those earning types are mostly the same for every company depending on its legal structure (LLC, Corporation, etc.)

#### Custom Earning Type
Custom earning types are all the other earning types added specifically for a company.

scope: `payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Earning Types"
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
      "Earning-Type": {
        "description": "The representation of an earning type in Gusto.",
        "type": "object",
        "x-examples": {
          "success": {
            "name": "Cash Tips",
            "uuid": "f5618c94-ed7d-4366-b2c4-ff05e430064f",
            "active": true
          },
          "custom_earning_type": {
            "name": "Gym Membership Stipend",
            "uuid": "6b4a8efb-db90-4c13-a75f-aae11b3f4ff9",
            "active": true
          }
        },
        "properties": {
          "name": {
            "type": "string",
            "description": "The name of the earning type."
          },
          "uuid": {
            "type": "string",
            "description": "The ID of the earning type.",
            "readOnly": true
          },
          "active": {
            "type": "boolean",
            "description": "Whether the earning type is active."
          }
        },
        "x-tags": [
          "Earning Types"
        ],
        "required": [
          "uuid"
        ]
      },
      "Earning-Type-List": {
        "type": "object",
        "description": "Lists of default and custom earning types for a company.",
        "x-examples": {
          "success": {
            "default": [
              {
                "name": "Bonus",
                "uuid": "b82e35c5-d7c6-4705-9e16-9f87499ade18",
                "active": true
              },
              {
                "name": "Cash Tips",
                "uuid": "f5618c94-ed7d-4366-b2c4-ff05e430064f",
                "active": true
              },
              {
                "name": "Commission",
                "uuid": "60191999-004a-49d9-b163-630574433653",
                "active": true
              },
              {
                "name": "Correction Payment",
                "uuid": "368226e0-8e8c-48f0-bc91-aee46caafbc9",
                "active": true
              },
              {
                "name": "Minimum Wage Adjustment",
                "uuid": "88a2e519-9ff5-4c19-9071-6a709f3c2939",
                "active": true
              },
              {
                "name": "Paycheck Tips",
                "uuid": "a3eaf03d-e712-4144-8f9b-71a85528adcf",
                "active": true
              },
              {
                "name": "Severance",
                "uuid": "a6a2eba7-6c7d-4ced-bbe8-43452fbc9f63",
                "active": true
              }
            ],
            "custom": [
              {
                "name": "Gym Membership Stipend",
                "uuid": "6b4a8efb-db90-4c13-a75f-aae11b3f4ff9",
                "active": true
              }
            ]
          },
          "defaults_only": {
            "default": [
              {
                "name": "Bonus",
                "uuid": "b82e35c5-d7c6-4705-9e16-9f87499ade18",
                "active": true
              },
              {
                "name": "Cash Tips",
                "uuid": "f5618c94-ed7d-4366-b2c4-ff05e430064f",
                "active": true
              },
              {
                "name": "Commission",
                "uuid": "60191999-004a-49d9-b163-630574433653",
                "active": true
              },
              {
                "name": "Correction Payment",
                "uuid": "368226e0-8e8c-48f0-bc91-aee46caafbc9",
                "active": true
              },
              {
                "name": "Minimum Wage Adjustment",
                "uuid": "88a2e519-9ff5-4c19-9071-6a709f3c2939",
                "active": true
              },
              {
                "name": "Paycheck Tips",
                "uuid": "a3eaf03d-e712-4144-8f9b-71a85528adcf",
                "active": true
              },
              {
                "name": "Severance",
                "uuid": "a6a2eba7-6c7d-4ced-bbe8-43452fbc9f63",
                "active": true
              }
            ],
            "custom": []
          }
        },
        "properties": {
          "default": {
            "type": "array",
            "description": "The default earning types for the company.",
            "items": {
              "$ref": "#/components/schemas/Earning-Type"
            }
          },
          "custom": {
            "type": "array",
            "description": "The custom earning types for the company.",
            "items": {
              "$ref": "#/components/schemas/Earning-Type"
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
    "/v1/companies/{company_id}/earning_types": {
      "get": {
        "summary": "Get all earning types for a company",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-earning_types",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "A payroll item in Gusto is associated to an earning type to name the type of earning described by the payroll item.\n\n#### Default Earning Type\nCertain earning types are special because they have tax considerations. Those earning types are mostly the same for every company depending on its legal structure (LLC, Corporation, etc.)\n\n#### Custom Earning Type\nCustom earning types are all the other earning types added specifically for a company.\n\nscope: `payrolls:read`",
        "tags": [
          "Earning Types"
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
                  "success": {
                    "value": {
                      "$ref": "#/components/schemas/Earning-Type-List/x-examples/success"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Earning-Type-List"
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
