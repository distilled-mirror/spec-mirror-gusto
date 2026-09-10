---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all information requests for a company

Fetch all information requests for a company.

scope: `information_requests:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Information Requests"
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
      "Information-Request": {
        "type": "object",
        "x-examples": {
          "example": {
            "uuid": "704c1291-274d-4552-aa5d-e7031023c2e5",
            "company_uuid": "3ac84ba3-87b3-40be-8523-d185dc243a6c",
            "type": "account_protection",
            "status": "pending_response",
            "blocking_payroll": false,
            "required_questions": []
          },
          "information_request_index_item": {
            "uuid": "704c1291-274d-4552-aa5d-e7031023c2e5",
            "company_uuid": "3ac84ba3-87b3-40be-8523-d185dc243a6c",
            "type": "company_onboarding",
            "status": "pending_response",
            "blocking_payroll": true,
            "required_questions": [
              {
                "question_uuid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
                "question_text": "How much wood can a wood chuck chuck?",
                "response_type": "text"
              },
              {
                "question_uuid": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
                "question_text": "Please upload supporting documentation",
                "response_type": "document"
              }
            ]
          }
        },
        "description": "Representation of an information request",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of an information request"
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company to which the information requests belongs"
          },
          "type": {
            "description": "The type of information request",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "company_onboarding",
                  "account_protection",
                  "payment_request",
                  "payment_error"
                ]
              },
              {
                "type": "null"
              }
            ]
          },
          "status": {
            "type": "string",
            "description": "The status of the information request",
            "enum": [
              "pending_response",
              "pending_review",
              "approved"
            ]
          },
          "blocking_payroll": {
            "type": "boolean",
            "description": "If true, this information request is blocking payroll, and may require response or requires review from our Risk Ops team."
          },
          "required_questions": {
            "type": "array",
            "description": "Questions the partner must answer or collect documents for",
            "items": {
              "type": "object",
              "properties": {
                "question_uuid": {
                  "type": "string"
                },
                "question_text": {
                  "type": "string"
                },
                "response_type": {
                  "type": "string"
                }
              },
              "required": [
                "question_uuid",
                "question_text",
                "response_type"
              ]
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
    "/v1/companies/{company_uuid}/information_requests": {
      "get": {
        "summary": "Get all information requests for a company",
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
          },
          {
            "name": "sort_by",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "pattern": "^(payroll_blocker|status|type)(:(asc|desc))?(,(payroll_blocker|status|type)(:(asc|desc))?)*$",
              "example": "payroll_blocker:asc"
            },
            "description": "Sort by one or more fields. Options: payroll_blocker, status, type. Append `:asc` or `:desc` to specify direction (e.g., `payroll_blocker:asc`). Defaults to ascending."
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-information-requests",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetch all information requests for a company.\n\nscope: `information_requests:read`",
        "tags": [
          "Information Requests"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Successful",
            "content": {
              "application/json": {
                "examples": {
                  "information_request_index_item": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Information-Request/x-examples/information_request_index_item"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Information-Request"
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
