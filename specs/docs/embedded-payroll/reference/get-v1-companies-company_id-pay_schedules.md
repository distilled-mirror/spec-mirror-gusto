---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get the pay schedules for a company

Returns all pay schedules for a company. The pay schedule object captures the details of when employees work and when they should be paid. A company can have multiple pay schedules.

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
      "Pay-Schedule-Show": {
        "type": "object",
        "title": "Pay Schedule",
        "description": "Pay schedule returned from pay schedule endpoints (GET by ID, POST create, PUT update). Same fields as Pay-Schedule with a required `version` for [optimistic concurrency](https://docs.gusto.com/embedded-payroll/docs/api-fundamentals#optimistic-version-control).\n\nFor API version 2025-11-15 and later, responses use `auto_payroll`; earlier versions use `auto_pilot` for the same semantic.\n",
        "required": [
          "uuid",
          "version"
        ],
        "properties": {
          "uuid": {
            "$ref": "#/components/schemas/Pay-Schedule-Uuid"
          },
          "version": {
            "$ref": "#/components/schemas/Pay-Schedule-Version"
          },
          "frequency": {
            "$ref": "#/components/schemas/Pay-Schedule-Frequency"
          },
          "anchor_pay_date": {
            "$ref": "#/components/schemas/Pay-Schedule-Anchor-Pay-Date"
          },
          "anchor_end_of_pay_period": {
            "$ref": "#/components/schemas/Pay-Schedule-Anchor-End-Of-Pay-Period"
          },
          "day_1": {
            "$ref": "#/components/schemas/Pay-Schedule-Day-1"
          },
          "day_2": {
            "$ref": "#/components/schemas/Pay-Schedule-Day-2"
          },
          "name": {
            "$ref": "#/components/schemas/Pay-Schedule-Name"
          },
          "custom_name": {
            "$ref": "#/components/schemas/Pay-Schedule-Custom-Name"
          },
          "auto_payroll": {
            "$ref": "#/components/schemas/Pay-Schedule-Auto-Payroll"
          },
          "active": {
            "$ref": "#/components/schemas/Pay-Schedule-Active"
          },
          "auto_payroll_enablement_blockers": {
            "$ref": "#/components/schemas/Pay-Schedule-Auto-Payroll-Enablement-Blockers"
          }
        },
        "x-tags": [
          "Pay Schedules"
        ],
        "x-examples": {
          "Example": {
            "uuid": "f2a69c38-e2f9-4e31-b5c5-4754fc60a052",
            "version": "68934a3e9455fa72420237eb05902327",
            "frequency": "Twice per month",
            "anchor_pay_date": "2020-05-15",
            "anchor_end_of_pay_period": "2020-05-08",
            "day_1": 15,
            "day_2": 31,
            "name": "Engineering",
            "auto_payroll": false,
            "custom_name": "A new monthly pay schedule",
            "active": true,
            "auto_payroll_enablement_blockers": null
          },
          "success_status": {
            "uuid": "f2a69c38-e2f9-4e31-b5c5-4754fc60a052",
            "version": "68934a3e9455fa72420237eb05902327",
            "frequency": "Twice per month",
            "anchor_pay_date": "2022-09-01",
            "anchor_end_of_pay_period": "2022-08-18",
            "day_1": 1,
            "day_2": 15,
            "name": null,
            "custom_name": "every 1st and 15th of the month",
            "auto_payroll": true,
            "active": true,
            "auto_payroll_enablement_blockers": null
          }
        }
      },
      "Pay-Schedule-Show-Response": {
        "type": "array",
        "description": "List of pay schedules for a company, as returned from [GET /v1/companies/{company_id}/pay_schedules](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies-company_id-pay_schedules). Each entry matches Pay-Schedule-Show (includes `version`).\n",
        "items": {
          "$ref": "#/components/schemas/Pay-Schedule-Show"
        },
        "x-tags": [
          "Pay Schedules"
        ],
        "x-examples": {
          "success_status": [
            {
              "uuid": "f2a69c38-e2f9-4e31-b5c5-4754fc60a052",
              "version": "68934a3e9455fa72420237eb05902327",
              "frequency": "Monthly",
              "anchor_pay_date": "2022-12-11",
              "anchor_end_of_pay_period": "2022-11-13",
              "day_1": 11,
              "day_2": null,
              "name": null,
              "custom_name": "every 11th of the month",
              "auto_payroll": true,
              "active": true,
              "auto_payroll_enablement_blockers": null
            }
          ]
        }
      },
      "Pay-Schedule-Version": {
        "type": "string",
        "description": "The current version of the pay schedule. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/api-fundamentals#optimistic-version-control) for information on how to use this field for optimistic concurrency.",
        "readOnly": true
      },
      "Pay-Schedule-Auto-Payroll": {
        "type": "boolean",
        "description": "With automatic payroll enabled, payroll runs automatically one day before payroll deadlines. When false, payroll does not run automatically.\nReturned for API version 2025-11-15 and later; for earlier versions the response uses auto_pilot instead.\n",
        "readOnly": true
      },
      "Pay-Schedule-Auto-Payroll-Enablement-Blockers": {
        "type": [
          "array",
          "null"
        ],
        "description": "List of blockers preventing automatic payroll from being enabled. If automatic payroll is already enabled, this field is null.",
        "items": {
          "$ref": "#/components/schemas/Pay-Schedule-Auto-Payroll-Enablement-Blocker"
        }
      },
      "Pay-Schedule-Auto-Payroll-Enablement-Blocker": {
        "type": "object",
        "description": "A single blocker preventing Autopayroll enablement.",
        "properties": {
          "key": {
            "type": "string",
            "description": "The blocker type. Possible values: employees_not_on_direct_deposit, employees_not_salaried, missing_state_tax_requirements, missing_funding_method, one_day_ach_speed_not_supported, company_suspended, earned_fast_ach_not_met, hourly_employees_missing_default_hours."
          },
          "metadata": {
            "type": "object",
            "description": "Blocker-specific metadata (e.g. employee_uuids, states)."
          }
        }
      },
      "Pay-Schedule-Uuid": {
        "type": "string",
        "description": "The unique identifier of the pay schedule in Gusto.",
        "readOnly": true
      },
      "Pay-Schedule-Frequency": {
        "type": "string",
        "description": "The frequency that employees on this pay schedule are paid with Gusto.\n\nREAD-ONLY in responses. Possible values:\n\n- `Every week`: Employees are paid weekly.\n- `Every other week`: Employees are paid bi-weekly (every two weeks).\n- `Twice per month`: Employees are paid on two fixed days each month (e.g. 1st and 15th); use day_1 and day_2.\n- `Monthly`: Employees are paid once per month; use day_1 for the pay day.\n- `Quarterly`: Employees are paid every three months.\n- `Annually`: Employees are paid once per year.\n",
        "enum": [
          "Every week",
          "Every other week",
          "Twice per month",
          "Monthly",
          "Quarterly",
          "Annually"
        ],
        "readOnly": true
      },
      "Pay-Schedule-Anchor-Pay-Date": {
        "type": "string",
        "format": "date",
        "description": "The first date that employees on this pay schedule are paid with Gusto (ISO 8601 YYYY-MM-DD).",
        "readOnly": true
      },
      "Pay-Schedule-Anchor-End-Of-Pay-Period": {
        "type": "string",
        "format": "date",
        "description": "The last date of the first pay period. This can be the same date as the anchor pay date (ISO 8601 YYYY-MM-DD).",
        "readOnly": true
      },
      "Pay-Schedule-Day-1": {
        "type": [
          "integer",
          "null"
        ],
        "description": "An integer between 1 and 31 indicating the first day of the month that employees are paid. This field is only relevant for pay schedules with the \"Twice per month\" and \"Monthly\" frequencies. It will be null for pay schedules with other frequencies.\n",
        "readOnly": true
      },
      "Pay-Schedule-Day-2": {
        "type": [
          "integer",
          "null"
        ],
        "description": "An integer between 1 and 31 indicating the second day of the month that employees are paid. This field is the second pay date for pay schedules with the \"Twice per month\" frequency. For semi-monthly pay schedules, this field should be set to 31. For months shorter than 31 days, the second pay date is set to the last day of the month. It will be null for pay schedules with other frequencies.\n",
        "readOnly": true
      },
      "Pay-Schedule-Name": {
        "type": [
          "string",
          "null"
        ],
        "description": "This field will be hourly when the pay schedule is for hourly employees, salaried when the pay schedule is for salaried employees, the department name if pay schedule is by department, and null when the pay schedule is for all employees.",
        "readOnly": true
      },
      "Pay-Schedule-Custom-Name": {
        "type": "string",
        "description": "A custom name for a pay schedule; defaults to the pay frequency description when none was set by the partner.\n\nWhen the partner never set a custom name (or cleared it), this field contains the auto-generated description derived from frequency and pay days (e.g. \"every 1st and 15th of the month\", \"every Friday\"). When the partner set a custom name on create or update, this field contains that value.\n",
        "readOnly": true
      },
      "Pay-Schedule-Active": {
        "type": "boolean",
        "description": "Whether this pay schedule is associated with any employees. A pay schedule is inactive when it's unassigned.",
        "readOnly": true
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
    "/v1/companies/{company_id}/pay_schedules": {
      "get": {
        "summary": "Get the pay schedules for a company",
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
        "operationId": "get-v1-companies-company_id-pay_schedules",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns all pay schedules for a company. The pay schedule object captures the details of when employees work and when they should be paid. A company can have multiple pay schedules.\n\nscope: `pay_schedules:read`",
        "tags": [
          "Pay Schedules"
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
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Pay-Schedule-Show-Response/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Pay-Schedule-Show-Response"
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
