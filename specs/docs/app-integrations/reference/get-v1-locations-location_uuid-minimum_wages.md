---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get minimum wages for a location

Get minimum wages for a location

scope: `companies:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Locations"
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
      "Minimum-Wage-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "uuid": "1b71bb5b-4811-46e9-8a8a-cf5521cbeda6",
              "authority": "City",
              "wage": "15.0",
              "wage_type": "Regular",
              "effective_date": "2017-01-01",
              "notes": "large companies"
            },
            {
              "uuid": "87434623-b57d-4630-8da5-9dde599c7840",
              "authority": "City",
              "wage": "10.5",
              "wage_type": "Regular",
              "effective_date": "2017-01-01",
              "notes": "large companies"
            },
            {
              "uuid": "fa055c11-bfe4-4ac3-84dd-8502cf046b20",
              "authority": "State",
              "wage": "10.5",
              "wage_type": "Regular",
              "effective_date": "2017-01-01",
              "notes": "large companies"
            },
            {
              "uuid": "cdd9dfc2-6465-4693-ae60-0eecff35038c",
              "authority": "Federal",
              "wage": "10.5",
              "wage_type": "Regular",
              "effective_date": "2017-01-01",
              "notes": "large companies"
            }
          ]
        },
        "items": {
          "$ref": "#/components/schemas/Minimum-Wage"
        }
      },
      "Minimum-Wage": {
        "type": "object",
        "description": "Representation of a Minimum Wage",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "unique identifier of a minimum wage"
          },
          "wage": {
            "type": "string",
            "format": "float",
            "description": "The wage rate for a minimum wage record. Represented as a float, e.g. \"15.0\"."
          },
          "wage_type": {
            "type": "string",
            "description": "The type of wage the minimum wage applies to, e.g. \"Regular\", \"Regular-Industry-Specific\"."
          },
          "effective_date": {
            "type": "string",
            "format": "date",
            "description": "The date the minimum wage rule is effective on."
          },
          "authority": {
            "type": "string",
            "description": "The governing authority that created the minimum wage, e.g. \"City\", \"State\", or \"Federal\"."
          },
          "notes": {
            "type": "string",
            "description": "Description of parties the minimum wage applies to."
          }
        },
        "required": [
          "uuid",
          "wage",
          "wage_type",
          "effective_date",
          "authority"
        ]
      },
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
    "/v1/locations/{location_uuid}/minimum_wages": {
      "get": {
        "summary": "Get minimum wages for a location",
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
            "name": "location_uuid",
            "in": "path",
            "description": "The UUID of the location",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "effective_date",
            "in": "query",
            "required": false,
            "example": "2020-01-31",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-locations-location_uuid-minimum_wages",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get minimum wages for a location\n\nscope: `companies:read`",
        "tags": [
          "Locations"
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
                      "$ref": "#/components/schemas/Minimum-Wage-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Minimum-Wage-List"
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
