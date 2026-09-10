---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all Wire In Requests for a company

Fetches all Wire In Requests for a company.

scope: `payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Wire In Requests"
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
      "Wire-In-Request": {
        "type": "object",
        "x-examples": {
          "example": {
            "uuid": "05ed3150-591e-4f8b-bfd5-55d478edd2d8",
            "status": "awaiting_funds",
            "origination_bank": "JP Morgan Chase",
            "origination_bank_address": "1 Chase Plaza, New York, NY 10081",
            "recipient_name": "Gusto, Inc",
            "recipient_address": "525 20th Street, San Francisco, CA 94107",
            "recipient_account_number": "21911761",
            "recipient_routing_number": "123454321",
            "additional_notes": "Additional Notes",
            "bank_name": "JP Morgan Chase",
            "date_sent": "2024-06-10",
            "unique_tracking_code": "1trvxwxp57zf",
            "payment_type": "Payroll",
            "payment_uuid": "5faae454-e629-490b-a72a-c022c2c9e6bc",
            "amount_sent": "1014500.00",
            "requested_amount": "1014500.00",
            "wire_in_deadline": "2024-06-21T18:00:00Z"
          }
        },
        "description": "Representation of a wire in request",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of a wire in request"
          },
          "status": {
            "type": "string",
            "description": "Status of the wire in",
            "enum": [
              "awaiting_funds",
              "pending_review",
              "approved",
              "canceled"
            ]
          },
          "origination_bank": {
            "type": "string",
            "description": "Name of bank receiving the wire in"
          },
          "origination_bank_address": {
            "type": "string",
            "description": "Address of bank receiving the wire in"
          },
          "recipient_name": {
            "type": "string",
            "description": "Name of the recipient of the wire In"
          },
          "recipient_address": {
            "type": "string",
            "description": "Address of the recipient of the wire in"
          },
          "recipient_account_number": {
            "type": "string",
            "description": "Recipient bank account number"
          },
          "recipient_routing_number": {
            "type": "string",
            "description": "Recipient bank routing number"
          },
          "additional_notes": {
            "type": [
              "string",
              "null"
            ],
            "description": "Notes for the wire in request"
          },
          "bank_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "Name of the bank initiating the wire in"
          },
          "date_sent": {
            "type": [
              "string",
              "null"
            ],
            "description": "Date the wire in was sent"
          },
          "unique_tracking_code": {
            "type": "string",
            "description": "Include in note with bank to track payment"
          },
          "payment_type": {
            "type": "string",
            "description": "Type of payment for the wire in",
            "enum": [
              "Payroll",
              "ContractorPaymentGroup"
            ]
          },
          "payment_uuid": {
            "type": "string",
            "description": "Unique identifier of the payment"
          },
          "amount_sent": {
            "type": [
              "string",
              "null"
            ],
            "description": "Amount sent through wire in"
          },
          "requested_amount": {
            "type": "string",
            "description": "Requested amount for the payment"
          },
          "wire_in_deadline": {
            "type": "string",
            "description": "Deadline to submit the wire in"
          }
        }
      },
      "Wire-In-Request-List": {
        "type": "array",
        "items": {
          "$ref": "#/components/schemas/Wire-In-Request"
        },
        "x-examples": {
          "example": [
            {
              "uuid": "c5fdae57-5483-4529-9aae-f0edceed92d4",
              "status": "awaiting_funds",
              "origination_bank": "JP Morgan Chase",
              "origination_bank_address": "1 Chase Plaza, New York, NY 10081",
              "recipient_name": "Gusto, Inc",
              "recipient_address": "525 20th Street, San Francisco, CA 94107",
              "recipient_account_number": "21911761",
              "recipient_routing_number": "123454321",
              "additional_notes": null,
              "bank_name": null,
              "date_sent": null,
              "unique_tracking_code": "1trvxwxp57zf",
              "payment_type": "Payroll",
              "payment_uuid": "5faae454-e629-490b-a72a-c022c2c9e6bc",
              "amount_sent": null,
              "requested_amount": "1014500.00",
              "wire_in_deadline": "2024-06-21T18:00:00Z"
            },
            {
              "uuid": "a47fc11d-8d92-4b3e-9f2a-3a23b9d8e7d1",
              "status": "awaiting_funds",
              "origination_bank": "JP Morgan Chase",
              "origination_bank_address": "1 Chase Plaza, New York, NY 10081",
              "recipient_name": "Gusto, Inc",
              "recipient_address": "525 20th Street, San Francisco, CA 94107",
              "recipient_account_number": "21911761",
              "recipient_routing_number": "123454321",
              "additional_notes": null,
              "bank_name": null,
              "date_sent": null,
              "unique_tracking_code": "6kfhwxq2crsm",
              "payment_type": "ContractorPaymentGroup",
              "payment_uuid": "8b6c3d70-9b8e-4d4d-b6a1-a1f3a6d9b2c4",
              "amount_sent": null,
              "requested_amount": "15000.00",
              "wire_in_deadline": "2024-06-21T18:00:00Z"
            }
          ]
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
    "/v1/companies/{company_uuid}/wire_in_requests": {
      "get": {
        "summary": "Get all Wire In Requests for a company",
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
            "name": "page",
            "in": "query",
            "required": false,
            "description": "The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.",
            "schema": {
              "type": "integer"
            }
          },
          {
            "name": "per",
            "in": "query",
            "required": false,
            "description": "Number of objects per page. For majority of endpoints will default to 25",
            "schema": {
              "type": "integer"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-companies-company_uuid-wire_in_request_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetches all Wire In Requests for a company.\n\nscope: `payrolls:read`",
        "tags": [
          "Wire In Requests"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Wire-In-Request-List/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Wire-In-Request-List"
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
