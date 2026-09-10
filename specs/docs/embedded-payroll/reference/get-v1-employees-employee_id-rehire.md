---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee rehire

Retrieve an employee's rehire, which contains information on when the employee returns to work.

scope: `employments:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employee Employments"
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
      "Rehire": {
        "type": "object",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/versioning#object-layer) for information on how to use this field."
          },
          "effective_date": {
            "type": "string",
            "description": "The day when the employee returns to work."
          },
          "file_new_hire_report": {
            "type": "boolean",
            "description": "The boolean flag indicating whether Gusto will file a new hire report for the employee."
          },
          "work_location_uuid": {
            "type": "string",
            "description": "The uuid of the employee's work location."
          },
          "employment_status": {
            "type": "string",
            "description": "The employee's employment status. Supplying an invalid option will set the employment_status to *not_set*.",
            "enum": [
              "part_time",
              "full_time",
              "part_time_eligible",
              "variable",
              "seasonal",
              "not_set"
            ]
          },
          "two_percent_shareholder": {
            "type": "boolean",
            "description": "Whether the employee is a two percent shareholder of the company. This field only applies to companies with an S-Corp entity type."
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee.",
            "readOnly": true
          },
          "active": {
            "type": "boolean",
            "description": "Whether the employee's rehire has gone into effect.",
            "readOnly": true
          }
        },
        "x-examples": {
          "example": {
            "version": "2e930d43acbdb241f8f14a2d531fa417",
            "employee_uuid": "8c290660-b6c9-4ad7-9f6e-ea146aaf79e8",
            "active": false,
            "effective_date": "2024-06-30",
            "employment_status": "seasonal",
            "file_new_hire_report": false,
            "work_location_uuid": "8cb87e2e-5b30-4c13-a4f4-bfffcbed1188",
            "two_percent_shareholder": false
          },
          "active_rehire": {
            "version": "7c930f42bcadb241f8f14a2d531fb528",
            "employee_uuid": "9d3b1770-c7d0-5be8-a07f-fb257bbg80f9",
            "active": true,
            "effective_date": "2024-01-15",
            "employment_status": "full_time",
            "file_new_hire_report": true,
            "work_location_uuid": "9dc98f3f-6c41-5d24-a5b5-c363687ebf29",
            "two_percent_shareholder": false
          },
          "created": {
            "version": "3a841e52dcbea351f9f25b3e642gb639",
            "employee_uuid": "8c290660-b6c9-4ad7-9f6e-ea146aaf79e8",
            "active": false,
            "effective_date": "2023-06-30",
            "employment_status": "full_time",
            "file_new_hire_report": true,
            "work_location_uuid": "b6ae9d93-d4b8-4119-8c96-dba595dd8c30",
            "two_percent_shareholder": false
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
    "/v1/employees/{employee_id}/rehire": {
      "get": {
        "summary": "Get an employee rehire",
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
            "name": "employee_id",
            "in": "path",
            "description": "The UUID of the employee",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employees-employee_id-rehire",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieve an employee's rehire, which contains information on when the employee returns to work.\n\nscope: `employments:read`",
        "tags": [
          "Employee Employments"
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
                      "$ref": "#/components/schemas/Rehire/x-examples/example"
                    }
                  },
                  "active_rehire": {
                    "value": {
                      "$ref": "#/components/schemas/Rehire/x-examples/active_rehire"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Rehire"
                }
              }
            }
          },
          "204": {
            "description": "No Content"
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
