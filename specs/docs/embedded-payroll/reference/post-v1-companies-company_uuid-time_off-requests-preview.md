---
updatedAt: 2026-04-20T21:25:53.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Preview a time off request

Preview a time off request to see balance impact before creating

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
      "Embedded-Time-Off-Request-Preview": {
        "type": "object",
        "description": "Preview of the balance impact for a time off request before it is created or updated.",
        "required": [
          "balance_hours",
          "this_request_hours",
          "other_requested_hours",
          "remaining_balance_hours",
          "allow_negative_balance",
          "unlimited"
        ],
        "x-examples": {
          "success_status": {
            "balance_hours": "64.0",
            "this_request_hours": "16.0",
            "other_requested_hours": "0.0",
            "remaining_balance_hours": "48.0",
            "allow_negative_balance": false,
            "unlimited": false
          }
        },
        "properties": {
          "balance_hours": {
            "type": "string",
            "nullable": true,
            "description": "The employee's current available balance hours for this policy. Null for unlimited policies.",
            "example": "64.0",
            "readOnly": true
          },
          "this_request_hours": {
            "type": "string",
            "description": "The total hours for this time off request.",
            "example": "16.0",
            "readOnly": true
          },
          "other_requested_hours": {
            "type": "string",
            "description": "Hours from other pending or approved requests for this policy.",
            "example": "0.0",
            "readOnly": true
          },
          "remaining_balance_hours": {
            "type": "string",
            "nullable": true,
            "description": "The projected balance after this request is applied. Null for unlimited policies.",
            "example": "48.0",
            "readOnly": true
          },
          "allow_negative_balance": {
            "type": "boolean",
            "description": "Whether the time off policy allows a negative balance.",
            "example": false,
            "readOnly": true
          },
          "unlimited": {
            "type": "boolean",
            "description": "Whether the time off policy provides unlimited time off.",
            "example": false,
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
    "/v1/companies/{company_uuid}/time_off/requests/preview": {
      "post": {
        "summary": "Preview a time off request",
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
        "operationId": "post-v1-companies-company_uuid-time_off-requests-preview",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Preview a time off request to see balance impact before creating\n\nscope: `time_off_requests:read`",
        "tags": [
          "Time Off Requests"
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
                      "$ref": "#/components/schemas/Embedded-Time-Off-Request-Preview/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Embedded-Time-Off-Request-Preview"
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
                  "request_uuid": {
                    "type": "string",
                    "description": "The UUID of an existing time off request to preview changes for"
                  },
                  "employee_uuid": {
                    "type": "string",
                    "description": "The UUID of the employee"
                  },
                  "policy_uuid": {
                    "type": "string",
                    "description": "The UUID of the time off policy"
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
