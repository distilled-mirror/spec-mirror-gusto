---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all time sheets for a company

Fetch all company's time sheets.

Time sheets represent the time worked by an employee or contractor for a given time range.
Hours are classified by pay classification, and can be regular, overtime, or double overtime.

scope: `time_sheet:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Time Tracking"
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
      "Time-Sheet": {
        "type": "object",
        "x-examples": {
          "example": {
            "uuid": "123e4567-e89b-12d3-a456-426655440000",
            "company_uuid": "123e4567-e89b-12d3-a456-426655440000",
            "status": "approved",
            "time_zone": "America/Los_Angeles",
            "entity_type": "Employee",
            "version": "72deb67e16f7b92713c00d3582fa6c68",
            "job_uuid": "123e4567-e89b-12d3-a456-426655440000",
            "entity_uuid": "123e4567-e89b-12d3-a456-426655440000",
            "shift_started_at": "2025-03-04T13:07:10Z",
            "shift_ended_at": "2025-03-04T16:07:10Z",
            "created_at": "2025-04-29T16:08:53Z",
            "updated_at": "2025-04-29T16:08:53Z",
            "metadata": {},
            "entries": [
              {
                "uuid": "123e4567-e89b-12d3-a456-426655440000",
                "hours_worked": "1.000",
                "pay_classification": "Regular"
              },
              {
                "uuid": "123e4567-e89b-12d3-a456-426655440000",
                "hours_worked": "1.000",
                "pay_classification": "Overtime"
              },
              {
                "uuid": "123e4567-e89b-12d3-a456-426655440000",
                "hours_worked": "1.000",
                "pay_classification": "Double overtime"
              }
            ]
          }
        },
        "description": "Record representing an employee/contractor's time sheet",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of the time sheet."
          },
          "status": {
            "type": "string",
            "description": "Status of the time sheet.",
            "enum": [
              "pending",
              "rejected",
              "approved"
            ]
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company to which the time sheet belongs."
          },
          "time_zone": {
            "type": "string",
            "description": "Time zone of where the time was tracked."
          },
          "entity_type": {
            "type": "string",
            "description": "Type of entity associated with the time sheet.",
            "enum": [
              "Employee",
              "Contractor"
            ]
          },
          "entity_uuid": {
            "type": "string",
            "description": "Unique identifier of the entity associated with the time sheet."
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/app-integrations/docs/idempotency) for information on how to use this field."
          },
          "job_uuid": {
            "type": "string",
            "description": "Unique identifier of the job for which time was reported."
          },
          "shift_started_at": {
            "type": "string",
            "format": "date-time",
            "description": "The start time of the shift."
          },
          "shift_ended_at": {
            "type": "string",
            "format": "date-time",
            "description": "The end time of the shift. If the shift is still ongoing this field will be null."
          },
          "created_at": {
            "type": "string",
            "format": "date-time",
            "description": "Datetime for when time sheet was created."
          },
          "updated_at": {
            "type": "string",
            "format": "date-time",
            "description": "Datetime for when time sheet was updated."
          },
          "synced_to_payroll_at": {
            "type": [
              "string",
              "null"
            ],
            "format": "date-time",
            "description": "Datetime for when time sheet was synced to payroll. Null if the time sheet has not yet been synced to payroll."
          },
          "metadata": {
            "type": "object",
            "additionalProperties": {
              "type": "string",
              "maxLength": 500
            },
            "propertyNames": {
              "type": "string",
              "maxLength": 40
            },
            "maxProperties": 50,
            "description": "Metadata associated with the time sheet. Key-value pairs of arbitrary data. Both keys and values must be strings."
          },
          "entries": {
            "type": "array",
            "description": "Entries associated with the time sheet.",
            "items": {
              "type": "object",
              "properties": {
                "uuid": {
                  "type": "string",
                  "description": "Unique identifier of the entry."
                },
                "hours_worked": {
                  "type": "string",
                  "format": "float",
                  "description": "Hours worked for this pay classification. Represented as a string, e.g. \"1.500\"."
                },
                "pay_classification": {
                  "type": "string",
                  "description": "Pay classification for the entry.",
                  "enum": [
                    "Regular",
                    "Overtime",
                    "Double overtime"
                  ]
                }
              }
            }
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
    "/v1/companies/{company_uuid}/time_tracking/time_sheets": {
      "get": {
        "summary": "Get all time sheets for a company",
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
            "required": true,
            "description": "The UUID of the company",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "entity_uuids",
            "in": "query",
            "required": false,
            "schema": {
              "type": "array",
              "items": {
                "type": "string"
              }
            },
            "description": "Entity UUIDs that reported time sheets"
          },
          {
            "name": "entity_type",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "Employee",
                "Contractor"
              ]
            },
            "description": "Type of entities to filter. One of: \"Employee\", \"Contractor\""
          },
          {
            "name": "status",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "approved",
                "pending",
                "rejected"
              ]
            },
            "description": "Status of time sheets. One of: \"approved\", \"pending\", \"rejected\""
          },
          {
            "name": "sort_by",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "created_at",
                "updated_at",
                "shift_started_at",
                "shift_ended_at"
              ]
            },
            "description": "Field to sort by. One of: \"created_at\", \"updated_at\", \"shift_started_at\", \"shift_ended_at\""
          },
          {
            "name": "sort_order",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            },
            "description": "Sorting order. One of: \"asc\", \"desc\""
          },
          {
            "name": "before",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string"
            },
            "description": "time sheets that were created before ISO 8601 timestamp. Filtering by \"created_at\""
          },
          {
            "name": "after",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string"
            },
            "description": "time sheets that were created after ISO 8601 timestamp. Filtering by \"created_at\""
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
        "operationId": "get-companies-company_uuid-time_tracking-time_sheets",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetch all company's time sheets.\n\nTime sheets represent the time worked by an employee or contractor for a given time range.\nHours are classified by pay classification, and can be regular, overtime, or double overtime.\n\nscope: `time_sheet:read`",
        "tags": [
          "Time Tracking"
        ],
        "x-gusto-integration-type": [
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "examples": {
                  "example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Time-Sheet/x-examples/example"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Time-Sheet"
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
