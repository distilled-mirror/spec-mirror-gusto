---
updatedAt: 2026-04-20T21:25:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a payroll sync

Fetch a payroll sync.

A payroll sync represents the result of syncing approved time sheet data to payroll. Use this endpoint to check the status of a previously initiated sync.

scope: `payroll_syncs:read`

# OpenAPI definition

````json
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
      "Entity-Error-Object": {
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
            "description": "Specifies the type of error. The category provides error groupings and can be used to build custom error handling in your integration. If category is `nested_errors`, the object will contain a nested `errors` property with entity errors."
          },
          "message": {
            "type": "string",
            "description": "Provides details about the error - generally this message can be surfaced to an end user."
          },
          "metadata": {
            "type": "object",
            "description": "Contains relevant data to identify the resource in question when applicable. For example, to identify an entity `entity_type` and `entity_uuid` will be provided.",
            "oneOf": [
              {
                "$ref": "#/components/schemas/Metadata-With-Multiple-Entities"
              },
              {
                "$ref": "#/components/schemas/Metadata-With-One-Entity"
              }
            ]
          },
          "errors": {
            "type": "array",
            "description": "Will only exist if category is `nested_errors`. It is possible to have multiple levels of nested errors.",
            "items": {
              "type": "object",
              "properties": {
                "error_key": {
                  "type": "string",
                  "description": "Specifies where the error occurs. Typically this key identifies the attribute/parameter related to the error."
                },
                "category": {
                  "type": "string",
                  "description": "Specifies the type of error. The category provides error groupings and can be used to build custom error handling in your integration. If category is `nested_errors`, the object will contain a nested `errors` property with entity errors."
                },
                "message": {
                  "type": "string",
                  "description": "Provides details about the error - generally this message can be surfaced to an end user."
                },
                "metadata": {
                  "type": "object",
                  "description": "Contains relevant data to identify the resource in question when applicable. For example, to identify an entity `entity_type` and `entity_uuid` will be provided."
                }
              }
            }
          }
        }
      },
      "Metadata-With-One-Entity": {
        "type": "object",
        "description": "single entity",
        "additionalProperties": true,
        "properties": {
          "entity_type": {
            "type": "string",
            "description": "Name of the entity that the error corresponds to."
          },
          "entity_uuid": {
            "type": "string",
            "description": "Unique identifier for the entity."
          },
          "valid_from": {
            "type": [
              "string",
              "null"
            ]
          },
          "valid_up_to": {
            "type": [
              "string",
              "null"
            ]
          },
          "key": {
            "type": [
              "string",
              "null"
            ]
          },
          "state": {
            "type": [
              "string",
              "null"
            ]
          }
        }
      },
      "Metadata-With-Multiple-Entities": {
        "type": "object",
        "description": "multiple entities",
        "required": [
          "entities"
        ],
        "properties": {
          "entities": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Metadata-With-One-Entity"
            }
          }
        }
      },
      "Payroll-Sync": {
        "type": "object",
        "description": "Record representing the sync of time sheet data to payroll.",
        "properties": {
          "uuid": {
            "type": "string",
            "format": "uuid",
            "description": "Unique identifier of the payroll sync.",
            "example": "123e4567-e89b-12d3-a456-426655440000"
          },
          "company_uuid": {
            "type": "string",
            "format": "uuid",
            "description": "Unique identifier of the company to which the payroll sync belongs.",
            "example": "123e4567-e89b-12d3-a456-426655440001"
          },
          "status": {
            "type": "string",
            "readOnly": true,
            "enum": [
              "pending",
              "in_progress",
              "success",
              "failure",
              "partial_success"
            ],
            "description": "The current status of the payroll sync. READ-ONLY.\n\n## State Transitions\n```\npending ──────► in_progress ──────► success\n                            ├─────► failure\n                            └─────► partial_success\n```\n\n### Valid Transitions\n- `pending` → `in_progress`: Automatic when processing begins\n- `in_progress` → `success`: All time sheet data synced successfully\n- `in_progress` → `failure`: Sync failed entirely\n- `in_progress` → `partial_success`: Some members failed to sync\n",
            "example": "pending"
          },
          "kind": {
            "type": "string",
            "enum": [
              "regular"
            ],
            "description": "The kind of payroll sync.\n- `regular`: A regular payroll sync\n",
            "example": "regular"
          },
          "pay_schedule_uuid": {
            "type": "string",
            "format": "uuid",
            "description": "Unique identifier of the pay schedule associated with this sync.",
            "example": "123e4567-e89b-12d3-a456-426655440002"
          },
          "pay_period_start_date": {
            "type": "string",
            "format": "date",
            "description": "The start date of the pay period per ISO 8601 format.",
            "example": "2025-01-01"
          },
          "pay_period_end_date": {
            "type": "string",
            "format": "date",
            "description": "The end date of the pay period per ISO 8601 format.",
            "example": "2025-01-15"
          },
          "submitted_at": {
            "type": "string",
            "format": "date-time",
            "description": "Datetime for when the payroll sync was submitted.",
            "example": "2025-01-16T12:00:00Z"
          },
          "completed_at": {
            "type": [
              "string",
              "null"
            ],
            "format": "date-time",
            "description": "Datetime for when the payroll sync completed. Null if the sync is still in progress.",
            "example": "2025-01-16T13:00:00Z"
          },
          "errors": {
            "type": "array",
            "description": "Errors encountered during the sync, if any. Each error follows the standard entity error format.",
            "items": {
              "$ref": "#/components/schemas/Entity-Error-Object"
            }
          },
          "warnings": {
            "type": "array",
            "description": "Warnings encountered during the sync, if any.",
            "items": {
              "type": "string"
            }
          }
        },
        "x-examples": {
          "pending_sync": {
            "uuid": "123e4567-e89b-12d3-a456-426655440000",
            "company_uuid": "123e4567-e89b-12d3-a456-426655440001",
            "status": "pending",
            "kind": "regular",
            "pay_schedule_uuid": "123e4567-e89b-12d3-a456-426655440002",
            "pay_period_start_date": "2025-01-01",
            "pay_period_end_date": "2025-01-15",
            "submitted_at": "2025-01-16T12:00:00Z",
            "completed_at": null
          },
          "completed_sync": {
            "uuid": "123e4567-e89b-12d3-a456-426655440000",
            "company_uuid": "123e4567-e89b-12d3-a456-426655440001",
            "status": "success",
            "kind": "regular",
            "pay_schedule_uuid": "123e4567-e89b-12d3-a456-426655440002",
            "pay_period_start_date": "2025-01-01",
            "pay_period_end_date": "2025-01-15",
            "submitted_at": "2025-01-16T12:00:00Z",
            "completed_at": "2025-01-16T13:00:00Z"
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
    "/v1/time_tracking/payroll_syncs/{payroll_sync_uuid}": {
      "get": {
        "summary": "Get a payroll sync",
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
            "name": "payroll_sync_uuid",
            "in": "path",
            "description": "The UUID of the payroll sync",
            "example": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-time_tracking-payroll_syncs-payroll_sync_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetch a payroll sync.\n\nA payroll sync represents the result of syncing approved time sheet data to payroll. Use this endpoint to check the status of a previously initiated sync.\n\nscope: `payroll_syncs:read`",
        "tags": [
          "Time Tracking"
        ],
        "x-gusto-integration-type": [
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "completed_sync": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Sync/x-examples/completed_sync"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payroll-Sync"
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
````
