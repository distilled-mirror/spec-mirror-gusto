---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get contribution exclusions for a company benefit

Returns all contributions for a given company benefit and whether they are excluded or not.

Currently this endpoint only works for 401-k and Roth 401-k benefit types.

scope: `company_benefits:read`

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
      "Contribution-Exclusion": {
        "description": "The representation of a contribution exclusion for a company benefit.",
        "type": "object",
        "properties": {
          "contribution_uuid": {
            "type": "string",
            "description": "The UUID of the contribution type.",
            "example": "082dfd3e-5b55-11f0-bb42-ab7136ba04e2"
          },
          "contribution_type": {
            "type": "string",
            "description": "The name of the contribution type.",
            "example": "Bonus"
          },
          "excluded": {
            "type": "boolean",
            "description": "Whether this contribution type is excluded from the benefit."
          }
        },
        "required": [
          "contribution_uuid",
          "contribution_type",
          "excluded"
        ],
        "x-tags": [
          "Company Benefits"
        ],
        "x-examples": {
          "exclusion_bonus": {
            "contribution_uuid": "b82e35c5-d7c6-4705-9e16-9f87499ade18",
            "contribution_type": "Bonus",
            "excluded": false
          },
          "exclusion_cash_tips": {
            "contribution_uuid": "f5618c94-ed7d-4366-b2c4-ff05e430064f",
            "contribution_type": "Cash Tips",
            "excluded": false
          },
          "exclusion_commission": {
            "contribution_uuid": "60191999-004a-49d9-b163-630574433653",
            "contribution_type": "Commission",
            "excluded": false
          },
          "exclusion_regular": {
            "contribution_uuid": "75a7a827-1f2d-4d6f-94f2-514c1fc32b13",
            "contribution_type": "Regular",
            "excluded": false
          },
          "exclusion_imputed": {
            "contribution_uuid": "eead3c7c-7964-4e3c-b609-670456127b09",
            "contribution_type": "Life insurance imputed benefit",
            "excluded": true
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
    "/v1/company_benefits/{company_benefit_id}/contribution_exclusions": {
      "get": {
        "summary": "Get contribution exclusions for a company benefit",
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
            "name": "company_benefit_id",
            "in": "path",
            "description": "The UUID of the company benefit",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-company_benefits-company_benefit_id-contribution_exclusions",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns all contributions for a given company benefit and whether they are excluded or not.\n\nCurrently this endpoint only works for 401-k and Roth 401-k benefit types.\n\nscope: `company_benefits:read`",
        "tags": [
          "Company Benefits"
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
                  "typical_exclusions": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Contribution-Exclusion/x-examples/exclusion_bonus"
                      },
                      {
                        "$ref": "#/components/schemas/Contribution-Exclusion/x-examples/exclusion_cash_tips"
                      },
                      {
                        "$ref": "#/components/schemas/Contribution-Exclusion/x-examples/exclusion_commission"
                      },
                      {
                        "$ref": "#/components/schemas/Contribution-Exclusion/x-examples/exclusion_regular"
                      },
                      {
                        "$ref": "#/components/schemas/Contribution-Exclusion/x-examples/exclusion_imputed"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Contribution-Exclusion"
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
