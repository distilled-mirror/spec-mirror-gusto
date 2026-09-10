---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Retrieve terms of service status for an admin

> Deprecated: use [PUT /v1/partner_managed_companies/{company_uuid}/terms_of_service](https://docs.gusto.com/embedded-payroll/reference/put-v1-partner-managed-companies-company-uuid-terms_of_service) for user-level status, or [GET /v1/partner_managed_companies/{company_uuid}/terms_of_service](https://docs.gusto.com/embedded-payroll/reference/get-v1-partner-managed-companies-company-uuid-terms_of_service) for company-level status.

Retrieve the user acceptance status of the Gusto Embedded Payroll's [Terms of Service](https://flows.gusto.com/terms).

scope: `terms_of_services:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Companies"
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
      "Partner-Managed-Company-Retrieve-Terms-Of-Service-Request": {
        "type": "object",
        "required": [
          "email"
        ],
        "properties": {
          "email": {
            "type": "string",
            "description": "The user's email address on Gusto. You can retrieve the user's email via company's `/admins`, `/employees`, `/signatories`, and `/contractors` endpoints."
          }
        },
        "x-examples": {
          "Example": {
            "email": "jsmith99@gmail.com"
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
    "/v1/partner_managed_companies/{company_uuid}/retrieve_terms_of_service": {
      "post": {
        "summary": "Retrieve terms of service status for an admin",
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
        "operationId": "post-partner-managed-companies-company_uuid-retrieve_terms_of_service",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "deprecated": true,
        "description": "> Deprecated: use [PUT /v1/partner_managed_companies/{company_uuid}/terms_of_service](https://docs.gusto.com/embedded-payroll/reference/put-v1-partner-managed-companies-company-uuid-terms_of_service) for user-level status, or [GET /v1/partner_managed_companies/{company_uuid}/terms_of_service](https://docs.gusto.com/embedded-payroll/reference/get-v1-partner-managed-companies-company-uuid-terms_of_service) for company-level status.\n\nRetrieve the user acceptance status of the Gusto Embedded Payroll's [Terms of Service](https://flows.gusto.com/terms).\n\nscope: `terms_of_services:read`",
        "tags": [
          "Companies"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "404": {
            "description": "Deprecated endpoint",
            "content": {
              "application/json": {
                "examples": {
                  "deprecated_retrieve_terms_of_service": {
                    "value": {
                      "$ref": "#/components/schemas/Not-Found-Error-Object/x-examples/deprecated_retrieve_terms_of_service"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Not-Found-Error-Object"
                }
              }
            }
          }
        },
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Partner-Managed-Company-Retrieve-Terms-Of-Service-Request"
              }
            }
          },
          "required": true
        }
      }
    }
  }
}
```
