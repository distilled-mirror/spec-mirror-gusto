---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get the contractor's onboarding status

Retrieves a contractor's onboarding status. The data returned helps inform the required onboarding steps and respective completion status.

## onboarding_status

### Admin-facilitated onboarding
| onboarding_status | Description |
|:------------------|------------:|
| `admin_onboarding_incomplete` | Admin needs to enter basic information about the contractor. |
| `admin_onboarding_review` | All information has been completed and admin needs to confirm onboarding. |
| `onboarding_completed` | Contractor has been fully onboarded and verified. |

### Contractor self-onboarding

| onboarding_status | Description |
| --- | ----------- |
| `admin_onboarding_incomplete` | Admin needs to enter basic information about the contractor. |
| `self_onboarding_not_invited` | Admin has the intention to invite the contractor to self-onboard (e.g., marking a checkbox), but the system has not yet sent the invitation. |
| `self_onboarding_invited` | Contractor has been sent an invitation to self-onboard. |
| `self_onboarding_started` | Contractor has started the self-onboarding process. |
| `self_onboarding_review` | Admin needs to review contractors's entered information and confirm onboarding. |
| `onboarding_completed` | Contractor has been fully onboarded and verified. |

## onboarding_steps

| onboarding_steps | Requirement(s) to be completed |
|:-----------------|-------------------------------:|
| `basic_details` | Add individual contractor's first name, last name, social security number or Business name and EIN depending on the contractor type |
| `add_address` | Add contractor address. |
| `compensation_details` | Add contractor compensation. |
| `payment_details` | (optional) Set up contractor's direct deposit or set to check. |
| `sign_documents` | Contractor forms (e.g., W9) are generated & signed. |
| `file_new_hire_report` | Contractor new hire report is generated. |

scope: `contractors:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractors"
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
      "Contractor-Onboarding-Status": {
        "description": "The representation of an contractor's onboarding status.",
        "type": "object",
        "title": "Contractor-Onboarding-Status",
        "x-tags": [
          "Contractor"
        ],
        "x-examples": {
          "example": {
            "uuid": "bc57832c-d8bc-43a7-ae99-3a03380ff037",
            "onboarding_status": "admin_onboarding_incomplete",
            "onboarding_steps": [
              {
                "title": "Basic details",
                "id": "basic_details",
                "required": true,
                "completed": false,
                "requirements": []
              },
              {
                "title": "Enter compensation details",
                "id": "compensation_details",
                "required": true,
                "completed": false,
                "requirements": []
              },
              {
                "title": "Add an address",
                "id": "add_address",
                "required": true,
                "completed": false,
                "requirements": []
              },
              {
                "title": "Payment details",
                "id": "payment_details",
                "required": true,
                "completed": false,
                "requirements": []
              },
              {
                "title": "Sign and acknowledge documents",
                "id": "sign_documents",
                "required": false,
                "completed": false,
                "requirements": [
                  "basic_details",
                  "add_address"
                ]
              },
              {
                "title": "File new hire report",
                "id": "file_new_hire_report",
                "required": false,
                "completed": false,
                "requirements": [
                  "basic_details"
                ]
              }
            ]
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier for this contractor."
          },
          "onboarding_status": {
            "type": "string",
            "description": "One of the \"onboarding_status\" enum values.",
            "enum": [
              "onboarding_completed",
              "admin_onboarding_review",
              "admin_onboarding_incomplete",
              "self_onboarding_not_invited",
              "self_onboarding_invited",
              "self_onboarding_started",
              "self_onboarding_review"
            ]
          },
          "onboarding_steps": {
            "type": "array",
            "description": "List of steps required to onboard a contractor.",
            "items": {
              "title": "Onboarding step",
              "type": "object",
              "properties": {
                "title": {
                  "type": "string",
                  "description": "User-friendly description of the onboarding step."
                },
                "id": {
                  "type": "string",
                  "description": "String identifier for the onboarding step."
                },
                "required": {
                  "type": "boolean",
                  "description": "When true, this step is required."
                },
                "completed": {
                  "type": "boolean",
                  "description": "When true, this step has been completed."
                },
                "requirements": {
                  "type": "array",
                  "description": "A list of onboarding steps required to begin this step.",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        },
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
    "/v1/contractors/{contractor_uuid}/onboarding_status": {
      "get": {
        "summary": "Get the contractor's onboarding status",
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
        "operationId": "get-v1-contractors-contractor_uuid-onboarding_status",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieves a contractor's onboarding status. The data returned helps inform the required onboarding steps and respective completion status.\n\n## onboarding_status\n\n### Admin-facilitated onboarding\n| onboarding_status | Description |\n|:------------------|------------:|\n| `admin_onboarding_incomplete` | Admin needs to enter basic information about the contractor. |\n| `admin_onboarding_review` | All information has been completed and admin needs to confirm onboarding. |\n| `onboarding_completed` | Contractor has been fully onboarded and verified. |\n\n### Contractor self-onboarding\n\n| onboarding_status | Description |\n| --- | ----------- |\n| `admin_onboarding_incomplete` | Admin needs to enter basic information about the contractor. |\n| `self_onboarding_not_invited` | Admin has the intention to invite the contractor to self-onboard (e.g., marking a checkbox), but the system has not yet sent the invitation. |\n| `self_onboarding_invited` | Contractor has been sent an invitation to self-onboard. |\n| `self_onboarding_started` | Contractor has started the self-onboarding process. |\n| `self_onboarding_review` | Admin needs to review contractors's entered information and confirm onboarding. |\n| `onboarding_completed` | Contractor has been fully onboarded and verified. |\n\n## onboarding_steps\n\n| onboarding_steps | Requirement(s) to be completed |\n|:-----------------|-------------------------------:|\n| `basic_details` | Add individual contractor's first name, last name, social security number or Business name and EIN depending on the contractor type |\n| `add_address` | Add contractor address. |\n| `compensation_details` | Add contractor compensation. |\n| `payment_details` | (optional) Set up contractor's direct deposit or set to check. |\n| `sign_documents` | Contractor forms (e.g., W9) are generated & signed. |\n| `file_new_hire_report` | Contractor new hire report is generated. |\n\nscope: `contractors:read`",
        "tags": [
          "Contractors"
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
                  "example": {
                    "value": {
                      "$ref": "#/components/schemas/Contractor-Onboarding-Status/x-examples/example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Contractor-Onboarding-Status"
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
