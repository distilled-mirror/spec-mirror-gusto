---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a supported benefit

Returns a benefit supported by Gusto. The benefit object in Gusto contains high level information about a particular benefit type and its tax considerations. When companies choose to offer a benefit, they are creating a Company Benefit object associated with a particular benefit.

scope: `benefits:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Company Benefits"
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
      "Supported-Benefit": {
        "description": "",
        "type": "object",
        "properties": {
          "benefit_type": {
            "type": "integer",
            "description": "The benefit type in Gusto.",
            "readOnly": true
          },
          "name": {
            "type": "string",
            "description": "The name of the benefit.",
            "readOnly": true
          },
          "description": {
            "type": "string",
            "description": "The description of the benefit.",
            "readOnly": true
          },
          "pretax": {
            "type": "boolean",
            "description": "Whether the benefit is deducted before tax calculations, thus reducing one’s taxable income",
            "readOnly": true
          },
          "posttax": {
            "type": "boolean",
            "description": "Whether the benefit is deducted after tax calculations.",
            "readOnly": true
          },
          "imputed": {
            "type": "boolean",
            "description": "Whether the benefit is considered imputed income.",
            "readOnly": true
          },
          "healthcare": {
            "type": "boolean",
            "description": "Whether the benefit is healthcare related.",
            "readOnly": true
          },
          "retirement": {
            "type": "boolean",
            "description": "Whether the benefit is associated with retirement planning.",
            "readOnly": true
          },
          "yearly_limit": {
            "type": "boolean",
            "description": "Whether the benefit has a government mandated yearly limit. If the benefit has a government mandated yearly limit, employees cannot be added to more than one benefit of this type.",
            "readOnly": true
          },
          "category": {
            "type": "string",
            "description": "Category where the benefit belongs to.",
            "readOnly": true
          },
          "writable_by_application": {
            "type": "boolean",
            "description": "Whether this benefit can be written (created, updated, or destroyed). Returns true if the benefit type is permitted for the application, false otherwise.",
            "readOnly": true
          }
        },
        "x-examples": {
          "Example": {
            "benefit_type": 1,
            "name": "Medical Insurance",
            "description": "Deductions and contributions for Medical Insurance",
            "pretax": true,
            "posttax": false,
            "imputed": false,
            "healthcare": true,
            "retirement": false,
            "yearly_limit": false,
            "category": "Health"
          },
          "Supported-Benefits-List": {
            "benefit_type": 1,
            "name": "Medical Insurance",
            "description": "Deductions and contributions for Medical Insurance",
            "pretax": true,
            "posttax": false,
            "imputed": false,
            "healthcare": true,
            "retirement": false,
            "yearly_limit": false,
            "category": "Health"
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
    "/v1/benefits/{benefit_id}": {
      "get": {
        "summary": "Get a supported benefit",
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
            "name": "benefit_id",
            "in": "path",
            "description": "The benefit type in Gusto.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-benefits-benefit_id",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a benefit supported by Gusto. The benefit object in Gusto contains high level information about a particular benefit type and its tax considerations. When companies choose to offer a benefit, they are creating a Company Benefit object associated with a particular benefit.\n\nscope: `benefits:read`",
        "tags": [
          "Company Benefits"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Successful",
            "content": {
              "application/json": {
                "examples": {
                  "Example": {
                    "value": {
                      "$ref": "#/components/schemas/Supported-Benefit/x-examples/Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Supported-Benefit"
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
