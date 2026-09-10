---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get pay schedule assignments for a company

This endpoint returns the current pay schedule assignment for a company, with pay schedule and employee/department mappings depending on the pay schedule type.

scope: `pay_schedules:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Pay Schedules"
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
      "Pay-Schedule-Assignment": {
        "description": "The representation of a pay schedule assignment.",
        "type": "object",
        "x-examples": {
          "example": {
            "type": "by_employee",
            "employees": [
              {
                "employee_uuid": "f0238368-f2cf-43e2-9a07-b0265f2cec69",
                "pay_schedule_uuid": "c277ac52-9871-4a96-a1e6-0c449684602a"
              }
            ]
          }
        },
        "properties": {
          "type": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "single",
                  "hourly_salaried",
                  "by_employee",
                  "by_department"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The pay schedule assignment type.",
            "readOnly": true
          },
          "hourly_pay_schedule_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "Pay schedule for hourly employees.",
            "readOnly": true
          },
          "salaried_pay_schedule_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "Pay schedule for salaried employees.",
            "readOnly": true
          },
          "default_pay_schedule_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "Default pay schedule for employees.",
            "readOnly": true
          },
          "employees": {
            "type": [
              "array",
              "null"
            ],
            "description": "List of employees and their pay schedules.",
            "readOnly": true,
            "items": {
              "$ref": "#/components/schemas/Pay-Schedule-Assignment-Employee"
            }
          },
          "departments": {
            "type": [
              "array",
              "null"
            ],
            "description": "List of departments and their pay schedules.",
            "readOnly": true,
            "items": {
              "$ref": "#/components/schemas/Pay-Schedule-Assignment-Department"
            }
          }
        },
        "x-tags": [
          "Pay Schedules"
        ]
      },
      "Pay-Schedule-Assignment-Employee": {
        "type": "object",
        "x-examples": {
          "example-1": {
            "employee_uuid": "43b39ada-dc49-4879-9594-fe95f67ae434",
            "pay_schedule_uuid": "3f029a58-155d-4c30-8361-cc266b2c1f11"
          }
        },
        "properties": {
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee."
          },
          "pay_schedule_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The employee's pay schedule UUID."
          }
        },
        "x-tags": [
          "Pay Schedules"
        ]
      },
      "Pay-Schedule-Assignment-Department": {
        "type": "object",
        "x-examples": {
          "example-1": {
            "department_uuid": "43b39ada-dc49-4879-9594-fe95f67ae434",
            "pay_schedule_uuid": "3f029a58-155d-4c30-8361-cc266b2c1f11"
          }
        },
        "properties": {
          "department_uuid": {
            "type": "string",
            "description": "The UUID of the department."
          },
          "pay_schedule_uuid": {
            "type": "string",
            "description": "The department's pay schedule UUID."
          }
        },
        "x-tags": [
          "Pay Schedules"
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
    "/v1/companies/{company_id}/pay_schedules/assignments": {
      "get": {
        "summary": "Get pay schedule assignments for a company",
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
        "operationId": "get-v1-companies-company_id-pay_schedules-assignments",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "This endpoint returns the current pay schedule assignment for a company, with pay schedule and employee/department mappings depending on the pay schedule type.\n\nscope: `pay_schedules:read`",
        "tags": [
          "Pay Schedules"
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
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Pay-Schedule-Assignment/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Pay-Schedule-Assignment"
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
