---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee's home addresses

The home address of an employee is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.

Supports home address effective dating and courtesy withholding.

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
      "Warning-Object": {
        "type": "object",
        "properties": {
          "error_key": {
            "type": "string",
            "description": "Specifies where the warning occurs. Typically identifies the attribute or parameter related to the warning."
          },
          "category": {
            "type": "string",
            "description": "Specifies the type of warning. Can be used to build custom warning handling."
          },
          "message": {
            "type": "string",
            "description": "Provides details about the warning. The message can be surfaced directly to the end user."
          }
        }
      },
      "Employee-Address-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "uuid": "d6b7472f-bb55-41ca-a55c-9adbd3c64e09",
              "version": "7eee445be93fc50fd3cbb55b8d943fb3",
              "employee_uuid": "d1a166b4-79b4-413f-b067-27534ec59ecd",
              "street_1": "3121 Milky Way",
              "street_2": "",
              "city": "San Francisco",
              "state": "CA",
              "zip": "94107",
              "country": "USA",
              "active": false,
              "effective_date": "2024-06-09",
              "courtesy_withholding": false
            },
            {
              "uuid": "1b59a593-d324-4d97-9296-99ecc95f81d1",
              "version": "5147ad755821c4ba3dbc3afa1055ff4d",
              "employee_uuid": "d1a166b4-79b4-413f-b067-27534ec59ecd",
              "street_1": "3624 Victoria Ln",
              "street_2": "",
              "city": "Cincinnati",
              "state": "OH",
              "zip": "45208",
              "country": "USA",
              "active": true,
              "effective_date": "2025-05-26",
              "courtesy_withholding": false
            },
            {
              "uuid": "69489b54-976d-4027-8b51-702e5c8c62d3",
              "version": "f0765fa5a85f62723320763494a481a6",
              "employee_uuid": "d1a166b4-79b4-413f-b067-27534ec59ecd",
              "street_1": "Main st.",
              "street_2": "",
              "city": "New York",
              "state": "NY",
              "zip": "10011",
              "country": "USA",
              "active": false,
              "effective_date": "2025-07-09",
              "courtesy_withholding": false
            }
          ]
        },
        "items": {
          "$ref": "#/components/schemas/Employee-Address"
        }
      },
      "Employee-Address": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "uuid": "700af712-62ba-4dff-824f-97a3c6fda416",
            "version": "6c3c23e4cc840bd3f1416f72b5380eff",
            "employee_uuid": "78d20691-f1b4-4f74-bc4c-1d4db0099b00",
            "street_1": "3121 Milky Way",
            "street_2": "",
            "city": "San Francisco",
            "state": "CA",
            "zip": "94107",
            "country": "USA",
            "active": true,
            "effective_date": "1970-01-01",
            "courtesy_withholding": false
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the employee address"
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee"
          },
          "effective_date": {
            "type": "string",
            "format": "date",
            "description": "The date the employee started living at the address."
          },
          "courtesy_withholding": {
            "type": "boolean",
            "description": "Determines if home taxes should be withheld and paid for employee."
          },
          "street_1": {
            "type": "string",
            "readOnly": false
          },
          "street_2": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false
          },
          "city": {
            "type": "string",
            "readOnly": false
          },
          "state": {
            "type": "string",
            "readOnly": false
          },
          "zip": {
            "type": "string",
            "readOnly": false
          },
          "country": {
            "type": "string",
            "readOnly": false,
            "default": "USA"
          },
          "active": {
            "type": "boolean",
            "description": "The status of the location. Inactive locations have been deleted, but may still have historical data associated with them.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "warnings": {
            "type": "array",
            "description": "An array of warning objects that provide additional information about the address. Warnings do not prevent the address from being saved.",
            "items": {
              "$ref": "#/components/schemas/Warning-Object"
            }
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
    "/v1/employees/{employee_id}/home_addresses": {
      "get": {
        "summary": "Get an employee's home addresses",
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
            "name": "employee_id",
            "in": "path",
            "description": "The UUID of the employee",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employees-employee_id-home_addresses",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "The home address of an employee is used to determine certain tax information about them. Addresses are geocoded on create and update to ensure validity.\n\nSupports home address effective dating and courtesy withholding.\n\nscope: `employees:read`",
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
                      "$ref": "#/components/schemas/Employee-Address-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Address-List"
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
