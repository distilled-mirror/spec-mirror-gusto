---
updatedAt: 2026-07-02T23:26:20.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all time off policies for a company

Get all time off policies for a company

scope: `time_off_policies:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Time Off Policies"
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
      "Time-Off-Policy": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "uuid": "3f746cd0-dd08-408f-b712-8180c7c621e9",
            "company_uuid": "de83cff2-8e7a-448e-a28c-14258a9971c3",
            "name": "test policy",
            "policy_type": "vacation",
            "accrual_method": "per_hour_worked",
            "accrual_rate": "40.0",
            "accrual_rate_unit": "40.0",
            "paid_out_on_termination": true,
            "accrual_waiting_period_days": 10,
            "carryover_limit_hours": "100.0",
            "max_accrual_hours_per_year": "100.0",
            "max_hours": "100.0",
            "complete": true,
            "version": "f5556bce3d75ec2b62bd11990aa7993a",
            "is_active": true,
            "policy_reset_date": "01-01",
            "employees": [
              {
                "uuid": "c61d1895-5cf8-4217-88c8-20d7c3132a04",
                "balance": "40.0"
              },
              {
                "uuid": "3633ce57-abb7-422f-8c5a-455566618e6a",
                "balance": "20.0"
              }
            ]
          },
          "success_status_no_employees": {
            "uuid": "3f746cd0-dd08-408f-b712-8180c7c621e9",
            "company_uuid": "de83cff2-8e7a-448e-a28c-14258a9971c3",
            "name": "test policy",
            "policy_type": "vacation",
            "accrual_method": "per_hour_worked",
            "accrual_rate": "40.0",
            "accrual_rate_unit": "40.0",
            "paid_out_on_termination": true,
            "accrual_waiting_period_days": 10,
            "carryover_limit_hours": "100.0",
            "max_accrual_hours_per_year": "100.0",
            "max_hours": "100.0",
            "complete": true,
            "version": "f5556bce3d75ec2b62bd11990aa7993a",
            "is_active": true,
            "policy_reset_date": "01-01",
            "employees": []
          },
          "deactivated_status": {
            "uuid": "3f746cd0-dd08-408f-b712-8180c7c621e9",
            "company_uuid": "de83cff2-8e7a-448e-a28c-14258a9971c3",
            "name": "test policy",
            "policy_type": "vacation",
            "accrual_method": "per_hour_worked",
            "accrual_rate": "40.0",
            "accrual_rate_unit": "40.0",
            "paid_out_on_termination": true,
            "accrual_waiting_period_days": 10,
            "carryover_limit_hours": "100.0",
            "max_accrual_hours_per_year": "100.0",
            "max_hours": "100.0",
            "complete": true,
            "version": null,
            "is_active": false,
            "policy_reset_date": "01-01",
            "employees": []
          }
        },
        "description": "Representation of a Time Off Policy",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of a time off policy"
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier for the company owning the time off policy"
          },
          "name": {
            "type": "string",
            "description": "Name of the time off policy"
          },
          "policy_type": {
            "type": "string",
            "description": "Type of the time off policy. Only \"vacation\" and \"sick\" can be created through the API, but other types may be present if the company was previously a Gusto.com customer.",
            "enum": [
              "vacation",
              "sick",
              "bereavement",
              "custom",
              "floating_holiday",
              "jury_duty",
              "learning_and_development",
              "parental_leave",
              "personal_day",
              "volunteer",
              "weather"
            ]
          },
          "accrual_method": {
            "type": "string",
            "description": "Policy time off accrual method"
          },
          "accrual_rate": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "description": "The rate at which the time off hours will accrue for an employee on the policy. Represented as a float, e.g. \"40.0\"."
          },
          "accrual_rate_unit": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "description": "The number of hours an employee has to work or be paid for to accrue the number of hours set in the accrual rate. Only used for hourly policies (per_hour_paid, per_hour_paid_no_overtime, per_hour_work, per_hour_worked_no_overtime). Represented as a float, e.g. \"40.0\"."
          },
          "paid_out_on_termination": {
            "type": "boolean",
            "description": "Boolean representing if an employee's accrued time off hours will be paid out on termination"
          },
          "accrual_waiting_period_days": {
            "type": [
              "integer",
              "null"
            ],
            "description": "Number of days before an employee on the policy will begin accruing time off hours"
          },
          "carryover_limit_hours": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "description": "The max number of hours an employee can carryover from one year to the next"
          },
          "max_accrual_hours_per_year": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "description": "The max number of hours an employee can accrue in a year"
          },
          "max_hours": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "description": "The max number of hours an employee can accrue"
          },
          "policy_reset_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "The date the policy resets. Format MM-DD"
          },
          "complete": {
            "type": "boolean",
            "description": "boolean representing if a policy has completed configuration"
          },
          "version": {
            "type": [
              "string",
              "null"
            ],
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/versioning#object-layer) for information on how to use this field. The version will be null if the policy is no longer active."
          },
          "is_active": {
            "type": "boolean",
            "description": "boolean representing if a policy is active or not"
          },
          "employees": {
            "type": "array",
            "description": "List of employee UUIDs under a time off policy",
            "items": {
              "type": "object",
              "properties": {
                "uuid": {
                  "type": "string"
                },
                "balance": {
                  "type": "string",
                  "description": "The time off balance for the employee"
                }
              }
            }
          }
        },
        "required": [
          "uuid",
          "company_uuid",
          "name",
          "policy_type",
          "accrual_method",
          "is_active",
          "employees"
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
    "/v1/companies/{company_uuid}/time_off_policies": {
      "get": {
        "summary": "Get all time off policies for a company",
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
            "name": "company_uuid",
            "in": "path",
            "description": "The UUID of the company",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_uuid-time_off_policies",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get all time off policies for a company\n\nscope: `time_off_policies:read`",
        "tags": [
          "Time Off Policies"
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
                    "value": [
                      {
                        "$ref": "#/components/schemas/Time-Off-Policy/x-examples/success_status"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Time-Off-Policy"
                  }
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
