---
updatedAt: 2026-04-20T21:25:53.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Create an admin-approved time off request

Create a pre-approved time off request on behalf of an employee (admin or system initiated).
The request is always created with approved status.

scope: `time_off_requests:manage`

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
      "Embedded-Time-Off-Request": {
        "type": "object",
        "description": "The representation of a time off request.",
        "required": [
          "uuid",
          "status",
          "employee_note",
          "employer_note",
          "policy_type",
          "policy_uuid",
          "days",
          "employee",
          "initiator",
          "approver"
        ],
        "x-examples": {
          "success_status": {
            "uuid": "ad158cfb-99e4-4741-9db3-0bd3a267f222",
            "status": "pending",
            "employee_note": "Family vacation",
            "employer_note": null,
            "days": {
              "2026-10-20": "8.000",
              "2026-10-21": "8.000"
            },
            "policy_type": "vacation",
            "policy_uuid": "c2d9b1bd-3f36-4c2d-a727-b2af057d6a7f",
            "employee": {
              "uuid": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
              "full_name": "Alex Johnson"
            },
            "approver": null,
            "initiator": {
              "uuid": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
              "full_name": "Alex Johnson"
            }
          },
          "approved_status": {
            "uuid": "ad158cfb-99e4-4741-9db3-0bd3a267f222",
            "status": "approved",
            "employee_note": "Family vacation",
            "employer_note": null,
            "days": {
              "2026-10-20": "8.000",
              "2026-10-21": "8.000"
            },
            "policy_type": "vacation",
            "policy_uuid": "c2d9b1bd-3f36-4c2d-a727-b2af057d6a7f",
            "employee": {
              "uuid": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
              "full_name": "Alex Johnson"
            },
            "approver": {
              "uuid": "21d8dff4-ce09-4120-a274-3a5628bf6769",
              "full_name": "Morgan Chen"
            },
            "initiator": {
              "uuid": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
              "full_name": "Alex Johnson"
            }
          },
          "declined_status": {
            "uuid": "ad158cfb-99e4-4741-9db3-0bd3a267f222",
            "status": "declined",
            "employee_note": "Family vacation",
            "employer_note": "Not enough coverage",
            "days": {
              "2026-10-20": "8.000",
              "2026-10-21": "8.000"
            },
            "policy_type": "vacation",
            "policy_uuid": "c2d9b1bd-3f36-4c2d-a727-b2af057d6a7f",
            "employee": {
              "uuid": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
              "full_name": "Alex Johnson"
            },
            "approver": null,
            "initiator": {
              "uuid": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
              "full_name": "Alex Johnson"
            }
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the time off request.",
            "example": "ad158cfb-99e4-4741-9db3-0bd3a267f222",
            "readOnly": true
          },
          "status": {
            "type": "string",
            "description": "The status of the time off request.",
            "example": "pending",
            "enum": [
              "pending",
              "approved",
              "declined",
              "consumed"
            ],
            "readOnly": true
          },
          "employee_note": {
            "type": [
              "string",
              "null"
            ],
            "description": "A note about the time off request, from the employee to the employer.",
            "example": "Family vacation",
            "readOnly": true
          },
          "employer_note": {
            "type": [
              "string",
              "null"
            ],
            "description": "A note about the time off request, from the employer to the employee.",
            "example": null,
            "readOnly": true
          },
          "policy_type": {
            "type": [
              "string",
              "null"
            ],
            "description": "The type of the time off policy (e.g. vacation, sick).",
            "example": "vacation",
            "readOnly": true
          },
          "policy_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the time off policy associated with this request.",
            "example": "c2d9b1bd-3f36-4c2d-a727-b2af057d6a7f",
            "readOnly": true
          },
          "days": {
            "description": "An object where keys are dates in YYYY-MM-DD format and values are hours as string decimals (e.g. {\"2025-01-20\": \"8.000\"}).",
            "type": "object",
            "additionalProperties": {
              "type": "string"
            },
            "example": {
              "2026-10-20": "8.000",
              "2026-10-21": "8.000"
            },
            "readOnly": true
          },
          "employee": {
            "type": "object",
            "description": "",
            "properties": {
              "uuid": {
                "type": "string",
                "description": "The UUID of the employee the time off request is for.",
                "example": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
                "readOnly": true
              },
              "full_name": {
                "type": "string",
                "description": "The full name of the employee the time off request is for.",
                "example": "Alex Johnson",
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
                "example": "51924fa0-26c6-4d4c-8832-3ef0b422c67e",
                "readOnly": true
              },
              "full_name": {
                "type": "string",
                "description": "The full name of the employee who initiated the time off request.",
                "example": "Alex Johnson",
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
                "example": "21d8dff4-ce09-4120-a274-3a5628bf6769",
                "readOnly": true
              },
              "full_name": {
                "type": "string",
                "description": "The full name of the employee who approved the time off request.",
                "example": "Morgan Chen",
                "readOnly": true
              }
            },
            "readOnly": true
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
    "/v1/companies/{company_uuid}/time_off/admin_approved_requests": {
      "post": {
        "summary": "Create an admin-approved time off request",
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
        "operationId": "post-v1-companies-company_uuid-time_off-admin_approved_requests",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Create a pre-approved time off request on behalf of an employee (admin or system initiated).\nThe request is always created with approved status.\n\nscope: `time_off_requests:manage`",
        "tags": [
          "Time Off Requests"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "201": {
            "description": "created",
            "content": {
              "application/json": {
                "examples": {
                  "approved_status": {
                    "value": {
                      "$ref": "#/components/schemas/Embedded-Time-Off-Request/x-examples/approved_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Embedded-Time-Off-Request"
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
        },
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "employee_uuid": {
                    "type": "string",
                    "description": "The UUID of the employee"
                  },
                  "policy_uuid": {
                    "type": "string",
                    "description": "The UUID of the time off policy"
                  },
                  "employer_note": {
                    "type": "string",
                    "description": "A note from the employer about the request"
                  },
                  "approver_uuid": {
                    "type": "string",
                    "description": "The UUID of the approving admin. Defaults to the primary payroll admin."
                  },
                  "start_date": {
                    "type": "string",
                    "description": "The start date of the time off request (YYYY-MM-DD)"
                  },
                  "end_date": {
                    "type": "string",
                    "description": "The end date of the time off request (YYYY-MM-DD)"
                  },
                  "days": {
                    "type": "object",
                    "additionalProperties": {
                      "type": "string"
                    },
                    "description": "An object where keys are dates in YYYY-MM-DD format and values are hours as string decimals (e.g. {\"2025-01-20\": \"8.000\"})"
                  }
                },
                "required": [
                  "employee_uuid",
                  "policy_uuid",
                  "start_date",
                  "end_date",
                  "days"
                ]
              }
            }
          },
          "required": true
        }
      }
    }
  }
}
```
