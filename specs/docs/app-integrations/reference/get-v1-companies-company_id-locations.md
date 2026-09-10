---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all company locations

Retrieves all company locations (addresses) associated with a company: mailing addresses, filing
addresses, or work locations. A single address may serve multiple, or all, purposes.

Since all company locations are subsets of locations, use the Locations endpoints to
[get](ref:get-v1-locations-location_id) or [update](ref:put-v1-locations-location_id) an individual record.

scope: `companies:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Locations"
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
      "Location": {
        "description": "The representation of an address in Gusto.",
        "type": "object",
        "title": "",
        "x-examples": {
          "success_status": {
            "created_at": "2025-06-09T13:43:49.000-07:00",
            "updated_at": "2025-06-09T13:43:50.000-07:00",
            "company_uuid": "10593a6a-505b-4aa6-bf31-15dcdceedbe3",
            "version": "e1bdd845a493c74908f8e15d6114169b",
            "uuid": "6b1351a2-de35-4499-b948-43abab274634",
            "street_1": "300 3rd Street",
            "street_2": "Apartment 318",
            "city": "San Francisco",
            "state": "CA",
            "zip": "94107",
            "country": "USA",
            "active": true,
            "phone_number": "8009360383",
            "filing_address": true,
            "mailing_address": true
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the location object.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "company_uuid": {
            "type": "string",
            "description": "The UUID for the company to which the location belongs. Only included if the location belongs to a company.",
            "readOnly": true
          },
          "phone_number": {
            "type": "string",
            "readOnly": false,
            "description": "The phone number for the location. Required for company locations. Optional for employee locations."
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
          "mailing_address": {
            "type": "boolean",
            "description": "Specifies if the location is the company's mailing address. Only included if the location belongs to a company."
          },
          "filing_address": {
            "description": "Specifies if the location is the company's filing address. Only included if the location belongs to a company.",
            "type": "boolean"
          },
          "created_at": {
            "type": "string",
            "description": "Datetime for when location is created"
          },
          "updated_at": {
            "type": "string",
            "description": "Datetime for when location is updated"
          },
          "active": {
            "type": "boolean",
            "description": "The status of the location. Inactive locations have been deleted, but may still have historical data associated with them.",
            "readOnly": true
          },
          "inactive": {
            "type": "boolean",
            "description": "The status of the location. Inactive locations have been deleted, but may still have historical data associated with them.",
            "readOnly": true
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
          "uuid"
        ]
      },
      "Company-Locations-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "uuid": "04552eb9-7829-4b18-ae96-6983552948df",
              "version": "7d9753112507b9dda4fb97910f39b06e",
              "company_uuid": "6bf7807c-a5a0-4f4d-b2e7-3fbb4b2299fb",
              "phone_number": "5825710808",
              "street_1": "412 Kiera Stravenue",
              "street_2": "Suite 391",
              "city": "San Francisco",
              "state": "CA",
              "zip": "94107",
              "country": "USA",
              "mailing_address": false,
              "filing_address": false,
              "created_at": "2023-09-12T16:42:25.000-07:00",
              "updated_at": "2023-09-12T16:42:25.000-07:00",
              "active": true,
              "inactive": false
            },
            {
              "uuid": "fa94a2fd-11a8-4024-87ff-85c587d9d2b4",
              "version": "15e6b9680e00f3122729e64e3cef3224",
              "company_uuid": "6bf7807c-a5a0-4f4d-b2e7-3fbb4b2299fb",
              "phone_number": "2866070827",
              "street_1": "644 Fay Vista",
              "street_2": "Suite 842",
              "city": "Richmond",
              "state": "VA",
              "zip": "23218",
              "country": "USA,",
              "mailing_address": true,
              "filing_address": false,
              "created_at": "2023-09-12T16:42:25.000-07:00",
              "updated_at": "2023-09-12T16:42:25.000-07:00",
              "active": true,
              "inactive": false
            }
          ]
        },
        "items": {
          "$ref": "#/components/schemas/Location"
        }
      },
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
    "/v1/companies/{company_id}/locations": {
      "get": {
        "summary": "Get all company locations",
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
            "name": "company_id",
            "in": "path",
            "description": "The UUID of the company",
            "example": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
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
        "operationId": "get-v1-companies-company_id-locations",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieves all company locations (addresses) associated with a company: mailing addresses, filing\naddresses, or work locations. A single address may serve multiple, or all, purposes.\n\nSince all company locations are subsets of locations, use the Locations endpoints to\n[get](https://docs.gusto.com/app-integrations/reference/get-v1-locations-location_id) or [update](https://docs.gusto.com/app-integrations/reference/put-v1-locations-location_id) an individual record.\n\nscope: `companies:read`",
        "tags": [
          "Locations"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Company-Locations-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Company-Locations-List"
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
