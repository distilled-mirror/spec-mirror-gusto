---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a salary estimate

Retrieve a salary estimate by its UUID. Returns the estimated salary calculation along with all occupation details, revenue, and location information.

scope: `salary_estimates:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Salary Estimates"
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
      "Salary-Estimate": {
        "type": "object",
        "description": "A salary estimate calculation for an S-Corp owner based on occupation, experience level, location, and business revenue.",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the salary estimate.",
            "readOnly": true
          },
          "employee_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the employee this salary estimate is for.",
            "readOnly": true
          },
          "employee_job_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the employee job this salary estimate is associated with (once accepted).",
            "readOnly": true
          },
          "annual_net_revenue": {
            "type": [
              "string",
              "null"
            ],
            "description": "The annual net revenue of the business used for salary calculations."
          },
          "zip_code": {
            "type": [
              "string",
              "null"
            ],
            "description": "The ZIP code used for location-based salary calculations.",
            "pattern": "^\\d{5}$"
          },
          "result": {
            "type": [
              "integer",
              "null"
            ],
            "description": "The calculated reasonable salary estimate in cents. Null if not yet calculated.",
            "readOnly": true
          },
          "accepted_at": {
            "type": [
              "string",
              "null"
            ],
            "format": "date-time",
            "description": "The timestamp when this salary estimate was accepted and finalized.",
            "readOnly": true
          },
          "created_at": {
            "type": "string",
            "format": "date-time",
            "description": "The timestamp when this salary estimate was created.",
            "readOnly": true
          },
          "updated_at": {
            "type": "string",
            "format": "date-time",
            "description": "The timestamp when this salary estimate was last updated.",
            "readOnly": true
          },
          "occupations": {
            "type": "array",
            "description": "Array of occupations with their experience levels and time allocations.",
            "items": {
              "type": "object",
              "properties": {
                "code": {
                  "type": "string",
                  "description": "Bureau of Labor Statistics (BLS) occupation code."
                },
                "name": {
                  "type": "string",
                  "description": "Occupation name."
                },
                "description": {
                  "type": "string",
                  "description": "Occupation description."
                },
                "experience_level": {
                  "type": "string",
                  "description": "Experience level for this occupation.",
                  "enum": [
                    "novice",
                    "intermediate",
                    "average",
                    "skilled",
                    "expert"
                  ]
                },
                "time_percentage": {
                  "type": "string",
                  "description": "Percentage of time spent in this occupation (as decimal string, 0-1)."
                },
                "primary": {
                  "type": "boolean",
                  "description": "Whether this is the primary occupation."
                }
              },
              "required": [
                "code",
                "experience_level",
                "time_percentage"
              ]
            }
          }
        },
        "required": [
          "uuid",
          "employee_uuid",
          "annual_net_revenue",
          "zip_code",
          "created_at",
          "updated_at",
          "occupations"
        ],
        "x-examples": {
          "success_status": {
            "uuid": "7f5d3d93-6d6f-48c0-9f4e-cd12c2d3e4b2",
            "employee_uuid": "8c290660-b6c9-4ad7-9f6e-ea146aaf79e8",
            "employee_job_uuid": null,
            "annual_net_revenue": "500000",
            "zip_code": "94107",
            "result": 12000000,
            "accepted_at": null,
            "created_at": "2025-01-15T10:30:00.000-08:00",
            "updated_at": "2025-01-15T10:30:00.000-08:00",
            "occupations": [
              {
                "code": "15-1252",
                "name": "Software Developers, Systems Software",
                "description": "Research, design, develop, and test operating systems-level software.",
                "experience_level": "skilled",
                "time_percentage": "1.0",
                "primary": true
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
    "/v1/salary_estimates/{uuid}": {
      "get": {
        "summary": "Get a salary estimate",
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
            "name": "uuid",
            "in": "path",
            "required": true,
            "description": "The UUID of the salary estimate",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-salary_estimates-id",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieve a salary estimate by its UUID. Returns the estimated salary calculation along with all occupation details, revenue, and location information.\n\nscope: `salary_estimates:read`",
        "tags": [
          "Salary Estimates"
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
                      "$ref": "#/components/schemas/Salary-Estimate/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Salary-Estimate"
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
