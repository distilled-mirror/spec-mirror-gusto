---
updatedAt: 2026-04-20T21:24:14.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a people batch

Returns the status and results of a people batch.

Poll this endpoint to check the batch processing status and retrieve results.

scope: `people_batches:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "People Batches"
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
      "People-Batch-Results": {
        "type": "object",
        "description": "A people batch with processing results.",
        "x-examples": {
          "success_status": {
            "uuid": "f711ab7a-2d44-4556-b90c-9f883195f53a",
            "idempotency_key": "95d84feb-3a17-4c0b-a00b-bf8d3dec3326",
            "status": "pending",
            "submitted_at": "2026-03-02T15:09:50-08:00",
            "completed_at": null,
            "submitted_items": null,
            "processed_items": 0,
            "excluded_items": 0,
            "results": []
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "format": "uuid",
            "description": "The unique identifier of the people batch.",
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
              "failed",
              "partial_success"
            ],
            "description": "The current status of the batch processing."
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
            "description": "The number of items submitted in the batch."
          },
          "processed_items": {
            "type": "integer",
            "description": "The number of items successfully processed."
          },
          "excluded_items": {
            "type": "integer",
            "description": "The number of items excluded from processing."
          },
          "results": {
            "type": "array",
            "description": "The results for each batch item.",
            "items": {
              "type": "object",
              "properties": {
                "external_id": {
                  "type": "string",
                  "description": "The external ID provided in the batch request."
                },
                "role": {
                  "type": "string",
                  "enum": [
                    "employee"
                  ],
                  "description": "The type of person created."
                },
                "status": {
                  "type": "string",
                  "enum": [
                    "success",
                    "partial_success",
                    "failed"
                  ],
                  "description": "The status of this batch item."
                },
                "idx": {
                  "type": "integer",
                  "description": "The index of this item in the original batch request."
                },
                "uuid": {
                  "type": "string",
                  "format": "uuid",
                  "description": "The UUID of the created person."
                },
                "employee_uuid": {
                  "type": "string",
                  "format": "uuid",
                  "description": "The UUID of the created employee (if role is employee)."
                },
                "errors": {
                  "type": [
                    "array",
                    "null"
                  ],
                  "description": "Errors encountered while processing this batch item.",
                  "items": {
                    "type": "object",
                    "properties": {
                      "error_key": {
                        "type": "string",
                        "description": "The key identifying the error source."
                      },
                      "category": {
                        "type": "string",
                        "description": "The error category."
                      },
                      "message": {
                        "type": [
                          "string",
                          "null"
                        ],
                        "description": "Human-readable error message."
                      },
                      "errors": {
                        "type": [
                          "array",
                          "null"
                        ],
                        "description": "Nested errors for sub-operations.",
                        "items": {
                          "type": "object"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "exclusions": {
            "type": [
              "array",
              "null"
            ],
            "description": "Items excluded from processing due to validation errors.",
            "items": {
              "type": "object",
              "properties": {
                "external_id": {
                  "type": "string",
                  "description": "The external ID of the excluded item(s)."
                },
                "category": {
                  "type": "string",
                  "description": "The exclusion category."
                },
                "message": {
                  "type": "string",
                  "description": "Human-readable explanation for exclusion."
                },
                "item_count": {
                  "type": "integer",
                  "description": "Number of items affected by this exclusion."
                }
              }
            }
          }
        },
        "required": [
          "uuid",
          "idempotency_key",
          "status"
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
    "/v1/people_batches/{people_batch_uuid}": {
      "get": {
        "summary": "Get a people batch",
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
            "name": "people_batch_uuid",
            "in": "path",
            "description": "The UUID of the people batch",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-people_batches-people_batch_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns the status and results of a people batch.\n\nPoll this endpoint to check the batch processing status and retrieve results.\n\nscope: `people_batches:read`",
        "tags": [
          "People Batches"
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
                      "$ref": "#/components/schemas/People-Batch-Results/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/People-Batch-Results"
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
