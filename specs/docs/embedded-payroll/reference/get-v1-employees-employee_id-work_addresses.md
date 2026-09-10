---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee's work addresses

Returns a list of an employee's work addresses. Each address includes its effective
date and a boolean signifying if it is the currently active work address.

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
      "Employee-Work-Addresses-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "uuid": "080b6254-ce7c-411f-9f7d-5a3ce3c51154",
              "employee_uuid": "6747692e-d2c8-4472-9c5e-183c65404fbf",
              "location_uuid": "9ccfade8-82ee-490c-8711-5c0787bccde8",
              "effective_date": "2021-01-01",
              "active": false,
              "version": "3097e9d0efb09ba2e00a8988a93b3091",
              "street_1": "91678 Farrell Meadow",
              "street_2": "Apt. 835",
              "city": "Phoenix",
              "state": "AZ",
              "zip": "85016",
              "country": "USA"
            },
            {
              "uuid": "35d62f15-75da-45aa-9c97-adc57342b925",
              "employee_uuid": "6747692e-d2c8-4472-9c5e-183c65404fbf",
              "location_uuid": "10330fe8-36ef-4713-aa59-9f8a432abd13",
              "effective_date": "2022-01-01",
              "active": false,
              "version": "5f48ce54afed81bb11dd89461bd0e214",
              "street_1": "800 Adolfo Gardens",
              "street_2": "Suite 419",
              "city": "Bremen",
              "state": "AL",
              "zip": "35033",
              "country": "USA"
            },
            {
              "uuid": "3f3ceaba-6b57-4039-a31a-0004bef83c6f",
              "employee_uuid": "6747692e-d2c8-4472-9c5e-183c65404fbf",
              "location_uuid": "98383e91-c67d-4b69-a617-5a57f91da48c",
              "effective_date": "2023-01-01",
              "active": true,
              "version": "a8a78c851337676137e22caf56ffe5b5",
              "street_1": "2216 Icie Villages",
              "street_2": "Apt. 798",
              "city": "Big Delta",
              "state": "AK",
              "zip": "99737",
              "country": "USA"
            }
          ]
        },
        "items": {
          "$ref": "#/components/schemas/Employee-Work-Address"
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
    "/v1/employees/{employee_id}/work_addresses": {
      "get": {
        "summary": "Get an employee's work addresses",
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
        "operationId": "get-v1-employees-employee_id-work_addresses",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a list of an employee's work addresses. Each address includes its effective\ndate and a boolean signifying if it is the currently active work address.\n\nscope: `employees:read`",
        "tags": [
          "Employee Addresses"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "List of employee work addresses",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Work-Addresses-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Work-Addresses-List"
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
