---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee work address

The work address of an employee is used for payroll tax purposes.

scope: `employees:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employee Addresses"
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
      "Employee-Work-Address": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "uuid": "64ee5fd7-3eb2-4083-883c-95e93e181cc8",
            "employee_uuid": "d773461f-848a-40a1-8f09-b2ee4249d5c7",
            "location_uuid": "733ab2af-9510-408f-8d20-09196967174f",
            "effective_date": "2020-01-31",
            "active": true,
            "version": "3879823d440f3a3215d129ac73c58966",
            "street_1": "977 Marks Viaduct",
            "street_2": "Apt. 958",
            "city": "Pink Hill",
            "state": "NC",
            "zip": "28572",
            "country": "USA"
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "readOnly": true,
            "description": "The unique identifier of this work address."
          },
          "effective_date": {
            "type": "string",
            "description": "The date the employee began working at this location."
          },
          "active": {
            "type": "boolean",
            "readOnly": true,
            "description": "Signifies if this address is the active work address for the current date"
          },
          "location_uuid": {
            "type": "string",
            "description": "UUID reference to the company location for this work address."
          },
          "employee_uuid": {
            "type": "string",
            "description": "UUID reference to the employee for this work address."
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "street_1": {
            "type": "string",
            "readOnly": true
          },
          "street_2": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": true
          },
          "city": {
            "type": "string",
            "readOnly": true
          },
          "state": {
            "type": "string",
            "readOnly": true
          },
          "zip": {
            "type": "string",
            "readOnly": true
          },
          "country": {
            "type": "string",
            "readOnly": true,
            "default": "USA"
          }
        },
        "required": [
          "uuid",
          "version"
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
    "/v1/work_addresses/{work_address_uuid}": {
      "get": {
        "summary": "Get an employee work address",
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
            "name": "work_address_uuid",
            "in": "path",
            "description": "The UUID of the work address",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-work_addresses-work_address_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "The work address of an employee is used for payroll tax purposes.\n\nscope: `employees:read`",
        "tags": [
          "Employee Addresses"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Work-Address/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Work-Address"
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
