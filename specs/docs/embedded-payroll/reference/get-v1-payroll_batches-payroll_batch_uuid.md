---
updatedAt: 2026-07-01T17:08:13.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a payroll cancellation batch

Returns the status and per-payroll results of a payroll cancellation batch.

Poll this endpoint until the batch `status` reaches a terminal value (`completed` or `failed`). Once terminal, the response includes the `results` array (one entry per authorized payroll, each with its own per-payroll `status` — `success` or `failed`) and the `exclusions` array (one entry per payroll that could not be processed). A cancel is atomic, so a per-payroll result is only ever `success` or `failed` — never `partial_success`.

Note that the top-level batch `status` (`pending` / `processing` / `completed` / `failed`) is the request lifecycle, distinct from the per-payroll `status` inside `results[]`. A `completed` batch does not imply every payroll was cancelled — inspect the array for per-payroll outcomes.

Results are stored in Redis with a limited TTL after completion. If the partner polls after results have expired, this endpoint returns 410 Gone — partners should re-submit a new batch.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `payroll_batches:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Payroll Cancellations"
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
      "Payroll-Batch-Results": {
        "type": "object",
        "description": "A payroll cancellation batch with per-payroll results.",
        "x-examples": {
          "success_status": {
            "uuid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "idempotency_key": "80a74f8b-2c16-45e5-9038-aa108849c6e6",
            "status": "completed",
            "submitted_at": "2026-04-01T14:30:00Z",
            "completed_at": "2026-04-01T14:30:09Z",
            "submitted_items": 4,
            "processed_items": 2,
            "excluded_items": 2,
            "results": [
              {
                "idx": 0,
                "uuid": "11111111-2222-3333-4444-555555555555",
                "status": "success"
              },
              {
                "idx": 1,
                "uuid": "66666666-7777-8888-9999-000000000000",
                "status": "failed",
                "errors": [
                  {
                    "error_key": "base",
                    "category": "not_cancellable",
                    "message": "Payroll cannot be canceled"
                  }
                ]
              }
            ],
            "exclusions": [
              {
                "idx": 2,
                "entity_type": "payroll",
                "uuid": "11111111-2222-3333-4444-555555555555",
                "company_uuid": "cccccccc-1111-2222-3333-444444444444",
                "status": "failed",
                "category": "duplicate_operation",
                "message": "Duplicate UUID. Only the first occurrence is processed."
              },
              {
                "idx": 3,
                "entity_type": "payroll",
                "uuid": "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                "company_uuid": "dddddddd-1111-2222-3333-444444444444",
                "status": "failed",
                "category": "not_found",
                "message": "Payroll not found or not associated with this partner"
              }
            ]
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "format": "uuid",
            "description": "The unique identifier of the payroll cancellation batch.",
            "readOnly": true
          },
          "idempotency_key": {
            "type": "string",
            "format": "uuid",
            "description": "The idempotency key provided when creating the batch."
          },
          "status": {
            "type": "string",
            "enum": [
              "pending",
              "processing",
              "completed",
              "failed"
            ],
            "description": "The lifecycle status of the batch request itself. Terminal values are `completed` (processing finished — inspect `results` and `exclusions` for per-payroll outcomes) and `failed` (the batch crashed at the system level; can be retried). This is distinct from the per-payroll `status` returned inside `results[]`. A `completed` batch does not imply every payroll was cancelled."
          },
          "submitted_at": {
            "type": "string",
            "format": "date-time",
            "description": "The timestamp when the batch was submitted."
          },
          "completed_at": {
            "type": [
              "string",
              "null"
            ],
            "format": "date-time",
            "description": "The timestamp when the batch processing completed."
          },
          "submitted_items": {
            "type": [
              "integer",
              "null"
            ],
            "description": "The number of payrolls submitted in the batch."
          },
          "processed_items": {
            "type": "integer",
            "description": "The number of payrolls processed (cancelled or attempted). Only present once the batch reaches a terminal status."
          },
          "excluded_items": {
            "type": "integer",
            "description": "The number of payrolls excluded from processing. Only present once the batch reaches a terminal status."
          },
          "results": {
            "type": "array",
            "description": "Per-payroll cancellation results. Only present once the batch reaches a terminal status. One entry per authorized payroll.",
            "items": {
              "type": "object",
              "properties": {
                "idx": {
                  "type": "integer",
                  "description": "The index of this payroll in the original POST batch array."
                },
                "uuid": {
                  "type": "string",
                  "format": "uuid",
                  "description": "The UUID of the payroll."
                },
                "status": {
                  "type": "string",
                  "enum": [
                    "success",
                    "failed"
                  ],
                  "description": "The outcome of cancelling this payroll. A cancel is atomic — there is no per-payroll `partial_success`.\n- `success`: the payroll was cancelled, or required no action (already cancelled / never run)\n- `failed`: the payroll could not be cancelled; see `errors`\n"
                },
                "errors": {
                  "type": "array",
                  "description": "Present only when `status` is `failed`. A cancel is a single atomic operation, so this is a flat array with exactly one error.",
                  "items": {
                    "type": "object",
                    "properties": {
                      "error_key": {
                        "type": "string",
                        "description": "The key identifying the error source."
                      },
                      "category": {
                        "type": "string",
                        "enum": [
                          "not_cancellable",
                          "internal_error"
                        ],
                        "description": "Machine-readable reason the cancellation failed.\n- `not_cancellable`: the payroll is past the point where it can be cancelled\n- `internal_error`: an unexpected error occurred; the request can be retried\n"
                      },
                      "message": {
                        "type": "string",
                        "description": "Human-readable explanation of the failure."
                      }
                    }
                  }
                }
              }
            }
          },
          "exclusions": {
            "type": "array",
            "description": "Payrolls that could not be processed, determined at submission time. Only present once the batch reaches a terminal status. Every UUID submitted in the POST batch appears in exactly one of `results` or `exclusions`.",
            "items": {
              "type": "object",
              "properties": {
                "idx": {
                  "type": "integer",
                  "description": "The index of this payroll in the original POST batch array."
                },
                "entity_type": {
                  "type": "string",
                  "enum": [
                    "payroll"
                  ],
                  "description": "The type of entity this exclusion represents."
                },
                "uuid": {
                  "type": "string",
                  "format": "uuid",
                  "description": "The UUID of the excluded payroll."
                },
                "company_uuid": {
                  "type": "string",
                  "format": "uuid",
                  "description": "The UUID of the company asserted to own the payroll."
                },
                "status": {
                  "type": "string",
                  "enum": [
                    "failed"
                  ],
                  "description": "Always `failed` for an excluded payroll."
                },
                "category": {
                  "type": "string",
                  "enum": [
                    "not_found",
                    "duplicate_operation"
                  ],
                  "description": "Machine-readable category for why the payroll was excluded.\n- `not_found`: the payroll does not exist, or is not associated with a company the partner is mapped to\n- `duplicate_operation`: the same payroll UUID appeared more than once in the request; only the first occurrence is processed\n"
                },
                "message": {
                  "type": "string",
                  "description": "Human-readable explanation for the exclusion."
                }
              }
            }
          }
        },
        "required": [
          "uuid",
          "idempotency_key",
          "status",
          "submitted_at"
        ]
      }
    },
    "securitySchemes": {
      "CompanyAccessAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "Company-level authentication"
      },
      "SystemAccessAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "System-level authentication"
      }
    }
  },
  "paths": {
    "/v1/payroll_batches/{payroll_batch_uuid}": {
      "get": {
        "summary": "Get a payroll cancellation batch",
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
            "name": "payroll_batch_uuid",
            "in": "path",
            "description": "The UUID of the payroll cancellation batch returned by `POST /v1/payroll_batches`.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-payroll_batches-payroll_batch_uuid",
        "security": [
          {
            "SystemAccessAuth": []
          }
        ],
        "description": "Returns the status and per-payroll results of a payroll cancellation batch.\n\nPoll this endpoint until the batch `status` reaches a terminal value (`completed` or `failed`). Once terminal, the response includes the `results` array (one entry per authorized payroll, each with its own per-payroll `status` — `success` or `failed`) and the `exclusions` array (one entry per payroll that could not be processed). A cancel is atomic, so a per-payroll result is only ever `success` or `failed` — never `partial_success`.\n\nNote that the top-level batch `status` (`pending` / `processing` / `completed` / `failed`) is the request lifecycle, distinct from the per-payroll `status` inside `results[]`. A `completed` batch does not imply every payroll was cancelled — inspect the array for per-payroll outcomes.\n\nResults are stored in Redis with a limited TTL after completion. If the partner polls after results have expired, this endpoint returns 410 Gone — partners should re-submit a new batch.\n\n📘 System Access Authentication\n\nThis endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)\n\nscope: `payroll_batches:read`",
        "tags": [
          "Payroll Cancellations"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Batch-Results/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payroll-Batch-Results"
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
          },
          "410": {
            "description": "Gone - results have expired from Redis",
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
