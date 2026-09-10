---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee form

Get an employee form

scope: `employee_forms:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employee Forms"
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
      "Form": {
        "title": "Form",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the form",
            "readOnly": true
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee to which the form belongs, if applicable.",
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
            "description": "The year of this form. For some forms, e.g. tax forms, this is the year which the form represents. A W2 for January - December 2022 would be delivered in January 2023 and have a year value of 2022. This value is nullable and will not be present on all forms.",
            "readOnly": true
          },
          "quarter": {
            "type": [
              "integer",
              "null"
            ],
            "description": "The quarter of this form. For some forms, e.g. tax forms, this is the calendar quarter which this form represents. An Employer's Quarterly Federal Tax Return (Form 941) for April, May, June 2022 would have a quarter value of 2 (and a year value of 2022). This value is nullable and will not be present on all forms.",
            "readOnly": true
          },
          "requires_signing": {
            "type": "boolean",
            "description": "A boolean flag that indicates whether the form needs signing or not. Note that this value will change after the form is signed.",
            "readOnly": true
          },
          "document_content_type": {
            "$ref": "#/components/schemas/Form-Document-Content-Type-Type"
          }
        },
        "x-examples": {
          "Example": {
            "uuid": "48cdd5ec-a4dd-4840-a424-ad79f38d8408",
            "name": "company_direct_deposit",
            "title": "Direct Deposit Authorization",
            "description": "We need you to sign paperwork to authorize us to debit and credit your bank account and file and pay your taxes.",
            "draft": false,
            "year": null,
            "quarter": null,
            "requires_signing": true,
            "document_content_type": "application/pdf"
          },
          "employee_form": {
            "uuid": "48cdd5ec-a4dd-4840-a424-ad79f38d8408",
            "employee_uuid": "c5fdae67-b148-4b52-8b33-1384024a1256",
            "name": "w4_federal",
            "title": "Form W-4: 2024",
            "description": "Form W-4 determines how much federal income tax your employer will withhold from your pay.",
            "draft": false,
            "year": 2024,
            "quarter": null,
            "requires_signing": true,
            "document_content_type": "application/pdf"
          },
          "quarterly_tax_form": {
            "uuid": "7a2b9f3e-1c4d-4e5f-8a6b-2d3e4f5a6b7c",
            "name": "form_941",
            "title": "Form 941: Q2 2024",
            "description": "Employer's Quarterly Federal Tax Return for the second quarter of 2024.",
            "draft": false,
            "year": 2024,
            "quarter": 2,
            "requires_signing": false,
            "document_content_type": "application/pdf"
          },
          "sandbox_w2": {
            "uuid": "bf5b2496-26df-436e-b465-eae4ed5c8021",
            "employee_uuid": "19394e76-a866-4570-b237-9a26b0163907",
            "name": "US_W-2",
            "title": "Draft Form W-2: 2021",
            "description": "Form W-2 records your annual wages and taxes.",
            "draft": true,
            "year": 2021,
            "quarter": null,
            "requires_signing": false,
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
    "/v1/employees/{employee_id}/forms/{form_id}": {
      "get": {
        "summary": "Get an employee form",
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
          },
          {
            "name": "form_id",
            "in": "path",
            "description": "The UUID of the form",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employee-form",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get an employee form\n\nscope: `employee_forms:read`",
        "tags": [
          "Employee Forms"
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
                  "employee_form": {
                    "value": {
                      "$ref": "#/components/schemas/Form/x-examples/employee_form"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Form"
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
