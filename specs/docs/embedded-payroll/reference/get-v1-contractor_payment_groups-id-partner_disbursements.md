---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get partner disbursements for a contractor payment group

Get partner disbursements for a specific contractor payment group.

scope: `partner_disbursements:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractor Payment Groups"
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
      "Contractor-Payment-Group-Partner-Disbursements": {
        "type": "object",
        "description": "Partner disbursements for a contractor payment group",
        "x-examples": {
          "success_status": {
            "contractor_payment_group_uuid": "123e4567-e89b-12d3-a456-426655440000",
            "disbursements": [
              {
                "contractor_payment_uuid": "123e4567-e89b-12d3-a456-426655440001",
                "contractor_uuid": "123e4567-e89b-12d3-a456-426655440002",
                "payment_method": "Check",
                "payment_status": "Not partner managed"
              },
              {
                "contractor_payment_uuid": "123e4567-e89b-12d3-a456-426655440003",
                "contractor_uuid": "123e4567-e89b-12d3-a456-426655440004",
                "payment_method": "Direct Deposit",
                "payment_status": "Pending"
              }
            ]
          }
        },
        "properties": {
          "contractor_payment_group_uuid": {
            "type": "string",
            "description": "The UUID of the contractor payment group"
          },
          "disbursements": {
            "type": "array",
            "description": "List of disbursements for the contractor payment group",
            "items": {
              "type": "object",
              "properties": {
                "contractor_payment_uuid": {
                  "type": "string",
                  "description": "The UUID of the contractor payment"
                },
                "contractor_uuid": {
                  "type": "string",
                  "description": "The UUID of the contractor"
                },
                "payment_method": {
                  "type": "string",
                  "description": "The payment method for the disbursement",
                  "enum": [
                    "Direct Deposit",
                    "Check"
                  ]
                },
                "payment_status": {
                  "type": "string",
                  "description": "The status of the payment",
                  "enum": [
                    "Pending",
                    "Paid",
                    "Not partner managed",
                    "Converted to check"
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
    "/v1/contractor_payment_groups/{id}/partner_disbursements": {
      "get": {
        "summary": "Get partner disbursements for a contractor payment group",
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
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The UUID of the contractor payment group",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-contractor_payment_groups-id-partner_disbursements",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get partner disbursements for a specific contractor payment group.\n\nscope: `partner_disbursements:read`",
        "tags": [
          "Contractor Payment Groups"
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
                      "$ref": "#/components/schemas/Contractor-Payment-Group-Partner-Disbursements/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Contractor-Payment-Group-Partner-Disbursements"
                }
              }
            }
          },
          "404": {
            "description": "Not Found\n\nThe requested contractor payment group does not exist. Make sure the provided UUID is valid.\n",
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
