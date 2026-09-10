---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all contractor forms

Get a list of all contractor's forms

scope: `contractor_forms:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractor Forms"
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
      "Form-Document-Content-Type-Type": {
        "type": [
          "string",
          "null"
        ],
        "description": "The content type of the associated document. Most forms are PDFs with a content type of `application/pdf`. Some tax file packages will be zip files (containing PDFs) with a content type of `application/zip`. This attribute will be `null` when the document has not been prepared.",
        "readOnly": true
      },
      "Form_1099": {
        "title": "Form",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the form",
            "readOnly": true
          },
          "name": {
            "type": "string",
            "description": "The type identifier of the form",
            "readOnly": true
          },
          "title": {
            "type": "string",
            "description": "The title of the form",
            "readOnly": true
          },
          "description": {
            "type": "string",
            "description": "The description of the form",
            "readOnly": true
          },
          "draft": {
            "type": "boolean",
            "description": "If the form is in a draft state. E.g. End of year tax forms may be provided in a draft state prior to being finalized.",
            "readOnly": true
          },
          "year": {
            "type": [
              "integer",
              "null"
            ],
            "description": "The year of this form. For some forms, e.g. tax forms, this is the year which the form represents. A 1099 for January - December 2022 would be delivered in January 2023 and have a year value of 2022. This value is nullable and will not be present on all forms.",
            "readOnly": true
          },
          "quarter": {
            "type": [
              "integer",
              "null"
            ],
            "description": "The quarter of this form. This value is currently always null since it is not present on any contractor forms.",
            "readOnly": true
          },
          "requires_signing": {
            "type": "boolean",
            "description": "A boolean flag that indicates whether the form needs signing or not. Note that this value will change after the form is signed.",
            "readOnly": true
          },
          "document_content_type": {
            "$ref": "#/components/schemas/Form-Document-Content-Type-Type"
          },
          "contractor_uuid": {
            "type": "string",
            "description": "The contractor UUID",
            "readOnly": true
          }
        },
        "x-examples": {
          "Example": {
            "uuid": "48cdd5ec-a4dd-4840-a424-ad79f38d8408",
            "name": "US_1099",
            "title": "Form 1099: 2020",
            "description": "Form 1099 records your annual income as a contractor.",
            "draft": false,
            "requires_signing": false,
            "year": 2020,
            "quarter": null,
            "document_content_type": "application/pdf",
            "contractor_uuid": "123dd616-6dbc-4724-938a-403f6217a933"
          },
          "sandbox_1099": {
            "uuid": "29afb141-2256-431d-90e0-1c7344222342",
            "contractor_uuid": "b68484a9-4487-4ee5-bafc-4245133a426c",
            "name": "US_1099",
            "title": "Form 1099: 2022",
            "description": "Form 1099 records your annual income as a contractor.",
            "draft": true,
            "requires_signing": false,
            "year": 2022,
            "quarter": null,
            "document_content_type": "application/pdf"
          }
        },
        "x-tags": [
          "Forms"
        ],
        "required": [
          "uuid"
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
    "/v1/contractors/{contractor_uuid}/forms": {
      "get": {
        "summary": "Get all contractor forms",
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
            "name": "contractor_uuid",
            "in": "path",
            "description": "The UUID of the contractor",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-contractor-forms",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get a list of all contractor's forms\n\nscope: `contractor_forms:read`",
        "tags": [
          "Contractor Forms"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Example response",
            "content": {
              "application/json": {
                "examples": {
                  "Example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Form_1099/x-examples/Example"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Form_1099"
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
