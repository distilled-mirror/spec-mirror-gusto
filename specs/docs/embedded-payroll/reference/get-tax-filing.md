---
updatedAt: 2026-11-25T22:59:39.000Z
agentTools:
  siteIndex: https://docs.gusto.com/llms.txt
  projectIndex: https://docs.gusto.com/embedded-payroll/llms.txt
---

# Get a tax filing for a company

Fetches a single tax filing obligation for a company by UUID.

scope: `tax_filings:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Tax Filings"
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
      "Tax-Filing": {
        "type": "object",
        "description": "Representation of a tax filing obligation",
        "x-examples": {
          "example": {
            "uuid": "11111111-1111-1111-1111-111111111111",
            "company_uuid": "f0e1d2c3-b4a5-6789-0fed-cba987654321",
            "form_title": "Quarterly Contribution Return and Report of Wages",
            "jurisdiction": "CA",
            "agency_name": "California Employment Development Department (EDD)",
            "period": "Q1 2026",
            "period_start": "2026-01-01",
            "period_end": "2026-03-31",
            "due_date": "2026-04-30",
            "successfully_filed_on": "",
            "is_amendment": false,
            "amends_filing_uuid": "",
            "status": "failed",
            "form_uuid": ""
          },
          "amended_filing": {
            "uuid": "55555555-5555-5555-5555-555555555555",
            "company_uuid": "f0e1d2c3-b4a5-6789-0fed-cba987654321",
            "form_title": "Quarterly Contribution Return and Report of Wages",
            "jurisdiction": "CA",
            "agency_name": "California Employment Development Department (EDD)",
            "period": "Q1 2026",
            "period_start": "2026-01-01",
            "period_end": "2026-03-31",
            "due_date": "2026-04-30",
            "successfully_filed_on": "2026-05-08",
            "is_amendment": true,
            "amends_filing_uuid": "11111111-1111-1111-1111-111111111111",
            "status": "accepted",
            "form_uuid": ""
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "format": "uuid",
            "description": "Unique identifier of the tax filing"
          },
          "company_uuid": {
            "type": "string",
            "format": "uuid",
            "description": "Unique identifier of the company to which the tax filing belongs"
          },
          "form_title": {
            "type": "string",
            "description": "The human-readable title of the tax form associated with this filing"
          },
          "jurisdiction": {
            "type": [
              "string",
              "null"
            ],
            "pattern": "^[A-Z]{2}$",
            "description": "The tax jurisdiction this filing is for. A two-letter state code, or US for federal."
          },
          "agency_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The name of the tax agency this filing is submitted to"
          },
          "period": {
            "type": [
              "string",
              "null"
            ],
            "description": "Humanized representation of the filing period (e.g. \"Q1 2026\", \"2026\", \"December 2026\")"
          },
          "period_start": {
            "type": [
              "string",
              "null"
            ],
            "format": "date",
            "description": "The start date of the period this filing covers"
          },
          "period_end": {
            "type": [
              "string",
              "null"
            ],
            "format": "date",
            "description": "The end date of the period this filing covers"
          },
          "due_date": {
            "type": [
              "string",
              "null"
            ],
            "format": "date",
            "description": "The date this filing is due"
          },
          "successfully_filed_on": {
            "type": [
              "string",
              "null"
            ],
            "format": "date",
            "description": "The date the filing was successfully filed with the tax agency. Null until then, and null while the filing's latest attempt is not a success, for example during a refile."
          },
          "is_amendment": {
            "type": "boolean",
            "description": "Whether this filing is an amendment to a previously filed filing"
          },
          "amends_filing_uuid": {
            "type": [
              "string",
              "null"
            ],
            "format": "uuid",
            "description": "The unique identifier of the filing this filing amends, if is_amendment is true"
          },
          "status": {
            "type": "string",
            "description": "The current status of the tax filing",
            "enum": [
              "not_started",
              "in_progress",
              "blocked",
              "accepted",
              "not_required",
              "failed",
              "unknown"
            ]
          },
          "form_uuid": {
            "type": [
              "string",
              "null"
            ],
            "format": "uuid",
            "description": "Unique identifier of the rendered PDF form for this filing, if one has been generated. Fetch the PDF via GET /v1/forms/{form_uuid}/pdf"
          }
        },
        "required": [
          "uuid",
          "company_uuid",
          "form_title",
          "jurisdiction",
          "agency_name",
          "period",
          "period_start",
          "period_end",
          "due_date",
          "successfully_filed_on",
          "is_amendment",
          "amends_filing_uuid",
          "status",
          "form_uuid"
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
    "/v1/companies/{company_uuid}/tax_filings/{uuid}": {
      "get": {
        "summary": "Get a tax filing for a company",
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
            "required": true,
            "description": "The UUID of the company",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "uuid",
            "in": "path",
            "required": true,
            "description": "The UUID of the tax filing",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-tax-filing",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Fetches a single tax filing obligation for a company by UUID.\n\nscope: `tax_filings:read`",
        "tags": [
          "Tax Filings"
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
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Filing/x-examples/example"
                    }
                  },
                  "amended_filing": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Filing/x-examples/amended_filing"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Tax-Filing"
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
