---
updatedAt: 2026-05-26T23:06:58.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get time off requests for a company

Get all time off requests, past and present, for a company.

In order to reduce the number of time off requests returned in a single response, or to retrieve time off requests from a time period of interest, you may use the `start_date` and `end_date` parameters.

You may provide both or either parameters to scope the returned data. For example:

`?start_date=2019-01-01`

Returns all time off requests where the request start date is equal to or after January 1, 2019.

`?end_date=2019-01-01`

Returns all time off requests where the request end date is equal to or before January 1, 2019.

`?start_date=2019-05-01&end_date=2019-08-31`

Returns all time off requests where the request start date is equal to or after May 1, 2019 and the request end date is equal to or before August 31, 2019.

`scope: time_off_requests:read`

scope: `time_off_requests:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Time Off Requests"
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
      "Time-Off-Request": {
        "type": "object",
        "description": "The representation of a time off request.",
        "x-examples": {
          "success_status": {
            "uuid": "9145390f-0431-45ee-b8a0-6e7a8850d4cf",
            "status": "approved",
            "employee_note": "Vacation at Disney World!",
            "employer_note": "But Universal has Harry Potter World...",
            "days": {
              "2019-06-01": "4.000",
              "2019-06-02": "8.000",
              "2019-06-03": "2.000"
            },
            "request_type": "vacation",
            "policy_type": "vacation",
            "policy_uuid": "ae382963-06b2-4b57-9780-8feda862bb70",
            "employee": {
              "uuid": "05f8663b-5944-4cfb-910e-1ee0a6df7b42",
              "full_name": "Jessica Gusto"
            },
            "approver": {
              "uuid": "21d8dff4-ce09-4120-a274-3a5628bf6769",
              "full_name": "Karen Gusto"
            },
            "initiator": {
              "uuid": "05f8663b-5944-4cfb-910e-1ee0a6df7b42",
              "full_name": "Jessica Gusto"
            }
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the time off request.",
            "readOnly": true
          },
          "status": {
            "type": "string",
            "description": "The status of the time off request.",
            "enum": [
              "pending",
              "approved",
              "declined",
              "consumed"
            ],
            "readOnly": true
          },
          "employee_note": {
            "type": "string",
            "description": "A note about the time off request, from the employee to the employer.",
            "readOnly": true
          },
          "employer_note": {
            "type": "string",
            "description": "A note about the time off request, from the employer to the employee.",
            "readOnly": true
          },
          "request_type": {
            "type": "string",
            "description": "The type of time off request.",
            "deprecated": true,
            "enum": [
              "vacation",
              "sick"
            ],
            "readOnly": true
          },
          "policy_type": {
            "type": "string",
            "description": "The type of the time off policy (e.g. vacation, sick).",
            "readOnly": true
          },
          "policy_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the time off policy associated with this request.",
            "readOnly": true
          },
          "days": {
            "description": "An object that represents the days in the time off request. The keys of the object are the dates, formatted as a YYYY-MM-DD string. The values of the object are the number of hours requested off for each day, formatted as a string representation of a numeric decimal to the thousands place.",
            "type": "object",
            "readOnly": true
          },
          "employee": {
            "type": "object",
            "description": "",
            "properties": {
              "uuid": {
                "type": "string",
                "description": "The UUID of the employee the time off request is for.",
                "readOnly": true
              },
              "full_name": {
                "type": "string",
                "description": "The full name of the employee the time off request is for.",
                "readOnly": true
              }
            },
            "readOnly": true
          },
          "initiator": {
            "type": [
              "object",
              "null"
            ],
            "description": "",
            "properties": {
              "uuid": {
                "type": "string",
                "description": "The UUID of the employee who initiated the time off request.",
                "readOnly": true
              },
              "full_name": {
                "type": "string",
                "description": "The full name of the employee who initiated the time off request.",
                "readOnly": true
              }
            },
            "readOnly": true
          },
          "approver": {
            "type": [
              "object",
              "null"
            ],
            "description": "This value will be null if the request has not been approved.",
            "properties": {
              "uuid": {
                "type": "string",
                "description": "The UUID of the employee who approved the time off request.",
                "readOnly": true
              },
              "full_name": {
                "type": "string",
                "description": "The full name of the employee who approved the time off request.",
                "readOnly": true
              }
            },
            "readOnly": true
          }
        }
      },
      "Time-Off-Request-List": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Time-Off-Request"
        },
        "x-examples": {
          "success_status": [
            {
              "uuid": "9145390f-0431-45ee-b8a0-6e7a8850d4cf",
              "status": "approved",
              "employee_note": "Vacation at Disney World!",
              "employer_note": "But Universal has Harry Potter World...",
              "days": {
                "2019-06-01": "4.000",
                "2019-06-02": "8.000",
                "2019-06-03": "2.000"
              },
              "request_type": "vacation",
              "policy_type": "vacation",
              "policy_uuid": "ae382963-06b2-4b57-9780-8feda862bb70",
              "employee": {
                "uuid": "05f8663b-5944-4cfb-910e-1ee0a6df7b42",
                "full_name": "Jessica Gusto"
              },
              "approver": {
                "uuid": "21d8dff4-ce09-4120-a274-3a5628bf6769",
                "full_name": "Karen Gusto"
              },
              "initiator": {
                "uuid": "05f8663b-5944-4cfb-910e-1ee0a6df7b42",
                "full_name": "Jessica Gusto"
              }
            },
            {
              "uuid": "944cbbf4-8b13-4c45-babd-11ff13e17581",
              "status": "pending",
              "employee_note": "Coming down with the flu",
              "employer_note": "",
              "days": {
                "2019-02-01": "8.000"
              },
              "request_type": "sick",
              "policy_type": "sick",
              "policy_uuid": "bf493c7e-1a2d-4e5f-8c9a-3d7b6e4f2a1c",
              "employee": {
                "uuid": "c2236d10-959a-4bb9-a21d-e14c6df447b6",
                "full_name": "James Gusto"
              },
              "approver": null,
              "initiator": {
                "uuid": "c2236d10-959a-4bb9-a21d-e14c6df447b6",
                "full_name": "James Gusto"
              }
            }
          ]
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
    "/v1/companies/{company_id}/time_off_requests": {
      "get": {
        "summary": "Get time off requests for a company",
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
            "description": "The company UUID",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "start_date",
            "in": "query",
            "required": false,
            "description": "Filter time off requests starting on or after this date",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "end_date",
            "in": "query",
            "required": false,
            "description": "Filter time off requests ending on or before this date",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-time_off_requests",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get all time off requests, past and present, for a company.\n\nIn order to reduce the number of time off requests returned in a single response, or to retrieve time off requests from a time period of interest, you may use the `start_date` and `end_date` parameters.\n\nYou may provide both or either parameters to scope the returned data. For example:\n\n`?start_date=2019-01-01`\n\nReturns all time off requests where the request start date is equal to or after January 1, 2019.\n\n`?end_date=2019-01-01`\n\nReturns all time off requests where the request end date is equal to or before January 1, 2019.\n\n`?start_date=2019-05-01&end_date=2019-08-31`\n\nReturns all time off requests where the request start date is equal to or after May 1, 2019 and the request end date is equal to or before August 31, 2019.\n\n`scope: time_off_requests:read`\n\nscope: `time_off_requests:read`",
        "tags": [
          "Time Off Requests"
        ],
        "x-gusto-integration-type": [
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
                      "$ref": "#/components/schemas/Time-Off-Request-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Time-Off-Request-List"
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
