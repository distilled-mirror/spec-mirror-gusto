---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get notifications for company

Returns all notifications relevant for the given company.

scope: `notifications:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Notifications"
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
      "Notifications-List": {
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "uuid": "d053ee2a-a80f-4a61-8bf8-6122c1f954dd",
              "company_uuid": "46c8329d-ebd1-49ba-878c-810b481a34c9",
              "category": "company_setup.missing_mandatory_sick_time_policy",
              "title": "Set up a sick time off policy",
              "message": "At least one company work location requires businesses to provide a sick time off policy.",
              "actionable": true,
              "can_block_payroll": false,
              "published_at": "2025-06-09T13:42:59.000-07:00",
              "due_at": null,
              "status": "open",
              "resources": [],
              "template_variables": {}
            },
            {
              "uuid": "2edd148b-c4c3-4cda-b3e1-72b87399e6c8",
              "company_uuid": "46c8329d-ebd1-49ba-878c-810b481a34c9",
              "category": "bank_error.compensation_credit_failure",
              "title": "Unable to deposit funds to Donn Cormier",
              "message": "We were unable to deposit a recent paycheck to Donn’s bank account, so these funds of $100.00 will be returned to Luettgen-Gusikowski’s bank account. Once the funds are received, the payment should be made directly to Donn.",
              "actionable": true,
              "can_block_payroll": false,
              "published_at": "2025-06-09T13:43:00.000-07:00",
              "due_at": null,
              "status": "open",
              "resources": [
                {
                  "entity_type": "Employee",
                  "entity_uuid": "66a27bb8-be5b-42e5-82b8-b2d0044a7f9e"
                }
              ],
              "template_variables": {
                "beneficiary_name": "Donn Cormier",
                "amount": "$100.00",
                "company_name": "Luettgen-Gusikowski"
              }
            }
          ],
          "with_transactional_mailer_notification": [
            {
              "uuid": "d053ee2a-a80f-4a61-8bf8-6122c1f954dd",
              "company_uuid": "46c8329d-ebd1-49ba-878c-810b481a34c9",
              "category": "company_setup.missing_mandatory_sick_time_policy",
              "title": "Set up a sick time off policy",
              "message": "At least one company work location requires businesses to provide a sick time off policy.",
              "actionable": true,
              "can_block_payroll": false,
              "published_at": "2025-06-09T13:42:59.000-07:00",
              "due_at": null,
              "status": "open",
              "resources": [],
              "template_variables": {}
            },
            {
              "uuid": "3f16b3e4-3c0e-4f92-9c1d-9e9dc9d1f7a2",
              "company_uuid": "46c8329d-ebd1-49ba-878c-810b481a34c9",
              "category": "notification.taxops.created",
              "title": "Confirm or amend the tax filing that was filed outside of payroll",
              "message": "We recently attempted to file Acme Consulting's Q2 2025 tax returns. However, California EDD rejected the filing because it has already been completed by someone else. Please confirm that the already-filed return matches the records on file. If the return is incorrect, you will need to amend it directly with the agency. We cannot amend returns we did not originally file. In the future, ensure this return is not filed outside of payroll.",
              "actionable": true,
              "can_block_payroll": false,
              "published_at": "2025-06-09T13:44:00.000-07:00",
              "due_at": null,
              "status": "open",
              "resources": [
                {
                  "entity_type": "Employee",
                  "entity_uuid": "66a27bb8-be5b-42e5-82b8-b2d0044a7f9e"
                }
              ],
              "template_variables": {
                "company_name": "Acme Consulting",
                "quarter": "Q2 2025",
                "agency_list": "California EDD"
              }
            }
          ]
        },
        "items": {
          "$ref": "#/components/schemas/Notification"
        }
      },
      "Notification": {
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "Unique identifier of a notification."
          },
          "company_uuid": {
            "type": "string",
            "description": "Unique identifier of the company to which the notification belongs."
          },
          "title": {
            "type": "string",
            "description": "The title of the notification. This highlights the actionable component of the notification."
          },
          "message": {
            "type": "string",
            "description": "The message of the notification. This provides additional context for the user and recommends a specific action to resolve the notification."
          },
          "status": {
            "type": "string",
            "description": "Represents the notification's status as managed by our system. It is updated based on observable system events and internal business logic, and does not reflect resolution steps taken outside our system. This field is read-only and cannot be modified via the API.",
            "enum": [
              "open",
              "resolved",
              "expired"
            ]
          },
          "category": {
            "type": "string",
            "description": "The notification's category."
          },
          "actionable": {
            "type": "boolean",
            "description": "Indicates whether a notification requires action or not. If false, the notification provides critical information only."
          },
          "can_block_payroll": {
            "type": "boolean",
            "description": "Indicates whether a notification may block ability to run payroll. If true, we suggest that these notifications are prioritized to your end users."
          },
          "published_at": {
            "type": "string",
            "description": "Timestamp of when the notification was published."
          },
          "due_at": {
            "type": [
              "string",
              "null"
            ],
            "description": "Timestamp of when the notification is due. If the notification has no due date, this field will be null."
          },
          "template_variables": {
            "type": "object",
            "description": "An object containing template variables used to render the notification. The structure of this object depends on the notification category. Each category defines a fixed set of variable names (keys), which are always present. The values of these variables can vary depending on the specific notification instance.",
            "additionalProperties": {
              "type": "string"
            }
          },
          "resources": {
            "type": "array",
            "description": "An array of entities relevant to the notification",
            "items": {
              "type": "object",
              "properties": {
                "entity_type": {
                  "type": "string",
                  "description": "The type of entity being described.",
                  "enum": [
                    "BankAccount",
                    "Contractor",
                    "ContractorPayment",
                    "Employee",
                    "Payroll",
                    "PaySchedule",
                    "RecoveryCase",
                    "Signatory",
                    "Wire In Request"
                  ]
                },
                "entity_uuid": {
                  "type": "string",
                  "description": "Unique identifier of the entity"
                },
                "reference_type": {
                  "type": "string",
                  "description": "Optional. The type of a resource that is related to the one described by entity_type and entity_uuid. For instance, if the entity_type is “BankAccount”, the reference_type could be the “Employee” or “Contractor” to whom the bank account belongs."
                },
                "reference_uuid": {
                  "type": "string",
                  "description": "Optional. Unique identifier of the reference."
                }
              },
              "required": [
                "entity_type",
                "entity_uuid"
              ]
            }
          }
        },
        "required": [
          "uuid",
          "company_uuid",
          "title",
          "message",
          "category",
          "actionable",
          "status",
          "published_at",
          "due_at",
          "resources",
          "can_block_payroll"
        ],
        "x-examples": {
          "notification_show": {
            "uuid": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "company_uuid": "88f7cca1-dcad-4d20-84db-7fb80303d69f",
            "title": "Action required: Additional information needed to process payroll",
            "message": "If we do not receive this information as soon as possible, your payroll may not be processed on time.",
            "status": "open",
            "category": "information_request",
            "actionable": true,
            "can_block_payroll": true,
            "published_at": "2022-01-01T00:00:00.000Z",
            "due_at": "2022-02-01T00:00:00.000Z",
            "template_variables": {
              "blocked_task": "Payroll"
            },
            "resources": [
              {
                "entity_type": "Employee",
                "entity_uuid": "21b6f9ce-0ac4-4745-8d8a-127f8c0f00f2"
              }
            ]
          },
          "transactional_mailer_notification_show": {
            "uuid": "3f16b3e4-3c0e-4f92-9c1d-9e9dc9d1f7a2",
            "company_uuid": "88f7cca1-dcad-4d20-84db-7fb80303d69f",
            "title": "Confirm or amend the tax filing that was filed outside of payroll",
            "message": "We recently attempted to file Acme Consulting's Q2 2025 tax returns. However, California EDD rejected the filing because it has already been completed by someone else. Please confirm that the already-filed return matches the records on file. If the return is incorrect, you will need to amend it directly with the agency. We cannot amend returns we did not originally file. In the future, ensure this return is not filed outside of payroll.",
            "status": "open",
            "category": "notification.taxops.created",
            "actionable": true,
            "can_block_payroll": false,
            "published_at": "2025-06-09T13:44:00.000-07:00",
            "due_at": null,
            "template_variables": {
              "company_name": "Acme Consulting",
              "quarter": "Q2 2025",
              "agency_list": "California EDD"
            },
            "resources": [
              {
                "entity_type": "Employee",
                "entity_uuid": "21b6f9ce-0ac4-4745-8d8a-127f8c0f00f2"
              }
            ]
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
    "/v1/companies/{company_uuid}/notifications": {
      "get": {
        "summary": "Get notifications for company",
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
            "description": "The UUID of the company for which you would like to return notifications",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "status",
            "in": "query",
            "schema": {
              "type": "string",
              "enum": [
                "open",
                "expired",
                "resolved"
              ]
            }
          },
          {
            "name": "page",
            "in": "query",
            "required": false,
            "description": "The page that is requested. When unspecified, will load all objects unless endpoint forces pagination.",
            "schema": {
              "type": "integer"
            }
          },
          {
            "name": "per",
            "in": "query",
            "required": false,
            "description": "Number of objects per page. For majority of endpoints will default to 25",
            "schema": {
              "type": "integer"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-company-notifications",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns all notifications relevant for the given company.\n\nscope: `notifications:read`",
        "tags": [
          "Notifications"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Notifications-List/x-examples/success_status"
                    }
                  },
                  "with_transactional_mailer_notification": {
                    "value": {
                      "$ref": "#/components/schemas/Notifications-List/x-examples/with_transactional_mailer_notification"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Notifications-List"
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
