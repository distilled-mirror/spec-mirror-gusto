---
updatedAt: 2026-07-01T17:07:11.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a bulk report batch

Get a bulk report batch's status and results given the `request_uuid`. While in progress, only batch metadata is returned; once complete, it also includes a signed `report_url` (a zip of all generated reports, valid for 10 minutes) and a per-company breakdown.

Reports containing PHI are inaccessible with `company_reports:read:tier_2_only` data scope.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `company_reports:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Reports"
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
      "Bulk-Report": {
        "type": "object",
        "required": [
          "uuid",
          "status",
          "submitted_at",
          "completed_at",
          "submitted_items"
        ],
        "properties": {
          "uuid": {
            "type": "string",
            "format": "uuid",
            "description": "Unique identifier of the bulk report batch."
          },
          "status": {
            "type": "string",
            "enum": [
              "pending",
              "processing",
              "success",
              "partial_success",
              "failed"
            ],
            "description": "Overall batch status. `pending`/`processing` while in progress; once finished, `success` (all reports succeeded), `partial_success` (some succeeded, some failed), or `failed` (none succeeded)."
          },
          "submitted_at": {
            "type": "string",
            "format": "date-time",
            "description": "When the batch was accepted."
          },
          "completed_at": {
            "type": [
              "string",
              "null"
            ],
            "format": "date-time",
            "description": "When the batch reached a terminal state. Null while non-terminal."
          },
          "submitted_items": {
            "type": "integer",
            "description": "How many reports the partner asked for in this batch."
          },
          "partner_uuid": {
            "type": "string",
            "format": "uuid",
            "description": "UUID of the partner that owns this batch. Returned only once the batch has finished; omitted while in progress."
          },
          "processed_items": {
            "type": "integer",
            "description": "How many reports succeeded. Returned only once the batch has finished; omitted while in progress."
          },
          "report_url": {
            "type": [
              "string",
              "null"
            ],
            "description": "Signed S3 URL to a zip containing every successfully-generated report, valid for 10 minutes. Returned only once the batch has finished; omitted while in progress."
          },
          "companies": {
            "type": "array",
            "description": "Per-company breakdown. Returned only once the batch has finished; omitted while in progress.",
            "items": {
              "$ref": "#/components/schemas/Bulk-Report-Company"
            }
          }
        },
        "x-examples": {
          "pending": {
            "uuid": "4c3a536c-4c88-4fec-a4db-eb4112ab9c92",
            "status": "processing",
            "submitted_at": "2026-06-10T10:24:54Z",
            "completed_at": null,
            "submitted_items": 2
          },
          "success": {
            "uuid": "4c3a536c-4c88-4fec-a4db-eb4112ab9c92",
            "status": "success",
            "submitted_at": "2026-06-10T10:24:54Z",
            "completed_at": "2026-06-10T10:25:08Z",
            "submitted_items": 2,
            "partner_uuid": "0b9deb0b-5572-4b62-bce7-9b5624b6381d",
            "processed_items": 2,
            "report_url": "https://reports.gusto-api.com/bulk_reports/4c3a536c-4c88-4fec-a4db-eb4112ab9c92.zip",
            "companies": [
              {
                "company_uuid": "12345678-abcd-ef12-3456-7890abcdef12",
                "status": "success",
                "reports": [
                  {
                    "report_type": "custom_report",
                    "file_type": "csv",
                    "status": "success",
                    "error": null
                  },
                  {
                    "report_type": "general_ledger",
                    "file_type": "json",
                    "status": "success",
                    "error": null
                  }
                ]
              }
            ]
          }
        },
        "x-tags": [
          "Reports"
        ]
      },
      "Bulk-Report-Company": {
        "description": "Results for a single company in a bulk report batch.",
        "type": "object",
        "required": [
          "company_uuid",
          "status",
          "reports"
        ],
        "properties": {
          "company_uuid": {
            "type": "string",
            "format": "uuid",
            "description": "UUID of the company."
          },
          "status": {
            "type": "string",
            "enum": [
              "pending",
              "success",
              "partial_success",
              "failed"
            ],
            "description": "This company's overall status across its `reports`:\n- `success`: every report succeeded\n- `partial_success`: some succeeded, some failed\n- `failed`: every report failed\n- `pending`: at least one report is still being generated\n"
          },
          "reports": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Bulk-Report-Item-Result"
            }
          }
        },
        "x-tags": [
          "Reports"
        ]
      },
      "Bulk-Report-Item-Result": {
        "description": "A single report's outcome.",
        "type": "object",
        "required": [
          "report_type",
          "file_type",
          "status",
          "error"
        ],
        "properties": {
          "report_type": {
            "type": "string",
            "enum": [
              "custom_report",
              "general_ledger"
            ],
            "description": "Which report this entry refers to."
          },
          "file_type": {
            "type": "string",
            "description": "The report's output file type."
          },
          "status": {
            "type": "string",
            "enum": [
              "pending",
              "success",
              "failed"
            ],
            "description": "The terminal state for this individual report."
          },
          "error": {
            "type": [
              "string",
              "null"
            ],
            "description": "A user-facing error message when status is `failed`. Null on success."
          }
        },
        "x-tags": [
          "Reports"
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
    "/v1/bulk_reports/{request_uuid}": {
      "get": {
        "summary": "Get a bulk report batch",
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
            "name": "request_uuid",
            "in": "path",
            "description": "The UUID of the bulk report batch.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-bulk_reports-request_uuid",
        "security": [
          {
            "SystemAccessAuth": []
          }
        ],
        "description": "Get a bulk report batch's status and results given the `request_uuid`. While in progress, only batch metadata is returned; once complete, it also includes a signed `report_url` (a zip of all generated reports, valid for 10 minutes) and a per-company breakdown.\n\nReports containing PHI are inaccessible with `company_reports:read:tier_2_only` data scope.\n\n📘 System Access Authentication\n\nThis endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)\n\nscope: `company_reports:read`",
        "tags": [
          "Reports"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "examples": {
                  "pending": {
                    "value": {
                      "$ref": "#/components/schemas/Bulk-Report/x-examples/pending"
                    }
                  },
                  "success": {
                    "value": {
                      "$ref": "#/components/schemas/Bulk-Report/x-examples/success"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Bulk-Report"
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
