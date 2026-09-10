---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee's I-9 verification document options

An employee's I-9 verification documents are the documents an employee has provided the employer to verify their identity and authorization to work in the United States. This endpoint returns the possible document options based on the employee's authorization status. These options can then be used to create the I-9 verification documents.

### Related guides
- [I-9 employment verification](doc:i-9-employment-verification)

scope: `i9_authorizations:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "I-9 Verification"
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
      "I9-Authorization-Document-Option": {
        "type": "object",
        "description": "An employee's I-9 verification document option based on the authorization status",
        "properties": {
          "section": {
            "type": "string",
            "description": "The document option's section in the list of acceptable documents on the Form I-9",
            "readOnly": true,
            "enum": [
              "A",
              "A1",
              "A2",
              "A3",
              "B",
              "C"
            ]
          },
          "description": {
            "type": "string",
            "description": "The document option's description",
            "readOnly": true
          },
          "document_type": {
            "type": "string",
            "description": "The document option's document type",
            "readOnly": true
          },
          "document_title": {
            "type": "array",
            "description": "The document option's document titles",
            "readOnly": true,
            "items": {
              "type": "string"
            }
          },
          "common_choice": {
            "type": "boolean",
            "description": "Whether the document is a common choice for I-9 verification",
            "readOnly": true
          }
        },
        "required": [
          "section",
          "description",
          "document_type",
          "document_title",
          "common_choice"
        ],
        "x-tags": [
          "I-9 Verification"
        ],
        "x-examples": {
          "example_a": {
            "section": "A",
            "description": "Foreign passport",
            "document_type": "foreign_passport_w_i94",
            "document_title": [
              "Foreign passport"
            ],
            "common_choice": true
          },
          "example_b": {
            "section": "B",
            "description": "Driver's license or state-issued ID card",
            "document_type": "driver_license",
            "document_title": [
              "Driver's license",
              "State ID card"
            ],
            "common_choice": true
          },
          "example_c": {
            "section": "C",
            "description": "Social Security card",
            "document_type": "ssn_card",
            "document_title": [
              "Social Security card"
            ],
            "common_choice": true
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
    "/v1/employees/{employee_id}/i9_authorization/document_options": {
      "get": {
        "summary": "Get an employee's I-9 verification document options",
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
        "operationId": "get-v1-employees-employee_id-i9_authorization-document_options",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "An employee's I-9 verification documents are the documents an employee has provided the employer to verify their identity and authorization to work in the United States. This endpoint returns the possible document options based on the employee's authorization status. These options can then be used to create the I-9 verification documents.\n\n### Related guides\n- [I-9 employment verification](https://docs.gusto.com/embedded-payroll/docs/i-9-employment-verification)\n\nscope: `i9_authorizations:read`",
        "tags": [
          "I-9 Verification"
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
                  "Example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/I9-Authorization-Document-Option/x-examples/example_a"
                      },
                      {
                        "$ref": "#/components/schemas/I9-Authorization-Document-Option/x-examples/example_b"
                      },
                      {
                        "$ref": "#/components/schemas/I9-Authorization-Document-Option/x-examples/example_c"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/I9-Authorization-Document-Option"
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
