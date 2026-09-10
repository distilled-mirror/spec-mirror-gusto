---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee's I-9 authorization

An employee's I-9 authorization stores information about an employee's authorization status and I-9 signatures, information required to fill out the Form I-9 for employment eligibility verification.

**NOTE:** The `form_uuid` in responses from this endpoint can be used to retrieve the PDF version of the I-9. See the "get employee form PDF" request for more details.

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
      "I9-Authorization": {
        "type": "object",
        "description": "An employee's I-9 authorization",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the I-9 authorization",
            "readOnly": true
          },
          "form_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the Form associated with this I-9 authorization. Use this with \"Employee Forms\" API endpoints.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field.",
            "readOnly": true
          },
          "authorization_status": {
            "type": "string",
            "description": "The employee's authorization status",
            "enum": [
              "citizen",
              "noncitizen",
              "permanent_resident",
              "alien"
            ]
          },
          "document_type": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "uscis_alien_registration_number",
                  "form_i94",
                  "foreign_passport"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The document's document type"
          },
          "has_document_number": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether or not a `document_number` exists for this document."
          },
          "expiration_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "The document's expiration date"
          },
          "country": {
            "type": [
              "string",
              "null"
            ],
            "description": "The document's country of issuance"
          },
          "employer_signed": {
            "type": "boolean",
            "description": "Whether the employer has signed the Form I-9",
            "readOnly": true
          },
          "employee_signed": {
            "type": "boolean",
            "description": "Whether the employee has signed the Form I-9",
            "readOnly": true
          },
          "additional_info": {
            "type": [
              "string",
              "null"
            ],
            "description": "Any additional notes"
          },
          "alt_procedure": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether an alternative procedure authorized by DHS to examine documents was used"
          }
        },
        "required": [
          "uuid",
          "version",
          "authorization_status",
          "employer_signed",
          "employee_signed"
        ],
        "x-tags": [
          "I-9 Verification"
        ],
        "x-examples": {
          "alien_with_foreign_passport": {
            "uuid": "7f2337f9-9b78-44b9-aeed-be4777b833a8",
            "version": "6ae7ff720107b356bf13b1606f60b24f",
            "form_uuid": "c54046f7-1be4-4c54-8194-f4842c30c86d",
            "authorization_status": "alien",
            "document_type": "foreign_passport",
            "has_document_number": true,
            "expiration_date": "2028-01-01",
            "country": "Canada",
            "employer_signed": false,
            "employee_signed": false,
            "additional_info": null,
            "alt_procedure": null
          },
          "citizen_authorization": {
            "uuid": "a12bc345-6789-4def-abcd-ef0123456789",
            "version": "52b7c567242cb7393b2a206ed6a86afcb",
            "form_uuid": null,
            "authorization_status": "citizen",
            "document_type": null,
            "has_document_number": false,
            "expiration_date": null,
            "country": null,
            "employer_signed": false,
            "employee_signed": false,
            "additional_info": null,
            "alt_procedure": null
          },
          "employer_signed_authorization": {
            "uuid": "7f2337f9-9b78-44b9-aeed-be4777b833a8",
            "version": "8bc7393b2a206ed6a86afcb4d00c1785",
            "form_uuid": "c54046f7-1be4-4c54-8194-f4842c30c86d",
            "authorization_status": "citizen",
            "document_type": null,
            "has_document_number": false,
            "expiration_date": null,
            "country": null,
            "employer_signed": true,
            "employee_signed": true,
            "additional_info": "Additional info",
            "alt_procedure": false
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
    "/v1/employees/{employee_id}/i9_authorization": {
      "get": {
        "summary": "Get an employee's I-9 authorization",
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
        "operationId": "get-v1-employees-employee_id-i9_authorization",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "An employee's I-9 authorization stores information about an employee's authorization status and I-9 signatures, information required to fill out the Form I-9 for employment eligibility verification.\n\n**NOTE:** The `form_uuid` in responses from this endpoint can be used to retrieve the PDF version of the I-9. See the \"get employee form PDF\" request for more details.\n\n### Related guides\n- [I-9 employment verification](https://docs.gusto.com/embedded-payroll/docs/i-9-employment-verification)\n\nscope: `i9_authorizations:read`",
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
                  "alien_with_foreign_passport": {
                    "value": {
                      "$ref": "#/components/schemas/I9-Authorization/x-examples/alien_with_foreign_passport"
                    }
                  },
                  "citizen_authorization": {
                    "value": {
                      "$ref": "#/components/schemas/I9-Authorization/x-examples/citizen_authorization"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/I9-Authorization"
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
