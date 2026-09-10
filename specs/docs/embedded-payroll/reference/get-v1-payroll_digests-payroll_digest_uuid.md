---
updatedAt: 2026-05-22T17:38:22.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a payroll digest batch

Returns the status and results of a payroll digest batch.

Poll this endpoint until the batch `status` reaches a terminal value (`completed` or `failed`). Once terminal, the response includes the full `results` array (one entry per attempted company, each with its own per-company `status` — `success`, `partial_success`, or `failed`) and the `exclusions` array (one entry per company that could not be looked up or processed).

Note that the top-level batch `status` (`pending` / `processing` / `completed` / `failed`) is distinct from the per-company `status` returned inside `results[]` and `exclusions[]`. A `completed` batch does not imply every company succeeded — inspect the arrays for per-company outcomes.

Results are stored in Redis with a short TTL after completion. If the partner polls after results have expired, this endpoint returns 410 Gone — partners should re-submit a new batch to fetch fresh data.

📘 System Access Authentication

This endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)

scope: `payroll_digests:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Payroll Digests"
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
      "Payroll-Digest-Results": {
        "type": "object",
        "description": "A payroll digest batch with processing results.",
        "x-examples": {
          "success_status": {
            "uuid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "idempotency_key": "80a74f8b-2c16-45e5-9038-aa108849c6e6",
            "status": "completed",
            "submitted_at": "2026-04-01T14:30:00Z",
            "completed_at": "2026-04-01T14:30:12Z",
            "submitted_items": 4,
            "processed_items": 2,
            "excluded_items": 2,
            "results": [
              {
                "idx": 0,
                "entity_type": "company",
                "uuid": "c1111111-1111-1111-1111-111111111111",
                "name": "Acme Corporation",
                "status": "success",
                "blockers": [
                  {
                    "type": "missing_bank_account",
                    "description": "Company bank account not set up"
                  }
                ],
                "payrolls": [
                  {
                    "payroll_uuid": null,
                    "payroll_type": "regular",
                    "display_title": "Run biweekly payroll",
                    "auto_payroll": false,
                    "status": "ready_to_start",
                    "pay_period": {
                      "start_date": "2026-03-16",
                      "end_date": "2026-03-29",
                      "check_date": "2026-04-03",
                      "run_payroll_by": "2026-03-31"
                    },
                    "pay_schedule": {
                      "uuid": "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                      "frequency": "Every other week",
                      "custom_name": "Custom - every 1st and 15th"
                    },
                    "totals": null
                  },
                  {
                    "payroll_uuid": "11111111-2222-3333-4444-555555555555",
                    "payroll_type": "regular",
                    "display_title": "Run biweekly payroll",
                    "auto_payroll": true,
                    "status": "submitted",
                    "pay_period": {
                      "start_date": "2026-03-02",
                      "end_date": "2026-03-15",
                      "check_date": "2026-03-20",
                      "run_payroll_by": "2026-03-17"
                    },
                    "pay_schedule": {
                      "uuid": "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                      "frequency": "Every other week",
                      "custom_name": "Custom - every 1st and 15th"
                    },
                    "totals": {
                      "total_debit_amount": "15234.56",
                      "net_pay": "11456.78",
                      "total_employer_cost": "16890.12"
                    }
                  }
                ]
              },
              {
                "idx": 3,
                "entity_type": "company",
                "uuid": "c2222222-2222-2222-2222-222222222222",
                "name": "Widget Inc",
                "status": "success",
                "payrolls": []
              }
            ],
            "exclusions": [
              {
                "idx": 1,
                "entity_type": "company",
                "uuid": "c3333333-3333-3333-3333-333333333333",
                "status": "failed",
                "category": "not_found",
                "message": "Company not found."
              },
              {
                "idx": 2,
                "entity_type": "company",
                "uuid": "c4444444-4444-4444-4444-444444444444",
                "status": "failed",
                "category": "company_inactive",
                "message": "Company is inactive or not fully onboarded."
              }
            ]
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "format": "uuid",
            "description": "The unique identifier of the payroll digest batch.",
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
            "description": "The lifecycle status of the batch request itself. Terminal values are `completed` (processing finished — inspect `results` and `exclusions` for per-company outcomes) and `failed` (request failed; can be retried). This is distinct from the per-company `status` returned inside `results[]` and `exclusions[]`."
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
            "description": "The number of companies submitted in the batch."
          },
          "processed_items": {
            "type": "integer",
            "description": "The number of companies successfully processed. Only present once the batch reaches a terminal status."
          },
          "excluded_items": {
            "type": "integer",
            "description": "The number of companies excluded from processing. Only present once the batch reaches a terminal status."
          },
          "results": {
            "type": "array",
            "description": "Per-company results. Only present once the batch reaches a terminal status. Includes successfully processed companies (with their `payrolls` array, which may be empty when the company has no payrolls in the date window).",
            "items": {
              "type": "object",
              "properties": {
                "idx": {
                  "type": "integer",
                  "description": "The index of this company in the original POST batch array."
                },
                "entity_type": {
                  "type": "string",
                  "enum": [
                    "company"
                  ],
                  "description": "The type of entity this result represents."
                },
                "uuid": {
                  "type": "string",
                  "format": "uuid",
                  "description": "The UUID of the company."
                },
                "name": {
                  "type": "string",
                  "description": "The legal/display name of the company."
                },
                "status": {
                  "type": "string",
                  "enum": [
                    "success",
                    "partial_success",
                    "failed"
                  ],
                  "description": "The status of this company's digest computation."
                },
                "blockers": {
                  "type": "array",
                  "description": "Reasons the company cannot currently run payroll. Applies to every payroll in this company's `payrolls` array — blockers are evaluated at the company level, not per payroll. Empty when there are no blockers.",
                  "items": {
                    "type": "object",
                    "properties": {
                      "type": {
                        "type": "string",
                        "description": "A machine-readable blocker key (e.g. `missing_bank_account`)."
                      },
                      "description": {
                        "type": "string",
                        "description": "Human-readable description of the blocker."
                      }
                    }
                  }
                },
                "payrolls": {
                  "type": "array",
                  "description": "Payrolls for this company within the digest date window (7 days past, 30–60 days future). May be empty.",
                  "items": {
                    "type": "object",
                    "properties": {
                      "payroll_uuid": {
                        "type": [
                          "string",
                          "null"
                        ],
                        "format": "uuid",
                        "description": "UUID of the payroll. `null` for upcoming pay periods that have not been started yet (the `payrolls` API has not yet created a payroll record). Once a payroll is created, subsequent digest requests will include the real `payroll_uuid`."
                      },
                      "payroll_type": {
                        "type": "string",
                        "description": "The type of payroll (e.g. `regular`, `new_hire`, `termination`, `transition`, `bonus`, `correction`)."
                      },
                      "display_title": {
                        "type": "string",
                        "description": "Partner-facing display title for this payroll (e.g. \"Run biweekly payroll\")."
                      },
                      "auto_payroll": {
                        "type": "boolean",
                        "description": "Whether the company has auto-payroll enabled for this pay schedule."
                      },
                      "status": {
                        "type": "string",
                        "description": "The lifecycle status of the payroll (e.g. `ready_to_start`, `in_progress`, `submitted`, `completed`, `failed`)."
                      },
                      "pay_period": {
                        "type": "object",
                        "properties": {
                          "start_date": {
                            "type": [
                              "string",
                              "null"
                            ],
                            "format": "date",
                            "description": "First day of the pay period."
                          },
                          "end_date": {
                            "type": [
                              "string",
                              "null"
                            ],
                            "format": "date",
                            "description": "Last day of the pay period."
                          },
                          "check_date": {
                            "type": [
                              "string",
                              "null"
                            ],
                            "format": "date",
                            "description": "The date employees get paid."
                          },
                          "run_payroll_by": {
                            "type": [
                              "string",
                              "null"
                            ],
                            "format": "date",
                            "description": "The deadline to run payroll for this pay period."
                          }
                        }
                      },
                      "pay_schedule": {
                        "type": [
                          "object",
                          "null"
                        ],
                        "properties": {
                          "uuid": {
                            "type": "string",
                            "format": "uuid",
                            "description": "UUID of the pay schedule."
                          },
                          "frequency": {
                            "type": "string",
                            "description": "Human-friendly pay frequency (e.g. \"Every other week\")."
                          },
                          "custom_name": {
                            "type": [
                              "string",
                              "null"
                            ],
                            "description": "Custom name for the pay schedule, when set."
                          }
                        }
                      },
                      "totals": {
                        "type": [
                          "object",
                          "null"
                        ],
                        "description": "Pay totals. `null` when the payroll has not been calculated, or when the calculation is stale (the partner edited hours/earnings after the last calculation).",
                        "properties": {
                          "total_debit_amount": {
                            "type": "string",
                            "description": "Total amount debited from the company bank account (string-formatted decimal)."
                          },
                          "net_pay": {
                            "type": "string",
                            "description": "Total net pay across all employees on this payroll (string-formatted decimal)."
                          },
                          "total_employer_cost": {
                            "type": "string",
                            "description": "Total employer cost including taxes and benefits (string-formatted decimal)."
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "exclusions": {
            "type": "array",
            "description": "Companies that could not be processed. Only present once the batch reaches a terminal status. Every UUID submitted in the POST batch appears in exactly one of `results` or `exclusions`.",
            "items": {
              "type": "object",
              "properties": {
                "idx": {
                  "type": "integer",
                  "description": "The index of this company in the original POST batch array."
                },
                "entity_type": {
                  "type": "string",
                  "enum": [
                    "company"
                  ],
                  "description": "The type of entity this exclusion represents."
                },
                "uuid": {
                  "type": "string",
                  "format": "uuid",
                  "description": "The UUID of the excluded company."
                },
                "status": {
                  "type": "string",
                  "enum": [
                    "failed"
                  ],
                  "description": "The status of this company's digest computation."
                },
                "category": {
                  "type": "string",
                  "enum": [
                    "not_found",
                    "company_inactive",
                    "duplicate",
                    "internal_error"
                  ],
                  "description": "Machine-readable category for why the company was excluded."
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
    "/v1/payroll_digests/{payroll_digest_uuid}": {
      "get": {
        "summary": "Get a payroll digest batch",
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
            "name": "payroll_digest_uuid",
            "in": "path",
            "description": "The UUID of the payroll digest batch returned by `POST /v1/payroll_digests`.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-payroll_digests-payroll_digest_uuid",
        "security": [
          {
            "SystemAccessAuth": []
          }
        ],
        "description": "Returns the status and results of a payroll digest batch.\n\nPoll this endpoint until the batch `status` reaches a terminal value (`completed` or `failed`). Once terminal, the response includes the full `results` array (one entry per attempted company, each with its own per-company `status` — `success`, `partial_success`, or `failed`) and the `exclusions` array (one entry per company that could not be looked up or processed).\n\nNote that the top-level batch `status` (`pending` / `processing` / `completed` / `failed`) is distinct from the per-company `status` returned inside `results[]` and `exclusions[]`. A `completed` batch does not imply every company succeeded — inspect the arrays for per-company outcomes.\n\nResults are stored in Redis with a short TTL after completion. If the partner polls after results have expired, this endpoint returns 410 Gone — partners should re-submit a new batch to fetch fresh data.\n\n📘 System Access Authentication\n\nThis endpoint uses the [Bearer Auth scheme with the system-level access token in the HTTP Authorization header](https://docs.gusto.com/embedded-payroll/docs/system-access)\n\nscope: `payroll_digests:read`",
        "tags": [
          "Payroll Digests"
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
                      "$ref": "#/components/schemas/Payroll-Digest-Results/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payroll-Digest-Results"
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
