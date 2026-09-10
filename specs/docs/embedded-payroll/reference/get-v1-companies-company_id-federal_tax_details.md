---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a company's federal tax details

Retrieves a company's federal tax details including EIN verification status, tax payer type, filing form, and other federal tax configuration.

scope: `company_federal_taxes:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Federal Tax Details"
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
      "Federal-Tax-Details": {
        "title": "Federal-Tax-Details",
        "type": "object",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "tax_payer_type": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "C-Corporation",
                  "S-Corporation",
                  "Sole proprietor",
                  "LLC",
                  "LLP",
                  "Limited partnership",
                  "Co-ownership",
                  "Association",
                  "Trusteeship",
                  "General partnership",
                  "Joint venture",
                  "Non-Profit"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "What type of tax entity the company is. One of:\n- C-Corporation\n- S-Corporation\n- Sole proprietor\n- LLC\n- LLP\n- Limited partnership\n- Co-ownership\n- Association\n- Trusteeship\n- General partnership\n- Joint venture\n- Non-Profit"
          },
          "taxable_as_scorp": {
            "type": "boolean",
            "description": "Whether the company is taxed as an S-Corporation. Tax payer types that may be taxed as an S-Corporation include:\n- S-Corporation\n- C-Corporation\n- LLC"
          },
          "filing_form": {
            "type": "string",
            "enum": [
              "941",
              "944"
            ],
            "description": "The form used by the company for federal tax filing. One of:\n- 941 (Quarterly federal tax return form)\n- 944 (Annual federal tax return form)"
          },
          "has_ein": {
            "type": "boolean",
            "description": "Whether company's Employer Identification Number (EIN) is present"
          },
          "ein_verified": {
            "type": "boolean",
            "description": "Whether the EIN has been successfully verified as a valid EIN with the IRS."
          },
          "ein_verification": {
            "type": "object",
            "nullable": false,
            "description": "Information about the status of verifying the company's Employer Identification Number (EIN)",
            "properties": {
              "status": {
                "type": "string",
                "nullable": false,
                "enum": [
                  "pending",
                  "verified",
                  "failed"
                ],
                "description": "The status of EIN verification:\n- `pending`: The EIN verification process has not completed (or the company does not yet have an EIN).\n- `verified`: The EIN has been successfully verified as a valid EIN with the IRS.\n- `failed`: The company's EIN did not pass verification. Common issues are being entered incorrectly or not matching the company's legal name."
              }
            }
          },
          "legal_name": {
            "type": "string",
            "description": "The legal name of the company"
          },
          "effective_date": {
            "type": "string",
            "description": "The date that these details took effect."
          },
          "deposit_schedule": {
            "type": "string",
            "description": "How often the company sends money to the IRS. One of:\n  - Semiweekly\n  - Monthly"
          }
        },
        "x-examples": {
          "Success": {
            "version": "68934a3e9455fa72420237eb",
            "tax_payer_type": "S-Corporation",
            "taxable_as_scorp": true,
            "filing_form": "941",
            "has_ein": true,
            "ein_verified": true,
            "ein_verification": {
              "status": "verified"
            },
            "legal_name": "Acme Corp",
            "effective_date": "2024-01-01",
            "deposit_schedule": "Semiweekly"
          }
        },
        "x-tags": [
          "Federal Tax Details"
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
    "/v1/companies/{company_id}/federal_tax_details": {
      "get": {
        "summary": "Get a company's federal tax details",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-federal_tax_details",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieves a company's federal tax details including EIN verification status, tax payer type, filing form, and other federal tax configuration.\n\nscope: `company_federal_taxes:read`",
        "tags": [
          "Federal Tax Details"
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
                  "Success": {
                    "value": {
                      "$ref": "#/components/schemas/Federal-Tax-Details/x-examples/Success"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Federal-Tax-Details"
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
