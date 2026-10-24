---
updatedAt: 2026-10-18T21:31:28.000Z
agentTools:
  siteIndex: https://docs.gusto.com/llms.txt
  projectIndex: https://docs.gusto.com/app-integrations/llms.txt
---

# Get a batch of time sheets

Fetch a batch of up to 500 time sheets.

When the batch is completed, `results` contains the outcome of each time sheet, matched by `external_id`.

scope: `time_sheet:read`

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
      "Time-Sheets-Batch-Item-Result": {
        "type": "object",
        "description": "The result of one time sheet in a batch.",
        "properties": {
          "external_id": {
            "type": "string",
            "description": "The `external_id` that you sent for this item."
          },
          "status": {
            "type": "string",
            "enum": [
              "pending",
              "success",
              "failed"
            ],
            "description": "Status of the item.\n- `pending`: The item is not processed yet.\n- `success`: The time sheet was created or updated.\n- `failed`: The time sheet was not created or updated. See `errors`.\n"
          },
          "uuid": {
            "type": "string",
            "description": "Unique identifier of the time sheet. Present only when `status` is `success`."
          },
          "version": {
            "type": "string",
            "description": "The current version of the time sheet. Present only when `status` is `success`. See the [versioning guide](https://docs.gusto.com/app-integrations/docs/idempotency) for information on how to use this field."
          },
          "errors": {
            "type": "array",
            "description": "The reasons why the item failed. Present only when `status` is `failed`.",
            "items": {
              "$ref": "#/components/schemas/Entity-Error-Object"
            }
          }
        },
        "x-examples": {
          "success": {
            "external_id": "shift-1001",
            "status": "success",
            "uuid": "123e4567-e89b-12d3-a456-426655440000",
            "version": "72deb67e16f7b92713c00d3582fa6c68"
          },
          "failed": {
            "external_id": "shift-1002",
            "status": "failed",
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Supplied Version 9a1f0c3e5b7d2e4f6a8c0b1d3e5f7a9c is invalid."
              }
            ]
          }
        }
      },
      "Time-Sheets-Batch": {
        "type": "object",
        "description": "A batch of time sheets that is created or updated asynchronously.",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of the batch."
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company to which the batch belongs."
          },
          "status": {
            "type": "string",
            "readOnly": true,
            "enum": [
              "pending",
              "processing",
              "success",
              "failed",
              "partial_success"
            ],
            "description": "Status of the batch. READ-ONLY.\n\n## State Transitions\n```\npending ──► processing ──┬──► success\n                         ├──► partial_success\n                         └──► failed\n```\n\n- `pending`: The batch is accepted and waits to be processed.\n- `processing`: The time sheets in the batch are being processed.\n- `success`: All time sheets were processed successfully.\n- `partial_success`: Some time sheets were processed successfully and some failed. See `results`.\n- `failed`: All time sheets failed. See `results`.\n"
          },
          "batch_type": {
            "type": "string",
            "enum": [
              "time_sheets_batch"
            ],
            "description": "Type of the batch."
          },
          "batch_action": {
            "type": "string",
            "enum": [
              "create",
              "update"
            ],
            "description": "The action applied to every time sheet in the batch."
          },
          "idempotency_key": {
            "type": "string",
            "description": "The idempotency key that you sent when you created the batch."
          },
          "submitted_items": {
            "type": "integer",
            "description": "Number of time sheets submitted in the batch."
          },
          "submitted_at": {
            "type": "string",
            "format": "date-time",
            "description": "Datetime for when the batch was submitted."
          },
          "completed_at": {
            "type": [
              "string",
              "null"
            ],
            "format": "date-time",
            "description": "Datetime for when the batch was completed. Null until the batch is completed."
          },
          "results": {
            "type": "array",
            "description": "The result of each time sheet in the batch. Empty until the batch is completed. The results do not include the time sheet body. Use [GET /v1/time_tracking/time_sheets/{time_sheet_uuid}](https://docs.gusto.com/app-integrations/reference/get-time_tracking-time_sheets-time_sheet_uuid) to fetch a time sheet.",
            "items": {
              "$ref": "#/components/schemas/Time-Sheets-Batch-Item-Result"
            }
          }
        },
        "x-examples": {
          "pending_batch": {
            "uuid": "0d4f8b3a-6c2e-4a1f-9b7d-5e3c1a2b4d6f",
            "company_uuid": "123e4567-e89b-12d3-a456-426655440000",
            "status": "pending",
            "submitted_items": 2,
            "batch_action": "create",
            "idempotency_key": "2f0c6a4e-8f3b-4d0e-9a51-6f1d2c7b9e10",
            "batch_type": "time_sheets_batch",
            "submitted_at": "2024-06-11T12:00:00Z",
            "completed_at": null,
            "results": []
          },
          "success_batch": {
            "uuid": "0d4f8b3a-6c2e-4a1f-9b7d-5e3c1a2b4d6f",
            "company_uuid": "123e4567-e89b-12d3-a456-426655440000",
            "status": "success",
            "submitted_items": 2,
            "batch_action": "create",
            "idempotency_key": "2f0c6a4e-8f3b-4d0e-9a51-6f1d2c7b9e10",
            "batch_type": "time_sheets_batch",
            "submitted_at": "2024-06-11T12:00:00Z",
            "completed_at": "2024-06-11T12:00:05Z",
            "results": [
              {
                "external_id": "shift-1001",
                "status": "success",
                "uuid": "123e4567-e89b-12d3-a456-426655440001",
                "version": "72deb67e16f7b92713c00d3582fa6c68"
              },
              {
                "external_id": "shift-1002",
                "status": "success",
                "uuid": "123e4567-e89b-12d3-a456-426655440002",
                "version": "9a1f0c3e5b7d2e4f6a8c0b1d3e5f7a9c"
              }
            ]
          },
          "partial_success_batch": {
            "uuid": "5a7c9e1b-3d5f-4a7c-9e1b-3d5f7a9c1e3b",
            "company_uuid": "123e4567-e89b-12d3-a456-426655440000",
            "status": "partial_success",
            "submitted_items": 2,
            "batch_action": "update",
            "idempotency_key": "7c9e2b1a-3d4f-4e5a-8b6c-1d2e3f4a5b6c",
            "batch_type": "time_sheets_batch",
            "submitted_at": "2024-06-11T12:00:00Z",
            "completed_at": "2024-06-11T12:00:05Z",
            "results": [
              {
                "external_id": "shift-1001",
                "status": "success",
                "uuid": "123e4567-e89b-12d3-a456-426655440001",
                "version": "3b5d7f9a1c3e5b7d9f1a3c5e7b9d1f3a"
              },
              {
                "external_id": "shift-1002",
                "status": "failed",
                "errors": [
                  {
                    "error_key": "uuid",
                    "category": "invalid_attribute_value",
                    "message": "Uuid not found"
                  }
                ]
              }
            ]
          }
        },
        "x-tags": [
          "Time Tracking"
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
    "/v1/time_tracking/time_sheets_batches/{time_sheets_batch_uuid}": {
      "get": {
        "summary": "Get a batch of time sheets",
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
            "name": "time_sheets_batch_uuid",
            "in": "path",
            "required": true,
            "description": "The UUID of the time sheets batch",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-time_tracking-time_sheets_batches-time_sheets_batch_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetch a batch of up to 500 time sheets.\n\nWhen the batch is completed, `results` contains the outcome of each time sheet, matched by `external_id`.\n\nscope: `time_sheet:read`",
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
                  "success_batch": {
                    "value": {
                      "$ref": "#/components/schemas/Time-Sheets-Batch/x-examples/success_batch"
                    }
                  },
                  "partial_success_batch": {
                    "value": {
                      "$ref": "#/components/schemas/Time-Sheets-Batch/x-examples/partial_success_batch"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Time-Sheets-Batch"
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
