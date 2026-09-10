---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get the employee's onboarding status

# Description
Retrieves an employee's onboarding status. The data returned helps inform the required onboarding steps and respective completion status.


## onboarding_status

### Admin-facilitated onboarding
| onboarding_status | Description |
|:------------------|------------:|
| `admin_onboarding_incomplete` | Admin needs to complete the full employee-onboarding. |
| `onboarding_completed` | Employee has been fully onboarded and verified. |

### Employee self-onboarding
| onboarding_status | Description |
|:------------------|------------:|
| `admin_onboarding_incomplete` | Admin needs to enter basic information about the employee. |
| `self_onboarding_pending_invite` | Admin has the intention to invite the employee to self-onboard (e.g., marking a checkbox), but the system has not yet sent the invitation. |
| `self_onboarding_invited` | Employee has been sent an invitation to self-onboard. |
| `self_onboarding_invited_started` | Employee has started the self-onboarding process. |
| `self_onboarding_invited_overdue` | Employee's start date has passed, and employee has still not completed self-onboarding. |
| `self_onboarding_completed_by_employee` | Employee has completed entering in their information. The status should be updated via API to "self_onboarding_awaiting_admin_review" from here, once the Admin has started reviewing. |
| `self_onboarding_awaiting_admin_review` | Admin has started to verify the employee's information. |
| `onboarding_completed` | Employee has been fully onboarded and verified. |

## onboarding_steps

| onboarding_steps | Requirement(s) to be completed |
|:-----------------|-------------------------------:|
| `personal_details` | Add employee's first name, last name, email, date of birth, social security number |
| `compensation_details` | Associate employee to a job & compensation. |
| `add_work_address` | Add employee work address. |
| `add_home_address` | Add employee home address. |
| `federal_tax_setup` | Set up federal tax withholdings. |
| `state_tax_setup` | Set up state tax withholdings. |
| `direct_deposit_setup` | (optional) Set up employee's direct deposit. |
| `employee_form_signing` | Employee forms (e.g., W4, direct deposit authorization) are generated & signed. |
| `file_new_hire_report` | File a new hire report for this employee. |
| `admin_review` | Admin reviews & confirms employee details (only required for Employee self-onboarding) |

