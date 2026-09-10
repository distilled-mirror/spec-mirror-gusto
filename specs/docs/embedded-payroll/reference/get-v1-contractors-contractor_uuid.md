---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a contractor

Get a contractor.

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
      "Contractor": {
        "description": "The representation of a contractor (individual or business) in Gusto.",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the contractor in Gusto.",
            "readOnly": true
          },
          "company_uuid": {
            "type": "string",
            "description": "The UUID of the company the contractor is employed by.",
            "readOnly": true
          },
          "wage_type": {
            "type": "string",
            "enum": [
              "Fixed",
              "Hourly"
            ],
            "description": "The contractor's wage type, either \"Fixed\" or \"Hourly\"."
          },
          "is_active": {
            "type": "boolean",
            "default": true,
            "description": "The status of the contractor with the company.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "type": {
            "type": "string",
            "enum": [
              "Individual",
              "Business"
            ],
            "description": "The contractor's type, either \"Individual\" or \"Business\". "
          },
          "first_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The contractor’s first name. This attribute is required for “Individual” contractors and will be ignored for “Business” contractors."
          },
          "last_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The contractor’s last name. This attribute is required for “Individual” contractors and will be ignored for “Business” contractors."
          },
          "middle_initial": {
            "type": [
              "string",
              "null"
            ],
            "description": "The contractor’s middle initial. This attribute is optional for “Individual” contractors and will be ignored for “Business” contractors."
          },
          "business_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The name of the contractor business. This attribute is required for “Business” contractors and will be ignored for “Individual” contractors."
          },
          "ein": {
            "type": [
              "string",
              "null"
            ],
            "description": "The Federal Employer Identification Number of the contractor business. This attribute is optional for “Business” contractors and will be ignored for “Individual” contractors."
          },
          "has_ein": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether company's Employer Identification Number (EIN) is present"
          },
          "email": {
            "type": [
              "string",
              "null"
            ],
            "description": "The contractor’s email address. This attribute is optional for “Individual” contractors and will be ignored for “Business” contractors. "
          },
          "work_email": {
            "type": [
              "string",
              "null"
            ],
            "description": "The work email address of the contractor. This is provided to support syncing users between our system and yours. You may not use this email address for any other purpose (e.g. marketing)."
          },
          "start_date": {
            "type": "string",
            "description": "The contractor's start date.",
            "readOnly": true
          },
          "address": {
            "type": [
              "object",
              "null"
            ],
            "description": "The contractor’s home address.",
            "properties": {
              "street_1": {
                "type": "string",
                "readOnly": true
              },
              "street_2": {
                "type": [
                  "string",
                  "null"
                ],
                "readOnly": true
              },
              "city": {
                "type": "string",
                "readOnly": true
              },
              "state": {
                "type": "string",
                "readOnly": true
              },
              "zip": {
                "type": "string",
                "readOnly": true
              },
              "country": {
                "type": "string",
                "readOnly": true
              }
            },
            "readOnly": true
          },
          "hourly_rate": {
            "type": "string",
            "example": "50.0",
            "description": "The contractor’s hourly rate. This attribute is required if the wage_type is “Hourly”."
          },
          "file_new_hire_report": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "The boolean flag indicating whether Gusto will file a new hire report for the contractor"
          },
          "work_state": {
            "type": [
              "string",
              "null"
            ],
            "description": "State where the contractor will be conducting the majority of their work for the company.\nThis value is used when generating the new hire report."
          },
          "onboarded": {
            "type": "boolean",
            "description": "The updated onboarding status for the contractor"
          },
          "onboarding_status": {
            "type": "string",
            "description": "One of the \"onboarding_status\" enum values.",
            "enum": [
              "admin_onboarding_incomplete",
              "admin_onboarding_review",
              "self_onboarding_not_invited",
              "self_onboarding_invited",
              "self_onboarding_started",
              "self_onboarding_review",
              "onboarding_completed"
            ]
          },
          "payment_method": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "Direct Deposit",
                  "Check"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The contractor's payment method."
          },
          "has_ssn": {
            "type": "boolean",
            "description": "Indicates whether the contractor has an SSN in Gusto."
          },
          "department_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the department the contractor is under"
          },
          "department": {
            "type": [
              "string",
              "null"
            ],
            "description": "The contractor's department in the company.",
            "readOnly": true
          },
          "department_title": {
            "type": [
              "string",
              "null"
            ],
            "description": "The title of the contractor's department.",
            "readOnly": true
          },
          "dismissal_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "The contractor's dismissal date.",
            "readOnly": true
          },
          "upcoming_employment": {
            "type": [
              "object",
              "null"
            ],
            "description": "The contractor's upcoming employment details, if a rehire is scheduled.",
            "readOnly": true,
            "properties": {
              "start_date": {
                "type": "string",
                "description": "The start date of the upcoming employment."
              },
              "setup_status": {
                "type": [
                  "string",
                  "null"
                ],
                "description": "The setup status of the upcoming employment."
              }
            }
          },
          "dismissal_cancellation_eligible": {
            "type": "boolean",
            "description": "Whether the contractor's pending dismissal can be cancelled.",
            "readOnly": true
          },
          "rehire_cancellation_eligible": {
            "type": "boolean",
            "description": "Whether the contractor's pending rehire can be cancelled.",
            "readOnly": true
          },
          "member_portal_invitation_status": {
            "type": [
              "object",
              "null"
            ],
            "description": "Member portal invitation status information. Only included when the include param has the portal_invitations value set.",
            "properties": {
              "status": {
                "type": "string",
                "description": "The current status of the member portal invitation.",
                "enum": [
                  "pending",
                  "sent",
                  "verified",
                  "complete",
                  "cancelled"
                ]
              },
              "token_expired": {
                "type": [
                  "boolean",
                  "null"
                ],
                "description": "Whether the invitation token has expired."
              },
              "welcome_email_sent_at": {
                "type": [
                  "string",
                  "null"
                ],
                "format": "date-time",
                "description": "The date and time when the welcome email was sent."
              },
              "last_password_resent_at": {
                "type": [
                  "string",
                  "null"
                ],
                "format": "date-time",
                "description": "The date and time when the password reset was last resent."
              }
            }
          },
          "partner_portal_invitation_sent": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether an external partner portal invitation webhook has been sent for this contractor. Only included when the include param has the portal_invitations value set."
          }
        },
        "x-tags": [
          "Contractors"
        ],
        "required": [
          "uuid"
        ],
        "x-examples": {
          "Individual Contractor": {
            "uuid": "c9fc1ad3-c107-4e7b-aa21-2dd4b00a7a07",
            "company_uuid": "b7457fec-3b76-43bb-9c6e-69cca4688942",
            "wage_type": "Hourly",
            "start_date": "2022-01-01",
            "is_active": true,
            "version": "63859768485e218ccf8a449bb60f14ed",
            "type": "Individual",
            "first_name": "Kory",
            "last_name": "Gottlieb",
            "middle_initial": "P",
            "business_name": null,
            "ein": null,
            "has_ein": false,
            "has_ssn": true,
            "department_uuid": "56260b3d-c375-415c-b77a-75d99f717193",
            "email": "keira.west@mckenzie.org",
            "file_new_hire_report": true,
            "work_state": "FL",
            "onboarded": true,
            "onboarding_status": "onboarding_completed",
            "address": {
              "street_1": "621 Jast Row",
              "street_2": "Apt. 281",
              "city": "Coral Springs",
              "state": "FL",
              "zip": "33065",
              "country": "USA"
            },
            "hourly_rate": "60.00",
            "payment_method": "Direct Deposit",
            "department": "Engineering",
            "department_title": "Engineering",
            "dismissal_date": null,
            "upcoming_employment": null,
            "dismissal_cancellation_eligible": false,
            "rehire_cancellation_eligible": false,
            "member_portal_invitation_status": {
              "status": "sent",
              "token_expired": false,
              "welcome_email_sent_at": "2024-01-15T14:30:00Z",
              "last_password_resent_at": null
            },
            "partner_portal_invitation_sent": true
          },
          "Business Contractor": {
            "uuid": "c7c0659c-21a6-4b4e-b74c-9252576fc68c",
            "company_uuid": "0ec4ae6e-e436-460d-b63c-94a14503d16f",
            "wage_type": "Fixed",
            "start_date": "2022-01-01",
            "is_active": true,
            "version": "8aab307f1e8ed788697f8986346af559",
            "type": "Business",
            "first_name": null,
            "last_name": null,
            "middle_initial": null,
            "business_name": "Labadie-Stroman",
            "ein": "XX-XXX0001",
            "has_ein": true,
            "has_ssn": false,
            "email": "jonatan@kerluke.info",
            "file_new_hire_report": false,
            "work_state": null,
            "onboarded": true,
            "onboarding_status": "onboarding_completed",
            "address": {
              "street_1": "1625 Bednar Center",
              "street_2": "Apt. 480",
              "city": "Port Charlotte",
              "state": "FL",
              "zip": "33954",
              "country": "USA"
            },
            "hourly_rate": "0.00",
            "payment_method": "Direct Deposit",
            "department_uuid": null,
            "department": null,
            "department_title": null,
            "dismissal_date": null,
            "upcoming_employment": null,
            "dismissal_cancellation_eligible": false,
            "rehire_cancellation_eligible": false,
            "member_portal_invitation_status": null,
            "partner_portal_invitation_sent": false
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
    "/v1/contractors/{contractor_uuid}": {
      "get": {
        "summary": "Get a contractor",
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
          },
          {
            "name": "include",
            "in": "query",
            "explode": false,
            "required": false,
            "schema": {
              "type": "array",
              "items": {
                "type": "string",
                "enum": [
                  "company_name",
                  "portal_invitations"
                ],
                "x-enumDescriptions": {
                  "company_name": "Include the name of the company that the contractor is associated with",
                  "portal_invitations": "Include portal invitation status information, including member portal invitation details and partner portal invitation status"
                }
              }
            },
            "description": "Include the requested attribute(s) in each contractor response. Multiple options are comma separated."
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-contractors-contractor_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get a contractor.\n\nscope: `contractors:read`",
        "tags": [
          "Contractors"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Successful",
            "content": {
              "application/json": {
                "examples": {
                  "Individual Contractor": {
                    "value": {
                      "$ref": "#/components/schemas/Contractor/x-examples/Individual Contractor"
                    }
                  },
                  "Business Contractor": {
                    "value": {
                      "$ref": "#/components/schemas/Contractor/x-examples/Business Contractor"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Contractor"
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
