---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get benefits for a company

Company benefits represent the benefits that a company is offering to employees. This ties together a particular supported benefit with the company-specific information for the offering of that benefit.

Note that company benefits can be deactivated only when no employees are enrolled.

Benefits containing PHI are only visible to applications with the `company_benefits:read:phi` scope.

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
      "Company-Benefit": {
        "description": "The representation of a company benefit.",
        "type": "object",
        "x-examples": {
          "Example": {
            "uuid": "54e37c27-43e6-4ae5-a5b2-e29895a133be",
            "version": "98jr3289h3298hr9329gf9egskt3kagri32qqgiqe3872",
            "benefit_type": 1,
            "active": true,
            "description": "Kaiser Permanente",
            "enrollment_count": 2,
            "source": "external",
            "partner_name": "XYZ Corp",
            "deletable": true,
            "supports_percentage_amounts": true,
            "responsible_for_employer_taxes": false,
            "responsible_for_employee_w2": false,
            "catch_up_type": "elective"
          }
        },
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "enrollment_count": {
            "type": "integer",
            "description": "The number of employees enrolled in the benefit, only returned when enrollment_count query param is set to true.",
            "readOnly": true
          },
          "company_uuid": {
            "type": "string",
            "description": "The UUID of the company.",
            "readOnly": true
          },
          "uuid": {
            "type": "string",
            "description": "The UUID of the company benefit.",
            "readOnly": true
          },
          "benefit_type": {
            "type": "integer",
            "description": "The type of the benefit to which the company benefit belongs.",
            "readOnly": true
          },
          "active": {
            "type": "boolean",
            "default": true,
            "description": "Whether this benefit is active for employee participation. Company benefits may only be deactivated if no employees are actively participating."
          },
          "description": {
            "type": "string",
            "minLength": 1,
            "description": "The description of the company benefit. For example, a company may offer multiple benefits with an ID of 1 (for Medical Insurance). The description would show something more specific like “Kaiser Permanente” or “Blue Cross/ Blue Shield”."
          },
          "source": {
            "type": "string",
            "enum": [
              "internal",
              "external",
              "partnered"
            ],
            "description": "The source of the company benefit. This can be \"internal\", \"external\", or \"partnered\". Company benefits created via the API default to \"external\". Certain partners can create company benefits with a source of \"partnered\".",
            "readOnly": true
          },
          "partner_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The partner name of the partner that created the company benefit. For example, \"XYZ Corp\".",
            "readOnly": true
          },
          "deletable": {
            "type": "boolean",
            "description": "Whether this company benefit can be deleted. Deletable will be set to true if the benefit has not been used in payroll, has no employee benefits associated, and the benefit is not owned by Gusto or a Partner"
          },
          "supports_percentage_amounts": {
            "type": "boolean",
            "description": "Whether employee deductions and company contributions can be set as percentages of payroll for an individual employee. This is determined by the type of benefit and is not configurable by the company.",
            "readOnly": true
          },
          "responsible_for_employer_taxes": {
            "type": "boolean",
            "description": "Whether the employer is subject to pay employer taxes when an employee is on leave. Only applicable to third party sick pay benefits."
          },
          "responsible_for_employee_w2": {
            "type": "boolean",
            "description": "Whether the employer is subject to file W-2 forms for an employee on leave. Only applicable to third party sick pay benefits."
          },
          "catch_up_type": {
            "description": "The type of catch-up contribution for this benefit, as required by Section 603 of the SECURE 2.0 Act. Only applicable to pre-tax 401(k) and 403(b) benefits.",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "elective",
                  "deemed"
                ]
              },
              {
                "type": "null"
              }
            ]
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
    "/v1/companies/{company_id}/company_benefits": {
      "get": {
        "summary": "Get benefits for a company",
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
            "name": "active",
            "in": "query",
            "required": false,
            "description": "Whether the benefit is currently active",
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "enrollment_count",
            "in": "query",
            "required": false,
            "description": "Whether to return employee enrollment count",
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "benefit_type",
            "in": "query",
            "required": false,
            "description": "Filter by benefit type. Comma-separated list of benefit type IDs, i.e. `?benefit_type=5,105`",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-company_benefits",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Company benefits represent the benefits that a company is offering to employees. This ties together a particular supported benefit with the company-specific information for the offering of that benefit.\n\nNote that company benefits can be deactivated only when no employees are enrolled.\n\nBenefits containing PHI are only visible to applications with the `company_benefits:read:phi` scope.\n\nscope: `company_benefits:read`",
        "tags": [
          "Company Benefits"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Example response",
            "content": {
              "application/json": {
                "examples": {
                  "Example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Company-Benefit/x-examples/Example"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Company-Benefit"
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