scope: `employees:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employees"
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
      "Employee-Onboarding-Status": {
        "description": "The representation of an employee's onboarding status.",
        "type": "object",
        "title": "Employee-Onboarding-Status",
        "x-examples": {
          "success_status": {
            "uuid": "8351cf2a-17cb-49e3-94a7-9986dcb11e84",
            "onboarding_status": "onboarding_completed",
            "onboarding_steps": [
              {
                "title": "Personal details",
                "id": "personal_details",
                "required": true,
                "completed": true,
                "requirements": []
              },
              {
                "title": "Enter compensation details",
                "id": "compensation_details",
                "required": true,
                "completed": true,
                "requirements": []
              },
              {
                "title": "Add work address",
                "id": "add_work_address",
                "required": true,
                "completed": true,
                "requirements": []
              },
              {
                "title": "Add home address",
                "id": "add_home_address",
                "required": true,
                "completed": true,
                "requirements": []
              },
              {
                "title": "Enter federal tax withholdings",
                "id": "federal_tax_setup",
                "required": true,
                "completed": true,
                "requirements": []
              },
              {
                "title": "Enter state tax information",
                "id": "state_tax_setup",
                "required": true,
                "completed": false,
                "requirements": [
                  "add_work_address",
                  "add_home_address"
                ]
              },
              {
                "title": "Direct deposit setup",
                "id": "direct_deposit_setup",
                "required": false,
                "completed": true,
                "requirements": []
              },
              {
                "title": "Employee form signing",
                "id": "employee_form_signing",
                "required": true,
                "completed": false,
                "requirements": [
                  "federal_tax_setup",
                  "state_tax_setup"
                ]
              },
              {
                "title": "File new hire report",
                "id": "file_new_hire_report",
                "required": true,
                "completed": false,
                "requirements": [
                  "add_work_address"
                ]
              }
            ],
            "blockers": []
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier for this employee."
          },
          "onboarding_status": {
            "type": "string",
            "description": "One of the \"onboarding_status\" enum values."
          },
          "onboarding_steps": {
            "type": "array",
            "description": "List of steps required to onboard an employee.",
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
          },
          "blockers": {
            "type": "array",
            "description": "Validation issues that should be resolved before this employee's onboarding is complete. Each entry identifies an affected field, a category describing the type of problem, and a human-readable message.\n\nSupported categories:\n\n- `duplicate_value`: Another employee in the same company already has this value. To resolve, cancel this onboarding and initiate a rehire if it's a returning employee, or contact support to investigate the conflict.\n\nThis list may grow over time as new validation rules are added.\n",
            "items": {
              "type": "object",
              "properties": {
                "field": {
                  "type": "string",
                  "enum": [
                    "ssn"
                  ],
                  "description": "The employee field affected."
                },
                "category": {
                  "type": "string",
                  "enum": [
                    "duplicate_value"
                  ],
                  "description": "Category of the blocker. See the array-level description for resolution guidance."
                },
                "message": {
                  "type": "string",
                  "description": "Human-readable description of the blocker."
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
    "/v1/employees/{employee_id}/onboarding_status": {
      "get": {
        "summary": "Get the employee's onboarding status",
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
        "operationId": "get-v1-employees-employee_id-onboarding_status",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "# Description\nRetrieves an employee's onboarding status. The data returned helps inform the required onboarding steps and respective completion status.\n\n\n## onboarding_status\n\n### Admin-facilitated onboarding\n| onboarding_status | Description |\n|:------------------|------------:|\n| `admin_onboarding_incomplete` | Admin needs to complete the full employee-onboarding. |\n| `onboarding_completed` | Employee has been fully onboarded and verified. |\n\n### Employee self-onboarding\n| onboarding_status | Description |\n|:------------------|------------:|\n| `admin_onboarding_incomplete` | Admin needs to enter basic information about the employee. |\n| `self_onboarding_pending_invite` | Admin has the intention to invite the employee to self-onboard (e.g., marking a checkbox), but the system has not yet sent the invitation. |\n| `self_onboarding_invited` | Employee has been sent an invitation to self-onboard. |\n| `self_onboarding_invited_started` | Employee has started the self-onboarding process. |\n| `self_onboarding_invited_overdue` | Employee's start date has passed, and employee has still not completed self-onboarding. |\n| `self_onboarding_completed_by_employee` | Employee has completed entering in their information. The status should be updated via API to \"self_onboarding_awaiting_admin_review\" from here, once the Admin has started reviewing. |\n| `self_onboarding_awaiting_admin_review` | Admin has started to verify the employee's information. |\n| `onboarding_completed` | Employee has been fully onboarded and verified. |\n\n## onboarding_steps\n\n| onboarding_steps | Requirement(s) to be completed |\n|:-----------------|-------------------------------:|\n| `personal_details` | Add employee's first name, last name, email, date of birth, social security number |\n| `compensation_details` | Associate employee to a job & compensation. |\n| `add_work_address` | Add employee work address. |\n| `add_home_address` | Add employee home address. |\n| `federal_tax_setup` | Set up federal tax withholdings. |\n| `state_tax_setup` | Set up state tax withholdings. |\n| `direct_deposit_setup` | (optional) Set up employee's direct deposit. |\n| `employee_form_signing` | Employee forms (e.g., W4, direct deposit authorization) are generated & signed. |\n| `file_new_hire_report` | File a new hire report for this employee. |\n| `admin_review` | Admin reviews & confirms employee details (only required for Employee self-onboarding) |\n\nscope: `employees:read`",
        "tags": [
          "Employees"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Onboarding-Status/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Onboarding-Status"
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
