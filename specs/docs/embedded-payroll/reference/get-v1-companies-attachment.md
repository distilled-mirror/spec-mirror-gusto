---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get Company Attachment Details

Retrieve the detail of an attachment uploaded by the company.

### Related guides
- [Manage company attachments](doc:manage-company-attachments)

scope: `company_attachments:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Company Attachment"
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
      "Company-Attachment": {
        "description": "The company attachment",
        "type": "object",
        "required": [
          "uuid",
          "name",
          "category",
          "upload_time"
        ],
        "x-examples": {
          "success_status": {
            "uuid": "1263eae5-4411-48d9-bd6d-18ed93082e65",
            "name": "Company_Attachment_File.pdf",
            "category": "gep_notice",
            "upload_time": "2024-09-10T01:54:20Z"
          },
          "compliance_attachment": {
            "uuid": "987058cc-23ee-46e9-81ef-5cee086cceca",
            "name": "Compliance_Document.pdf",
            "category": "compliance",
            "upload_time": "2024-10-15T14:30:00Z"
          }
        },
        "x-tags": [
          "Company Attachment"
        ],
        "properties": {
          "uuid": {
            "type": "string",
            "description": "UUID of the company attachment"
          },
          "name": {
            "type": "string",
            "description": "name of the file uploaded"
          },
          "category": {
            "type": "string",
            "description": "The category of the company attachment.\n- `gep_notice`: A tax notice attachment\n- `compliance`: A compliance attachment\n- `other`: Any other attachment type\n",
            "enum": [
              "gep_notice",
              "compliance",
              "other"
            ]
          },
          "upload_time": {
            "type": "string",
            "description": "The ISO 8601 timestamp of when an attachment was uploaded"
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
    "/v1/companies/{company_id}/attachments/{company_attachment_uuid}": {
      "get": {
        "summary": "Get Company Attachment Details",
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
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "company_attachment_uuid",
            "in": "path",
            "description": "The UUID of the company attachment",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-attachment",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieve the detail of an attachment uploaded by the company.\n\n### Related guides\n- [Manage company attachments](https://docs.gusto.com/embedded-payroll/docs/manage-company-attachments)\n\nscope: `company_attachments:read`",
        "tags": [
          "Company Attachment"
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
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Company-Attachment/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Company-Attachment"
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
