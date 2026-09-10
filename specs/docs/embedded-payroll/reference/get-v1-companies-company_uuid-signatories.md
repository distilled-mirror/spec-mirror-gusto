---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get the signatories for a company

Returns the signatories for a company. A company has at most one signatory.

## Related guides
- [Signatory Events](doc:signatory-events)

scope: `signatories:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Signatories"
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
      "Signatory": {
        "description": "The representation of a company's signatory",
        "type": "object",
        "title": "Signatory",
        "x-tags": [
          "Signatories"
        ],
        "properties": {
          "uuid": {
            "type": "string"
          },
          "first_name": {
            "type": [
              "string",
              "null"
            ]
          },
          "last_name": {
            "type": [
              "string",
              "null"
            ]
          },
          "title": {
            "type": [
              "string",
              "null"
            ]
          },
          "phone": {
            "type": [
              "string",
              "null"
            ]
          },
          "email": {
            "type": "string"
          },
          "birthday": {
            "type": [
              "string",
              "null"
            ]
          },
          "is_admin": {
            "type": "boolean",
            "description": "Whether or not the signatory is also the payroll admin of the company."
          },
          "has_ssn": {
            "type": "boolean",
            "description": "Indicates whether the signatory has an SSN in Gusto."
          },
          "version": {
            "type": "string",
            "description": "The current version of the signatory. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "identity_verification_status": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "Pass",
                  "Fail",
                  "Skipped"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "|   |   |\n|---|---|\n|__Status__| __Description__ |\n| Pass | Signatory can sign all forms |\n| Fail | Signatory cannot sign forms |\n| Skipped | Signatory cannot sign Form 8655 until the form is manually uploaded as wet-signed |\n| null | Identity verification process has not been completed |"
          },
          "home_address": {
            "type": [
              "object",
              "null"
            ],
            "properties": {
              "street_1": {
                "type": "string"
              },
              "street_2": {
                "type": "string"
              },
              "city": {
                "type": "string"
              },
              "state": {
                "type": "string"
              },
              "zip": {
                "type": "string"
              },
              "country": {
                "type": "string",
                "default": "USA"
              }
            }
          }
        },
        "required": [
          "uuid"
        ],
        "x-examples": {
          "typical_signatory": {
            "uuid": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "first_name": "Bob",
            "last_name": "Jones",
            "title": "CEO",
            "phone": "4156051234",
            "email": "bob@example.com",
            "birthday": "1980-08-04",
            "is_admin": true,
            "has_ssn": true,
            "version": "e1bdd845a493c74908f8e15d6114169b",
            "identity_verification_status": "Skipped",
            "home_address": null
          },
          "signatory_with_address": {
            "uuid": "8c2e1ef2-7514-5b17-9879-d2ee8e35e38b",
            "first_name": "Rachel",
            "last_name": "Greene",
            "title": "Onboarding specialist",
            "phone": "4155551234",
            "email": "rachel@example.com",
            "birthday": null,
            "is_admin": false,
            "has_ssn": false,
            "version": "def456",
            "identity_verification_status": null,
            "home_address": {
              "street_1": "525 20th Street",
              "street_2": "Apt. 1",
              "city": "San Francisco",
              "state": "CA",
              "zip": "94107",
              "country": "USA"
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
    "/v1/companies/{company_uuid}/signatories": {
      "get": {
        "summary": "Get the signatories for a company",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_uuid-signatories",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns the signatories for a company. A company has at most one signatory.\n\n## Related guides\n- [Signatory Events](https://docs.gusto.com/embedded-payroll/docs/signatory-events)\n\nscope: `signatories:read`",
        "tags": [
          "Signatories"
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
                  "typical_signatory": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Signatory/x-examples/typical_signatory"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Signatory"
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
