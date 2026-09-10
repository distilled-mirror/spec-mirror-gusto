---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Update a historical employee

Update a historical employee, an employee that was previously dismissed from the company in the current year.

scope: `employees:manage employees:write`

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
      "Versionable-Required": {
        "type": "object",
        "properties": {
          "version": {
            "type": "string",
            "example": "56d00c178bc7393b2a206ed6a86afcb4",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          }
        },
        "required": [
          "version"
        ]
      },
      "Location": {
        "description": "The representation of an address in Gusto.",
        "type": "object",
        "title": "",
        "x-examples": {
          "success_status": {
            "created_at": "2025-06-09T13:43:49.000-07:00",
            "updated_at": "2025-06-09T13:43:50.000-07:00",
            "company_uuid": "10593a6a-505b-4aa6-bf31-15dcdceedbe3",
            "version": "e1bdd845a493c74908f8e15d6114169b",
            "uuid": "6b1351a2-de35-4499-b948-43abab274634",
            "street_1": "300 3rd Street",
            "street_2": "Apartment 318",
            "city": "San Francisco",
            "state": "CA",
            "zip": "94107",
            "country": "USA",
            "active": true,
            "phone_number": "8009360383",
            "filing_address": true,
            "mailing_address": true
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the location object.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "company_uuid": {
            "type": "string",
            "description": "The UUID for the company to which the location belongs. Only included if the location belongs to a company.",
            "readOnly": true
          },
          "phone_number": {
            "type": "string",
            "readOnly": false,
            "description": "The phone number for the location. Required for company locations. Optional for employee locations."
          },
          "street_1": {
            "type": "string",
            "readOnly": false
          },
          "street_2": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false
          },
          "city": {
            "type": "string",
            "readOnly": false
          },
          "state": {
            "type": "string",
            "readOnly": false
          },
          "zip": {
            "type": "string",
            "readOnly": false
          },
          "country": {
            "type": "string",
            "readOnly": false,
            "default": "USA"
          },
          "mailing_address": {
            "type": "boolean",
            "description": "Specifies if the location is the company's mailing address. Only included if the location belongs to a company."
          },
          "filing_address": {
            "description": "Specifies if the location is the company's filing address. Only included if the location belongs to a company.",
            "type": "boolean"
          },
          "created_at": {
            "type": "string",
            "description": "Datetime for when location is created"
          },
          "updated_at": {
            "type": "string",
            "description": "Datetime for when location is updated"
          },
          "active": {
            "type": "boolean",
            "description": "The status of the location. Inactive locations have been deleted, but may still have historical data associated with them.",
            "readOnly": true
          },
          "inactive": {
            "type": "boolean",
            "description": "The status of the location. Inactive locations have been deleted, but may still have historical data associated with them.",
            "readOnly": true
          },
          "warnings": {
            "type": "array",
            "description": "An array of warning objects that provide additional information about the address. Warnings do not prevent the address from being saved.",
            "items": {
              "$ref": "#/components/schemas/Warning-Object"
            }
          }
        },
        "required": [
          "uuid"
        ]
      },
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
      "Unprocessable-Entity-Error-Object": {
        "description": "Unprocessable Entity\n  \nThis may happen when the body of your request contains errors such as `invalid_attribute_value`, or the request fails due to an `invalid_operation`. See the [Errors Categories](https://docs.gusto.com/embedded-payroll/docs/error-categories) guide for more details.\n",
        "type": "object",
        "required": [
          "errors"
        ],
        "properties": {
          "errors": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Entity-Error-Object"
            }
          }
        },
        "x-examples": {
          "tax_filing_invalid_status": {
            "errors": [
              {
                "error_key": "status",
                "category": "invalid_attribute_value",
                "message": "Status must be one of: not_started, in_progress, blocked, accepted, not_required, failed"
              }
            ]
          },
          "tax_filing_invalid_sort_by": {
            "errors": [
              {
                "error_key": "sort_by",
                "category": "invalid_attribute_value",
                "message": "Sort by must be one of period_start, period_end, due_date, filed_at, optionally suffixed with :asc or :desc"
              }
            ]
          },
          "tax_filing_invalid_period_start": {
            "errors": [
              {
                "error_key": "period_start",
                "category": "invalid_attribute_value",
                "message": "Period start must be a valid ISO 8601 date"
              }
            ]
          },
          "tax_filing_invalid_jurisdiction": {
            "errors": [
              {
                "error_key": "jurisdiction",
                "category": "invalid_attribute_value",
                "message": "Jurisdiction must be two-letter state codes or US (invalid: XX)"
              }
            ]
          },
          "tax_payment_invalid_sort_by": {
            "errors": [
              {
                "error_key": "sort_by",
                "category": "invalid_parameter",
                "message": "Unknown sort_by: bogus:asc. Must be one of amount, due_date, payment_sent_on, period_end, period_start, optionally suffixed with :asc or :desc"
              }
            ]
          },
          "tax_payment_inverted_range": {
            "errors": [
              {
                "error_key": "due_date_to",
                "category": "invalid_attribute_value",
                "message": "Due date to must be greater than or equal to due date from"
              }
            ]
          },
          "partner_managed_company_disassociate_not_associated": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Could not disassociate from embedded payroll: company not associated with partner."
              }
            ]
          },
          "bulk_report_invalid_report_type": {
            "errors": [
              {
                "error_key": "batch",
                "category": "nested_errors",
                "errors": [
                  {
                    "idx": 0,
                    "category": "nested_errors",
                    "errors": [
                      {
                        "error_key": "report_type",
                        "category": "invalid_attribute_value",
                        "message": "Invalid report type: invalid_type"
                      }
                    ]
                  }
                ]
              }
            ]
          },
          "nested_disbursement_errors": {
            "errors": [
              {
                "error_key": "disbursements",
                "category": "nested_errors",
                "metadata": {
                  "employee_uuid": "invalid-uuid-1"
                },
                "errors": [
                  {
                    "error_key": "employee_uuid",
                    "category": "not_found",
                    "message": "Disbursement not found."
                  }
                ]
              },
              {
                "error_key": "disbursements",
                "category": "nested_errors",
                "metadata": {
                  "employee_uuid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
                },
                "errors": [
                  {
                    "error_key": "payment_method",
                    "category": "invalid_attribute_value",
                    "message": "Payment method must be one of: Direct Deposit, Check."
                  },
                  {
                    "error_key": "payment_status",
                    "category": "invalid_attribute_value",
                    "message": "Payment status is not valid for payment method 'InvalidMethod'."
                  }
                ]
              }
            ]
          },
          "webhook_subscription_url_missing": {
            "errors": [
              {
                "error_key": "url",
                "category": "invalid_attribute_value",
                "message": "URL can't be blank"
              }
            ]
          },
          "webhook_subscription_invalid_entity_type": {
            "errors": [
              {
                "error_key": "subscription_entities.entity_type",
                "category": "invalid_attribute_value",
                "message": "Entity type is not included in the list"
              }
            ]
          },
          "invalid_token": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Invalid verification token"
              }
            ]
          },
          "notification_supporting_data_invalid": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Invalid notification: supporting data is no longer valid."
              }
            ]
          },
          "employee_payment_details_invalid_filter_combination": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_request_error",
                "message": "Cannot filter by both employee_uuid and payroll_uuid simultaneously."
              }
            ]
          },
          "contractor_document_sign_missing_agree": {
            "errors": [
              {
                "error_key": "agree",
                "category": "invalid_attribute_value",
                "message": "You must agree to sign the document electronically"
              }
            ]
          },
          "contractor_document_sign_invalid_ip_address": {
            "errors": [
              {
                "error_key": "signed_by_ip_address",
                "category": "invalid_attribute_value",
                "message": "Signed by ip address is invalid"
              }
            ]
          },
          "contractor_document_sign_missing_fields": {
            "errors": [
              {
                "error_key": "fields",
                "category": "nested_errors",
                "errors": [
                  {
                    "error_key": "dogs_name",
                    "category": "invalid_attribute_value",
                    "message": "Field is required."
                  },
                  {
                    "error_key": "dogs_favorite_food",
                    "category": "invalid_attribute_value",
                    "message": "Field is required."
                  },
                  {
                    "error_key": "dogs_signature",
                    "category": "invalid_attribute_value",
                    "message": "Field is required."
                  }
                ]
              }
            ]
          },
          "contractor_document_sign_already_signed": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This form has already been signed"
              }
            ]
          },
          "contractor_document_unsupported_form_type": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Form type is not supported"
              }
            ]
          },
          "bank_account_delete_unfunded_payments": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "FundingMethod has unfunded payments"
              }
            ]
          },
          "bank_account_verify_incorrect_deposits": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Your bank account cannot be verified. Please check the test deposit amounts."
              }
            ]
          },
          "bank_account_verify_already_verified": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Your bank account has already been verified."
              }
            ]
          },
          "bank_account_missing_routing": {
            "errors": [
              {
                "error_key": "routing_number",
                "category": "invalid_attribute_value",
                "message": "Routing number is required."
              }
            ]
          },
          "plaid_processor_token_missing": {
            "errors": [
              {
                "error_key": "processor_token",
                "category": "invalid_attribute_value",
                "message": "Processor token param is missing or the value is empty: processor_token"
              }
            ]
          },
          "contractor_bank_account_invalid_account_number": {
            "errors": [
              {
                "error_key": "account_number",
                "category": "invalid_attribute_value",
                "message": "Invalid account number format"
              }
            ]
          },
          "contractor_bank_account_invalid_account_type": {
            "errors": [
              {
                "error_key": "account_type",
                "category": "invalid_attribute_value",
                "message": "Account type's value is not included in the list"
              }
            ]
          },
          "contractor_payment_method_invalid_type": {
            "errors": [
              {
                "error_key": "type",
                "category": "invalid_attribute_value",
                "message": "Payment method must be 'Check' or 'Direct Deposit'"
              }
            ]
          },
          "company_attachment_missing_document": {
            "errors": [
              {
                "error_key": "base",
                "category": "missing_parameter",
                "message": "'document' is required"
              }
            ]
          },
          "company_attachment_invalid_category": {
            "errors": [
              {
                "error_key": "base",
                "category": "missing_parameter",
                "message": "Attachment category is not supported"
              }
            ]
          },
          "company_attachment_invalid_file_type": {
            "errors": [
              {
                "error_key": "file",
                "category": "invalid_attribute_value",
                "message": "file type is not allowed"
              }
            ]
          },
          "provision_missing_user": {
            "errors": [
              {
                "error_key": "user",
                "category": "missing_parameter",
                "message": "user is required."
              }
            ]
          },
          "provision_invalid_email": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Invalid email address."
              }
            ]
          },
          "admin_missing_required_field": {
            "errors": [
              {
                "error_key": "last_name",
                "category": "missing_parameter",
                "message": "last_name is required."
              }
            ]
          },
          "admin_duplicate_email": {
            "errors": [
              {
                "error_key": "email",
                "category": "invalid_attribute_value",
                "message": "User has already been taken"
              },
              {
                "error_key": "company",
                "category": "invalid_attribute_value",
                "message": "Company is invalid"
              }
            ]
          },
          "sandbox_w2_already_generated": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "W2 already generated for this year"
              }
            ]
          },
          "sandbox_w2_invalid_year": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Cannot generate form for year 1800"
              }
            ]
          },
          "sandbox_1099_invalid_year": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Please enter a year between 2015 and 2024"
              }
            ]
          },
          "employee_bank_account_missing_name": {
            "errors": [
              {
                "error_key": "name",
                "category": "invalid_attribute_value",
                "message": "Name is required"
              }
            ]
          },
          "employee_bank_account_invalid_account_number": {
            "errors": [
              {
                "error_key": "account_number",
                "category": "invalid_attribute_value",
                "message": "Invalid account number"
              }
            ]
          },
          "employee_bank_account_duplicate": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Bank account with the same details already exists"
              }
            ]
          },
          "employee_bank_account_invalid_routing_on_update": {
            "errors": [
              {
                "error_key": "routing_number",
                "category": "invalid_attribute_value",
                "message": "Invalid routing number"
              }
            ]
          },
          "payment_configs_missing_parameter": {
            "errors": [
              {
                "error_key": "base",
                "category": "missing_parameter",
                "message": "At least one parameter must be provided"
              }
            ]
          },
          "payment_configs_invalid_fast_payment_limit": {
            "errors": [
              {
                "error_key": "fast_payment_limit",
                "category": "invalid_attribute_value",
                "message": "Fast payment limit should be a number"
              }
            ]
          },
          "pay_periods_invalid_end_date": {
            "errors": [
              {
                "error_key": "end_date",
                "category": "invalid_parameter",
                "message": "End date cannot be more than 3 months in future"
              }
            ]
          },
          "company_industry_selection_naics_code_required": {
            "errors": [
              {
                "error_key": "naics_code",
                "category": "invalid_attribute_value",
                "message": "Naics code is required."
              }
            ]
          },
          "company_industry_selection_naics_code_invalid": {
            "errors": [
              {
                "error_key": "naics_code",
                "category": "invalid_attribute_value",
                "message": "Naics code must be equal to 6 digits."
              }
            ]
          },
          "company_industry_selection_sics_codes_invalid": {
            "errors": [
              {
                "error_key": "sic_codes",
                "category": "invalid_attribute_value",
                "message": "Sic codes must be equal to 4 digits"
              }
            ]
          },
          "time_off_policy_name_required": {
            "errors": [
              {
                "error_key": "name",
                "category": "invalid_attribute_value",
                "message": "Name is required."
              }
            ]
          },
          "time_off_policy_unlimited_invalid_accrual_rate": {
            "errors": [
              {
                "error_key": "accrual_rate",
                "category": "invalid_operation",
                "message": "Accrual rate must be blank for unlimited policies."
              }
            ]
          },
          "time_off_policy_pending_requests": {
            "errors": [
              {
                "error_key": "time_off_policy",
                "category": "invalid_operation",
                "message": "Cannot deactivate policy with pending time off requests."
              }
            ]
          },
          "time_off_policy_employees_required": {
            "errors": [
              {
                "error_key": "employees",
                "category": "invalid_attribute_value",
                "message": "Employees are required."
              }
            ]
          },
          "time_off_policy_unlimited_balance_update": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Can not adjust balances for unlimited policies."
              }
            ]
          },
          "payroll_sync_invalid_pay_schedule": {
            "errors": [
              {
                "error_key": "pay_schedule_uuid",
                "category": "invalid_attribute_value",
                "message": "Pay schedule uuid could not be found."
              }
            ]
          },
          "payroll_sync_no_employees": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "There are no employees to run payroll for in the selected pay period."
              }
            ]
          },
          "payroll_sync_empty_export": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "There are no hours to sync to payroll for the selected pay period."
              }
            ]
          },
          "payroll_update_payroll_item_validation_error": {
            "errors": [
              {
                "error_key": "employee_compensations",
                "category": "nested_errors",
                "errors": [
                  {
                    "error_key": "payment_method",
                    "category": "invalid_attribute_value",
                    "message": "Payment method cannot be changed for check-only payrolls. All employees must be paid by check."
                  }
                ]
              }
            ]
          },
          "payroll_update_recurring_reimbursement_error": {
            "errors": [
              {
                "error_key": "employee_compensations",
                "category": "nested_errors",
                "errors": [
                  {
                    "error_key": "reimbursements",
                    "category": "invalid_attribute_value",
                    "message": "Cannot update recurring reimbursements through payroll updates. Update the recurring reimbursement directly."
                  }
                ]
              }
            ]
          },
          "migrate_company_terms_of_service": {
            "errors": [
              {
                "error_key": "base",
                "category": "migration_blocker",
                "message": "Terms of service must be accepted by a company payroll admin.",
                "metadata": {
                  "key": "terms_of_service"
                }
              }
            ]
          },
          "migrate_company_already_migrated": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "The operation was already performed for this company.",
                "metadata": {
                  "key": "migrated_company"
                }
              }
            ]
          },
          "partner_managed_company_create_missing_company": {
            "errors": [
              {
                "error_key": "company",
                "category": "missing_parameter",
                "message": "company is required."
              }
            ]
          },
          "partner_managed_company_create_invalid_name": {
            "errors": [
              {
                "error_key": "name",
                "category": "invalid_attribute_value",
                "message": "Company name must be at least 2 characters"
              }
            ]
          },
          "partner_managed_company_tos_invalid_ip_address": {
            "errors": [
              {
                "error_key": "ip_address",
                "category": "invalid_attribute_value",
                "message": "A valid user's IP Address is required in order to accept terms of service."
              }
            ]
          },
          "partner_managed_company_tos_missing_external_user_id": {
            "errors": [
              {
                "error_key": "external_user_id",
                "category": "invalid_attribute_value",
                "message": "Your platform's User ID is required in order to accept terms of service."
              }
            ]
          },
          "partner_managed_company_tos_invalid_user_email": {
            "errors": [
              {
                "error_key": "email",
                "category": "invalid_attribute_value",
                "message": "Email does not belong to company user."
              }
            ]
          },
          "holiday_pay_policy_already_exists": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Company already has a holiday pay policy."
              }
            ]
          },
          "holiday_pay_policy_not_exists": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Company does not have a holiday pay policy, please create one"
              }
            ]
          },
          "holiday_pay_policy_invalid_employees": {
            "errors": [
              {
                "error_key": "employees",
                "category": "invalid_attribute_value",
                "message": "Invalid employee uuids provided."
              }
            ]
          },
          "onboarded_employee": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Cannot delete onboarded employee"
              }
            ]
          },
          "garnishment_invalid_amount": {
            "errors": [
              {
                "error_key": "amount",
                "category": "invalid_attribute_value",
                "message": "Amount must be greater than or equal to 0"
              }
            ]
          },
          "garnishment_pay_period_exceeds_annual": {
            "errors": [
              {
                "error_key": "pay_period_maximum",
                "category": "invalid_attribute_value",
                "message": "Pay period maximum must be less than annual maximum"
              }
            ]
          },
          "garnishment_type_cannot_change": {
            "errors": [
              {
                "error_key": "garnishment_type",
                "category": "invalid_attribute_value",
                "message": "Garnishment type cannot change"
              }
            ]
          },
          "garnishment_child_support_invalid_fips": {
            "errors": [
              {
                "error_key": "child_support",
                "category": "nested_errors",
                "errors": [
                  {
                    "error_key": "fips_code",
                    "category": "invalid_attribute_value",
                    "message": "FIPS code is not valid for CA"
                  }
                ]
              }
            ]
          },
          "garnishment_child_support_missing_fields": {
            "errors": [
              {
                "error_key": "child_support",
                "category": "nested_errors",
                "errors": [
                  {
                    "error_key": "state",
                    "category": "invalid_attribute_value",
                    "message": "Select a valid state agency"
                  },
                  {
                    "error_key": "payment_period",
                    "category": "invalid_attribute_value",
                    "message": "Select a valid payment period"
                  },
                  {
                    "error_key": "case_number",
                    "category": "invalid_attribute_value",
                    "message": "Case number is required"
                  }
                ]
              }
            ]
          },
          "invalid_attribute": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "There is an error in the request body."
              }
            ]
          },
          "pay_schedule_missing_anchor_dates": {
            "errors": [
              {
                "error_key": "anchor_pay_date",
                "category": "invalid_attribute_value",
                "message": "can't be blank"
              },
              {
                "error_key": "anchor_end_of_pay_period",
                "category": "invalid_attribute_value",
                "message": "can't be blank"
              }
            ]
          },
          "pay_schedule_invalid_frequency": {
            "errors": [
              {
                "error_key": "frequency",
                "category": "invalid_attribute_value",
                "message": "is not included in the list"
              }
            ]
          },
          "pay_schedule_malformed_dates": {
            "errors": [
              {
                "error_key": "anchor_pay_date",
                "category": "invalid_attribute_value",
                "message": "is invalid"
              },
              {
                "error_key": "anchor_end_of_pay_period",
                "category": "invalid_attribute_value",
                "message": "is invalid"
              }
            ]
          },
          "skip_payroll_invalid_payroll_type": {
            "errors": [
              {
                "error_key": "payroll_type",
                "category": "invalid_attribute_value",
                "message": "Payroll type is not valid."
              }
            ]
          },
          "paid_holidays_invalid_year": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Invalid year provided."
              }
            ]
          },
          "tax_requirements_invalid_requirement_key": {
            "errors": [
              {
                "error_key": "requirement_sets",
                "category": "nested_errors",
                "metadata": {
                  "key": "misc",
                  "effective_from": null,
                  "state": "NY"
                },
                "errors": [
                  {
                    "error_key": "requirements",
                    "category": "nested_errors",
                    "metadata": {
                      "key": "1-2-3-4"
                    },
                    "errors": [
                      {
                        "error_key": "key",
                        "category": "invalid_attribute_value",
                        "message": "Key is required"
                      }
                    ]
                  }
                ]
              }
            ]
          },
          "tax_requirements_invalid_value_type": {
            "errors": [
              {
                "error_key": "requirement_sets",
                "category": "nested_errors",
                "metadata": {
                  "key": "misc",
                  "effective_from": null,
                  "state": "NY"
                },
                "errors": [
                  {
                    "error_key": "requirements",
                    "category": "nested_errors",
                    "metadata": {
                      "key": "71653ec0-00b5-4c66-a58b-22ecf21704c5"
                    },
                    "errors": [
                      {
                        "error_key": "value",
                        "category": "invalid_attribute_value",
                        "message": "Expected a value of type boolean, but got string"
                      }
                    ]
                  }
                ]
              }
            ]
          },
          "tax_requirements_domain_validation_failure": {
            "errors": [
              {
                "error_key": "requirement_sets",
                "category": "nested_errors",
                "metadata": {
                  "key": "taxrates",
                  "effective_from": "2026-01-01",
                  "state": "NY"
                },
                "errors": [
                  {
                    "error_key": "requirements",
                    "category": "nested_errors",
                    "metadata": {
                      "key": "e0ac2284-8d30-4100-ae23-f85f9574868b"
                    },
                    "errors": [
                      {
                        "error_key": "value",
                        "category": "invalid_attribute_value",
                        "message": "SUI Tax Rate must be between 0.00% and 9.825%"
                      }
                    ]
                  }
                ]
              }
            ]
          },
          "company_cannot_enable_contractor_only": {
            "errors": [
              {
                "error_key": "contractor_only",
                "category": "invalid_attribute_value",
                "message": "Contractor only cannot be enabled for existing companies."
              }
            ]
          },
          "company_missing_parameter": {
            "errors": [
              {
                "error_key": "base",
                "category": "missing_parameter",
                "message": "contractor_only is required."
              }
            ]
          },
          "starting_after_uuid_invalid": {
            "errors": [
              {
                "error_key": "starting_after_uuid",
                "category": "invalid_attribute_value",
                "message": "Parameter 'starting_after_uuid' does not correspond to a valid event."
              }
            ]
          },
          "resource_uuid_invalid": {
            "errors": [
              {
                "error_key": "resource_uuid",
                "category": "invalid_attribute_value",
                "message": "Parameter 'resource_uuid' does not correspond to a valid resource."
              }
            ]
          },
          "payroll_gross_up_invalid_net_pay": {
            "errors": [
              {
                "error_key": "net_pay",
                "category": "invalid_attribute_value",
                "message": "Net pay must be a number."
              }
            ]
          },
          "payroll_accruing_hours_invalid": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Hours cannot be negative."
              }
            ]
          },
          "payroll_cannot_cancel": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Payroll cannot be canceled."
              }
            ]
          },
          "frozen_payroll": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This payroll has already been processed. Its data cannot be updated or altered."
              }
            ]
          },
          "frozen_payroll_processing": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This payroll is being processed and cannot be updated at this time."
              }
            ]
          },
          "unmodifiable_payroll_type": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This type of payroll cannot be modified or processed. It is reserved for system processes."
              }
            ]
          },
          "employee_uuids_required": {
            "errors": [
              {
                "error_key": "employee_uuids",
                "category": "invalid_attribute_value",
                "message": "At least one employee_uuid is required to create an off-cycle payroll."
              }
            ]
          },
          "invalid_employee_uuids_format": {
            "errors": [
              {
                "error_key": "employee_uuids",
                "category": "invalid_attribute_value",
                "message": "Parameter employee_uuids must be an array."
              }
            ]
          },
          "maximum_employee_uuids_surpassed": {
            "errors": [
              {
                "error_key": "employee_uuids",
                "category": "invalid_attribute_value",
                "message": "Exceeded maximum of 100 for lookup."
              }
            ]
          },
          "maximum_off_roster_additions_surpassed": {
            "errors": [
              {
                "error_key": "employee_uuids",
                "category": "invalid_attribute_value",
                "message": "Cannot add more than 25 new employees to the payroll per call."
              }
            ]
          },
          "invalid_employee_uuid": {
            "errors": [
              {
                "error_key": "employee_uuids",
                "category": "invalid_attribute_value",
                "message": "Invalid Employee UUID(s).",
                "metadata": {
                  "entity_type": "Employee",
                  "entity_uuid": "invalid-uuid-123"
                }
              }
            ]
          },
          "payroll_blocker_missing_bank_info": {
            "errors": [
              {
                "error_key": "base",
                "category": "payroll_blocker",
                "message": "Company must have a bank account in order to run payroll.",
                "metadata": {
                  "key": "missing_bank_info"
                }
              }
            ]
          },
          "payroll_blocker_missing_employee_setup": {
            "errors": [
              {
                "error_key": "base",
                "category": "payroll_blocker",
                "message": "Company must add employees in order to run payroll.",
                "metadata": {
                  "key": "missing_employee_setup"
                }
              }
            ]
          },
          "payroll_blocker_missing_federal_tax_setup": {
            "errors": [
              {
                "error_key": "base",
                "category": "payroll_blocker",
                "message": "Company must complete federal tax setup in order to run payroll.",
                "metadata": {
                  "key": "missing_federal_tax_setup"
                }
              }
            ]
          },
          "payroll_blocker_missing_bank_verification": {
            "errors": [
              {
                "error_key": "base",
                "category": "payroll_blocker",
                "message": "Company bank account must be verified in order to run payroll.",
                "metadata": {
                  "key": "missing_bank_verification"
                }
              }
            ]
          },
          "payroll_blocker_suspended": {
            "errors": [
              {
                "error_key": "base",
                "category": "payroll_blocker",
                "message": "Company is suspended and cannot run payroll.",
                "metadata": {
                  "key": "suspended"
                }
              }
            ]
          },
          "submission_blocker_missing_selection": {
            "errors": [
              {
                "error_key": "submission_blockers",
                "category": "invalid_attribute_value",
                "message": "Submission blockers selections required"
              }
            ]
          },
          "submission_blocker_invalid_option": {
            "errors": [
              {
                "error_key": "submission_blockers",
                "category": "nested_errors",
                "metadata": {
                  "blocker_type": "fast_ach_threshold_exceeded"
                },
                "errors": [
                  {
                    "error_key": "selected_option",
                    "category": "invalid_attribute_value",
                    "message": "Selection is not available to resolve Fast ACH Threshold Exceeded. Please choose one of Wire In, Move To Four Day"
                  }
                ]
              }
            ]
          },
          "invalid_version": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_resource_version",
                "message": "You are attempting to update a resource using an out-of-date version."
              }
            ]
          },
          "payroll_update_stale_employee_compensation_version": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_resource_version",
                "message": "Supplied Version (stale-version) is invalid.",
                "metadata": {
                  "entity_type": "Employee",
                  "entity_uuid": "a8e9d2c6-1f3b-4d5a-9c8e-7f0b2d4c6e8a"
                }
              }
            ]
          },
          "employee_create_self_onboarding_missing_email": {
            "errors": [
              {
                "error_key": "email",
                "category": "invalid_attribute_value",
                "message": "Email is required to invite the employee to self-onboard"
              }
            ]
          },
          "employee_benefit_simple_ira_elective_mismatch": {
            "errors": [
              {
                "error_key": "elective",
                "category": "invalid_attribute_value",
                "message": "Elective must be true for matching Simple IRA benefits"
              }
            ]
          },
          "signatory_email_required": {
            "errors": [
              {
                "error_key": "email",
                "category": "invalid_attribute_value",
                "message": "Email is required"
              }
            ]
          },
          "signatory_company_already_has_signatory": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Cannot have more than one signatory in a company. Please remove the existing signatory before adding a new one."
              }
            ]
          },
          "mixed_disbursement_errors": {
            "errors": [
              {
                "error_key": "disbursements",
                "category": "nested_errors",
                "metadata": {
                  "contractor_payment_uuid": "invalid-uuid-1"
                },
                "errors": [
                  {
                    "error_key": "contractor_payment_uuid",
                    "category": "not_found",
                    "message": "Disbursement not found."
                  }
                ]
              },
              {
                "error_key": "disbursements",
                "category": "nested_errors",
                "metadata": {
                  "contractor_payment_uuid": "d0dfa222-ad08-4ea7-a06a-717688c3b179"
                },
                "errors": [
                  {
                    "error_key": "payment_method",
                    "category": "invalid_attribute_value",
                    "message": "Payment method must be one of: Direct Deposit, Check."
                  },
                  {
                    "error_key": "payment_status",
                    "category": "invalid_attribute_value",
                    "message": "Payment status is not valid for payment method 'InvalidMethod'."
                  }
                ]
              }
            ]
          },
          "not_found": {
            "errors": [
              {
                "error_key": "request",
                "category": "not_found",
                "message": "The requested resource was not found."
              }
            ]
          },
          "finish_onboarding_incomplete": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Company is not ready to exit onboarding."
              }
            ]
          },
          "federal_tax_invalid_ein": {
            "errors": [
              {
                "error_key": "ein",
                "category": "invalid_attribute_value",
                "message": "EIN must be 9 digits"
              }
            ]
          },
          "federal_tax_ein_cannot_change": {
            "errors": [
              {
                "error_key": "ein",
                "category": "invalid_attribute_value",
                "message": "EIN cannot be updated after company has been onboarded. Please contact support to update the EIN."
              }
            ]
          },
          "federal_tax_legal_name_cannot_change": {
            "errors": [
              {
                "error_key": "legal_name",
                "category": "invalid_attribute_value",
                "message": "Legal name cannot be updated after company has been onboarded. Please contact support to update the legal name."
              }
            ]
          },
          "ein_collision": {
            "errors": [
              {
                "error_key": "ein",
                "category": "invalid_attribute_value",
                "message": "EIN is already in use"
              }
            ]
          },
          "company_location_validation": {
            "errors": [
              {
                "error_key": "street_1",
                "category": "invalid_attribute_value",
                "message": "Must include a street address"
              },
              {
                "error_key": "city",
                "category": "invalid_attribute_value",
                "message": "Must include a city"
              },
              {
                "error_key": "state",
                "category": "invalid_attribute_value",
                "message": "State is in the wrong format"
              },
              {
                "error_key": "zip",
                "category": "invalid_attribute_value",
                "message": "Please enter a valid zip code (e.g. 12345)."
              },
              {
                "error_key": "phone_number",
                "category": "invalid_attribute_value",
                "message": "Phone number must be 10 digits"
              }
            ]
          },
          "conflict": {
            "errors": [
              {
                "error_key": "request",
                "category": "duplicate_operation",
                "message": "A resource with these attributes already exists."
              }
            ]
          },
          "invalid_parameter": {
            "errors": [
              {
                "error_key": "request",
                "category": "invalid_parameter",
                "message": "The provided parameter is invalid or missing."
              }
            ]
          },
          "invalid_sort_by": {
            "errors": [
              {
                "error_key": "sort_by",
                "category": "invalid_parameter",
                "message": "Invalid sort order or direction."
              }
            ]
          },
          "flow_invalid_entity": {
            "errors": [
              {
                "error_key": "entity_type",
                "category": "invalid_attribute_value",
                "message": "Invalid flow entity"
              },
              {
                "error_key": "entity_uuid",
                "category": "invalid_attribute_value",
                "message": "Invalid flow entity"
              }
            ]
          },
          "flow_nested_options_errors": {
            "errors": [
              {
                "error_key": "options",
                "category": "nested_errors",
                "metadata": {
                  "flow_type": "company_forms"
                },
                "errors": [
                  {
                    "error_key": "form_types",
                    "category": "invalid_attribute_value",
                    "message": "Supplied value 'invalid' contains no permitted values"
                  }
                ]
              }
            ]
          },
          "basic": {
            "errors": [
              {
                "error_key": "base",
                "category": "payroll_blocker",
                "message": "Company must complete all onboarding requirements in order to run payroll.",
                "metadata": {
                  "key": "needs_onboarding"
                }
              }
            ]
          },
          "contractor_already_onboarded": {
            "errors": [
              {
                "error_key": "onboarding_status",
                "category": "invalid_attribute_value",
                "message": "Contractor is already fully onboarded"
              }
            ]
          },
          "contractor_is_active_pending_dismissal": {
            "errors": [
              {
                "error_key": "is_active",
                "category": "invalid_attribute_value",
                "message": "Cannot deactivate while a dismissal is scheduled. Use the cancel termination endpoint to remove the pending dismissal first."
              }
            ]
          },
          "contractor_is_active_pending_dismissal_uncancelable": {
            "errors": [
              {
                "error_key": "is_active",
                "category": "invalid_attribute_value",
                "message": "Cannot deactivate while a non-cancelable dismissal is in progress. The dismissal has already been processed."
              }
            ]
          },
          "contractor_is_active_pending_rehire": {
            "errors": [
              {
                "error_key": "is_active",
                "category": "invalid_attribute_value",
                "message": "Cannot reactivate while a rehire is scheduled. Use the cancel rehire endpoint to remove the pending rehire first."
              }
            ]
          },
          "contractor_rehire_start_date_required": {
            "errors": [
              {
                "error_key": "start_date",
                "category": "invalid_attribute_value",
                "message": "Start date is required"
              }
            ]
          },
          "contractor_rehire_no_pending": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "No pending rehire to cancel"
              }
            ]
          },
          "contractor_termination_end_date_required": {
            "errors": [
              {
                "error_key": "end_date",
                "category": "invalid_attribute_value",
                "message": "End date is required"
              }
            ]
          },
          "contractor_termination_no_pending_dismissal": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "No pending dismissal to cancel"
              }
            ]
          },
          "contractor_address_invalid_attribute": {
            "errors": [
              {
                "error_key": "street_1",
                "category": "invalid_attribute_value",
                "message": "Must include a street address"
              }
            ]
          },
          "contractor_payment_invalid_wage": {
            "errors": [
              {
                "error_key": "wage",
                "category": "invalid_attribute_value",
                "message": "Wage must be greater than or equal to 0."
              }
            ]
          },
          "contractor_payment_cannot_cancel": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Payment has already been processed and cannot be cancelled. Contact support directly."
              }
            ]
          },
          "contractor_payment_should_not_be_funded": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This payment should not be funded."
              }
            ]
          },
          "contractor_payments_preview_no_payments": {
            "errors": [
              {
                "error_key": "contractor_payments",
                "category": "invalid_attribute_value",
                "message": "Please enter a contractor payment before continuing."
              }
            ]
          },
          "ytd_benefit_amounts_invalid_tax_year": {
            "errors": [
              {
                "error_key": "tax_year",
                "category": "invalid_attribute_value",
                "message": "Tax year must be greater than or equal to 2000"
              }
            ]
          },
          "printable_payroll_checks_invalid_printing_format": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Invalid printing_format 'bad_name', only 'top' and 'bottom' supported"
              }
            ]
          },
          "recovery_case_not_redebitable": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Unable to initiate another redebit at this time. Please contact support."
              }
            ]
          },
          "recovery_case_exceeded_retries": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "You exceeded the maximum redebit attempts. Please contact support."
              }
            ]
          },
          "report_invalid_columns": {
            "errors": [
              {
                "error_key": "columns",
                "category": "invalid_attribute_value",
                "message": "Invalid column(s): unexpected_column"
              }
            ]
          },
          "general_ledger_invalid_aggregation": {
            "errors": [
              {
                "error_key": "aggregation",
                "category": "invalid_attribute_value",
                "message": "Invalid aggregation option."
              }
            ]
          },
          "report_template_invalid_report_type": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Invalid report type"
              }
            ]
          },
          "time_sheet_invalid_entries": {
            "errors": [
              {
                "error_key": "entries",
                "category": "invalid_attribute_value",
                "message": "Entries are invalid"
              }
            ]
          },
          "time_sheet_invalid_attribute": {
            "errors": [
              {
                "error_key": "time_zone",
                "category": "invalid_attribute_value",
                "message": "Time zone is invalid"
              }
            ]
          },
          "time_sheet_version_invalid": {
            "errors": [
              {
                "error_key": "version",
                "category": "invalid_attribute_value",
                "message": "Version 'somefakeversion' does not match the latest version of this object"
              }
            ]
          },
          "time_off_request_cannot_delete": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This time off request cannot be deleted."
              }
            ]
          },
          "time_off_request_cannot_approve": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Cannot approve this request."
              }
            ]
          },
          "time_off_request_missing_employer_note": {
            "errors": [
              {
                "error_key": "employer_note",
                "category": "missing_parameter",
                "message": "'employer_note' is required"
              }
            ]
          },
          "time_off_request_invalid_status_filter": {
            "errors": [
              {
                "error_key": "status",
                "category": "invalid_parameter",
                "message": "Parameter `status` contains invalid value(s): cancelled. Allowed values: pending, approved, declined, consumed."
              }
            ]
          },
          "resource": {
            "errors": [
              {
                "error_key": "first_name",
                "category": "invalid_attribute_value",
                "message": "First name is required"
              },
              {
                "error_key": "date_of_birth",
                "category": "invalid_attribute_value",
                "message": "Date of birth is not a valid date"
              }
            ]
          },
          "nested": {
            "errors": [
              {
                "error_key": "contractor_payments",
                "category": "nested_errors",
                "metadata": {
                  "contractor_uuid": "72ae4617-daa9-4ed7-85e0-18ed5d0ee835"
                },
                "errors": [
                  {
                    "error_key": "hours",
                    "category": "invalid_attribute_value",
                    "message": "Ella Fitzgerald is paid fixed wage and hours cannot be set on a contractor payment"
                  }
                ]
              },
              {
                "error_key": "contractor_payments",
                "category": "nested_errors",
                "metadata": {
                  "contractor_uuid": "2d7bf62c-babf-4a12-8292-340e2d9cab28"
                },
                "errors": [
                  {
                    "error_key": "wage",
                    "category": "invalid_attribute_value",
                    "message": "Isaiah Berlin is paid hourly and wage cannot be set on a contractor payment"
                  }
                ]
              }
            ]
          },
          "compensation_invalid_rate": {
            "errors": [
              {
                "error_key": "rate",
                "category": "invalid_attribute_value",
                "message": "Rate is not a valid number"
              }
            ]
          },
          "compensation_invalid_payment_unit": {
            "errors": [
              {
                "error_key": "payment_unit",
                "category": "invalid_attribute_value",
                "message": "Payment unit must be one of Hour, Week, Month, or Year"
              }
            ]
          },
          "compensation_already_processed": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Compensation has already been processed on payroll."
              }
            ]
          },
          "termination_already_terminated": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Employee may only have one termination"
              }
            ]
          },
          "termination_invalid_effective_date": {
            "errors": [
              {
                "error_key": "effective_date",
                "category": "invalid_attribute_value",
                "message": "Effective date is not a valid date"
              }
            ]
          },
          "termination_effective_date_required": {
            "errors": [
              {
                "error_key": "effective_date",
                "category": "invalid_attribute_value",
                "message": "Effective date is required"
              }
            ]
          },
          "termination_already_in_effect": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Employee has already been terminated"
              }
            ]
          },
          "termination_payroll_exists": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Cannot cancel a termination with a termination payroll"
              }
            ]
          },
          "termination_rehired": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Unable to modify a termination with a future rehire."
              }
            ]
          },
          "job_title_required": {
            "errors": [
              {
                "error_key": "title",
                "category": "invalid_attribute_value",
                "message": "Title is required"
              }
            ]
          },
          "job_primary_cannot_delete": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Employee's primary job cannot be set to inactive."
              }
            ]
          },
          "job_exempt_multiple_jobs": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Only hourly employees can have multiple jobs."
              }
            ]
          },
          "job_invalid_hire_date": {
            "errors": [
              {
                "error_key": "hire_date",
                "category": "invalid_attribute_value",
                "message": "Hire date is invalid"
              }
            ]
          },
          "job_duplicate_title": {
            "errors": [
              {
                "error_key": "title",
                "category": "invalid_attribute_value",
                "message": "Employee cannot have two jobs with the same title."
              }
            ]
          },
          "i9_authorization_unneeded_document_params": {
            "errors": [
              {
                "error_key": "expiration_date",
                "category": "invalid_attribute_value",
                "message": "For the submitted authorization status, expiration date is not allowed"
              },
              {
                "error_key": "document_type",
                "category": "invalid_attribute_value",
                "message": "For the submitted authorization status, document type is not allowed"
              }
            ]
          },
          "i9_authorization_not_self_onboarding": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Employee is not self-onboarding."
              }
            ]
          },
          "i9_authorization_employee_already_signed": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Employee has already signed the form."
              }
            ]
          },
          "i9_employer_sign_invalid_params": {
            "errors": [
              {
                "error_key": "signed_by_ip_address",
                "category": "invalid_attribute_value",
                "message": "Signed by IP address is invalid"
              },
              {
                "error_key": "signer_title",
                "category": "invalid_attribute_value",
                "message": "Signer title is required"
              },
              {
                "error_key": "agree",
                "category": "invalid_attribute_value",
                "message": "You must agree to sign electronically"
              },
              {
                "error_key": "signature_text",
                "category": "invalid_attribute_value",
                "message": "Signature text is required"
              }
            ]
          },
          "i9_employer_sign_employee_not_signed": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Employee has not signed I-9"
              }
            ]
          },
          "i9_employer_sign_already_signed": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "I-9 has already been signed by the employer"
              }
            ]
          },
          "i9_documents_already_signed": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "I-9 cannot be updated as it has already been signed by the employer"
              }
            ]
          },
          "i9_documents_invalid_params": {
            "errors": [
              {
                "error_key": "documents",
                "category": "nested_errors",
                "metadata": {
                  "document_type": "invalid_type"
                },
                "errors": [
                  {
                    "error_key": "document_type",
                    "category": "invalid_attribute_value",
                    "message": "Document type's value is not included in the list"
                  },
                  {
                    "error_key": "document_title",
                    "category": "invalid_attribute_value",
                    "message": "Document title's value is not included in the list"
                  }
                ]
              }
            ]
          },
          "i9_documents_not_array": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Parameter `documents` must be an array"
              }
            ]
          },
          "company_benefit_missing_benefit_type": {
            "errors": [
              {
                "error_key": "base",
                "category": "missing_parameter",
                "message": "benefit_type is required."
              }
            ]
          },
          "company_benefit_invalid_benefit_type": {
            "errors": [
              {
                "error_key": "benefit_type",
                "category": "invalid_attribute_value",
                "message": "Benefit type does not correspond with a supported benefit"
              }
            ]
          },
          "company_benefit_missing_description": {
            "errors": [
              {
                "error_key": "description",
                "category": "invalid_attribute_value",
                "message": "Description is required"
              }
            ]
          },
          "company_benefit_cannot_disable": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Company benefit cannot be disabled while employees are still enrolled"
              }
            ]
          },
          "company_benefit_cannot_change_type": {
            "errors": [
              {
                "error_key": "benefit_type",
                "category": "invalid_attribute_value",
                "message": "The associated benefit cannot be changed"
              }
            ]
          },
          "company_benefit_invalid_contribution_exclusions": {
            "errors": [
              {
                "error_key": "contribution_exclusions",
                "category": "invalid_attribute_value",
                "message": "Expected contribution_exclusions array of hashes."
              }
            ]
          },
          "employee_benefits_invalid_parameter": {
            "errors": [
              {
                "error_key": "employee_benefits",
                "category": "invalid_parameter",
                "message": "Missing or invalid parameter 'employee_benefits'."
              }
            ]
          },
          "time_off_activity_invalid_type": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_parameter",
                "message": "Expected one of: vacation, sick"
              }
            ]
          },
          "employee_benefit_negative_company_contribution": {
            "errors": [
              {
                "error_key": "company_contribution",
                "category": "invalid_attribute_value",
                "message": "Company contribution must be greater than or equal to 0"
              }
            ]
          },
          "employee_benefit_active_requires_contribution_or_deduction": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "An active employee benefit must have either a company contribution or an employee deduction"
              }
            ]
          },
          "employee_benefit_invalid_effective_date": {
            "errors": [
              {
                "error_key": "effective_date",
                "category": "invalid_attribute_value",
                "message": "Effective date is not a valid date"
              }
            ]
          },
          "employee_benefit_duplicate_type": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Employee cannot have more than one 401(k)"
              }
            ]
          },
          "employee_benefit_invalid_limit_option": {
            "errors": [
              {
                "error_key": "limit_option",
                "category": "invalid_attribute_value",
                "message": "Limit option must be one of \"Family\", \"Individual\""
              }
            ]
          },
          "employee_benefit_coverage_amount_only_for_gtl": {
            "errors": [
              {
                "error_key": "coverage_amount",
                "category": "invalid_attribute_value",
                "message": "Coverage amount is only applicable for group term life employee benefit."
              }
            ]
          },
          "employee_benefit_destroy_invalid": {
            "errors": [
              {
                "error_key": "benefit_type",
                "category": "invalid_parameter",
                "message": "This application is not permitted to modify benefits of type 100 (Other (taxable))."
              }
            ]
          },
          "company_benefit_has_employees": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "There are employees associated with this benefit, please remove these employees before deleting the benefit."
              }
            ]
          },
          "company_benefit_partnered": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This benefit is managed by the partner and cannot be deleted."
              }
            ]
          },
          "rehire_delete_already_effective": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Unable to delete the rehire that is already effective, please terminate the employee instead."
              }
            ]
          },
          "rehire_not_terminated": {
            "errors": [
              {
                "error_key": "effective_date",
                "category": "invalid_attribute_value",
                "message": "Cannot rehire if employee has not been terminated"
              }
            ]
          },
          "rehire_missing_required_fields": {
            "errors": [
              {
                "error_key": "effective_date",
                "category": "invalid_attribute_value",
                "message": "Effective date is required"
              },
              {
                "error_key": "work_location_uuid",
                "category": "invalid_attribute_value",
                "message": "Work location not found"
              },
              {
                "error_key": "file_new_hire_report",
                "category": "invalid_attribute_value",
                "message": "File new hire report is required"
              }
            ]
          },
          "rehire_invalid_work_location": {
            "errors": [
              {
                "error_key": "work_location_uuid",
                "category": "invalid_attribute_value",
                "message": "Work location not found"
              }
            ]
          },
          "rehire_no_future_employment": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "The employee does not have any future employment, please rehire the employee first."
              }
            ]
          },
          "earning_type_missing_name": {
            "errors": [
              {
                "error_key": "name",
                "category": "invalid_attribute_value",
                "message": "Name is required"
              }
            ]
          },
          "earning_type_duplicate_name": {
            "errors": [
              {
                "error_key": "name",
                "category": "invalid_attribute_value",
                "message": "There is already an earning called Bonus"
              }
            ]
          },
          "department_duplicate_title": {
            "errors": [
              {
                "error_key": "title",
                "category": "invalid_attribute_value",
                "message": "Department name has already been taken."
              }
            ]
          },
          "department_has_active_members": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "You cannot delete a department that has active team members. Please remove them first."
              }
            ]
          },
          "department_invalid_employees": {
            "errors": [
              {
                "error_key": "employees",
                "category": "invalid_attribute_value",
                "message": "Employees must be valid"
              },
              {
                "error_key": "contractors",
                "category": "invalid_attribute_value",
                "message": "Contractors must be valid"
              }
            ]
          },
          "form_already_signed": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This form has already been signed"
              }
            ]
          },
          "form_no_signature_required": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This form does not require a signature"
              }
            ]
          },
          "form_invalid_ip_address": {
            "errors": [
              {
                "error_key": "signed_by_ip_address",
                "category": "invalid_attribute_value",
                "message": "Signed by ip address is invalid"
              }
            ]
          },
          "form_preparer_not_supported": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This form does not allow preparer information"
              }
            ]
          },
          "invoice_period_invalid_format": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_parameter",
                "message": "Invalid invoice_period param format, should be 'YYYY-MM'"
              }
            ]
          },
          "invoice_period_future": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_parameter",
                "message": "Invalid invoice_period param, cannot be a future invoice period"
              }
            ]
          },
          "invoice_company_uuids_max_exceeded": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_parameter",
                "message": "Invalid company_uuids passed, max of 50"
              }
            ]
          },
          "wire_in_request_invalid_date_sent": {
            "errors": [
              {
                "error_key": "date_sent",
                "category": "invalid_attribute_value",
                "message": "Date sent must be a valid date"
              }
            ]
          },
          "wire_in_request_missing_bank_name": {
            "errors": [
              {
                "error_key": "bank_name",
                "category": "invalid_attribute_value",
                "message": "Bank name must be present"
              }
            ]
          },
          "wire_in_request_invalid_amount_sent": {
            "errors": [
              {
                "error_key": "amount_sent",
                "category": "invalid_attribute_value",
                "message": "Amount sent must be a number"
              }
            ]
          },
          "wire_in_request_additional_notes_too_long": {
            "errors": [
              {
                "error_key": "additional_notes",
                "category": "invalid_attribute_value",
                "message": "Additional notes must be less than 255 characters"
              }
            ]
          },
          "wire_in_request_not_awaiting_funds": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Wire in request status must be awaiting funds"
              }
            ]
          },
          "external_payroll_missing_check_date": {
            "errors": [
              {
                "error_key": "check_date",
                "category": "invalid_attribute_value",
                "message": "Check date is required"
              }
            ]
          },
          "external_payroll_missing_payment_period_dates": {
            "errors": [
              {
                "error_key": "payment_period_start_date",
                "category": "invalid_attribute_value",
                "message": "Payment period start date is required"
              },
              {
                "error_key": "payment_period_end_date",
                "category": "invalid_attribute_value",
                "message": "Payment period end date is required"
              }
            ]
          },
          "external_payroll_net_pay_less_than_zero": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Net pay less than zero for one or more external payroll items"
              }
            ]
          },
          "external_payroll_invalid_payroll_item": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Invalid payload or parameters"
              }
            ]
          },
          "external_payrolls_locked": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "External Payrolls have already been finalized or a payroll has already been processed."
              }
            ]
          },
          "employee_bank_account_destroy_invalid": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_attribute_value",
                "message": "Cannot delete this bank account."
              }
            ]
          },
          "external_payroll_invalid_liability_selection": {
            "errors": [
              {
                "error_key": "tax_id",
                "category": "invalid_attribute_value",
                "message": "Tax is required"
              }
            ]
          },
          "invalid_tax_liability_selection": {
            "errors": [
              {
                "error_key": "tax_id",
                "category": "invalid_attribute_value",
                "message": "Tax is required"
              }
            ]
          },
          "external_payroll_invalid_tax_liability_selections": {
            "errors": [
              {
                "error_key": "tax_id",
                "category": "invalid_attribute_value",
                "message": "Tax liability selections are not valid"
              }
            ]
          },
          "member_portal_already_complete": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "Member has already complete member portal registration."
              }
            ]
          },
          "member_portal_not_eligible": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This member is not eligible for a member portal invitation in their current onboarding status (admin_onboarding_incomplete). Invite the member to self-onboard before sending a member portal invitation."
              }
            ]
          },
          "member_portal_member_info_incomplete_missing_start_date": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This member has not completed onboarding. Cannot proceed without member's job start date."
              }
            ]
          },
          "member_portal_member_info_incomplete_missing_email": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This member has not completed onboarding. Cannot proceed without an email."
              }
            ]
          },
          "member_portal_already_cancelled": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This invitation has already been cancelled."
              }
            ]
          },
          "member_portal_not_cancellable": {
            "errors": [
              {
                "error_key": "base",
                "category": "invalid_operation",
                "message": "This invitation is no longer cancellable."
              }
            ]
          }
        }
      },
      "Entity-Error-Object": {
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
            "description": "Specifies the type of error. The category provides error groupings and can be used to build custom error handling in your integration. If category is `nested_errors`, the object will contain a nested `errors` property with entity errors."
          },
          "message": {
            "type": "string",
            "description": "Provides details about the error - generally this message can be surfaced to an end user."
          },
          "metadata": {
            "type": "object",
            "description": "Contains relevant data to identify the resource in question when applicable. For example, to identify an entity `entity_type` and `entity_uuid` will be provided.",
            "oneOf": [
              {
                "$ref": "#/components/schemas/Metadata-With-Multiple-Entities"
              },
              {
                "$ref": "#/components/schemas/Metadata-With-One-Entity"
              }
            ]
          },
          "errors": {
            "type": "array",
            "description": "Will only exist if category is `nested_errors`. It is possible to have multiple levels of nested errors.",
            "items": {
              "type": "object",
              "properties": {
                "error_key": {
                  "type": "string",
                  "description": "Specifies where the error occurs. Typically this key identifies the attribute/parameter related to the error."
                },
                "category": {
                  "type": "string",
                  "description": "Specifies the type of error. The category provides error groupings and can be used to build custom error handling in your integration. If category is `nested_errors`, the object will contain a nested `errors` property with entity errors."
                },
                "message": {
                  "type": "string",
                  "description": "Provides details about the error - generally this message can be surfaced to an end user."
                },
                "metadata": {
                  "type": "object",
                  "description": "Contains relevant data to identify the resource in question when applicable. For example, to identify an entity `entity_type` and `entity_uuid` will be provided."
                }
              }
            }
          }
        }
      },
      "Warning-Object": {
        "type": "object",
        "properties": {
          "error_key": {
            "type": "string",
            "description": "Specifies where the warning occurs. Typically identifies the attribute or parameter related to the warning."
          },
          "category": {
            "type": "string",
            "description": "Specifies the type of warning. Can be used to build custom warning handling."
          },
          "message": {
            "type": "string",
            "description": "Provides details about the warning. The message can be surfaced directly to the end user."
          }
        }
      },
      "Metadata-With-One-Entity": {
        "type": "object",
        "description": "single entity",
        "additionalProperties": true,
        "properties": {
          "entity_type": {
            "type": "string",
            "description": "Name of the entity that the error corresponds to."
          },
          "entity_uuid": {
            "type": "string",
            "description": "Unique identifier for the entity."
          },
          "valid_from": {
            "type": [
              "string",
              "null"
            ]
          },
          "valid_up_to": {
            "type": [
              "string",
              "null"
            ]
          },
          "key": {
            "type": [
              "string",
              "null"
            ]
          },
          "state": {
            "type": [
              "string",
              "null"
            ]
          }
        }
      },
      "Metadata-With-Multiple-Entities": {
        "type": "object",
        "description": "multiple entities",
        "required": [
          "entities"
        ],
        "properties": {
          "entities": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Metadata-With-One-Entity"
            }
          }
        }
      },
      "Employee": {
        "title": "Employee",
        "type": "object",
        "description": "The representation of an employee in Gusto.",
        "x-examples": {
          "success_status": {
            "uuid": "d7282d99-ab6b-42f5-ba45-f4a670e886a8",
            "first_name": "Boaty",
            "middle_initial": null,
            "last_name": "Koss",
            "email": "keena.feest@kiehn.co.uk",
            "company_uuid": "e904cc79-818a-4da8-9d37-0be0a86fdda8",
            "manager_uuid": null,
            "version": "a5cec1f1c0135feb3e76ca6ea3c46176",
            "current_employment_status": "full_time",
            "onboarding_status": "onboarding_completed",
            "preferred_first_name": null,
            "department_uuid": null,
            "employee_code": "46f036",
            "payment_method": "Direct Deposit",
            "department": null,
            "terminated": false,
            "two_percent_shareholder": false,
            "onboarded": true,
            "historical": false,
            "has_ssn": true,
            "onboarding_documents_config": {
              "uuid": null,
              "i9_document": false
            },
            "jobs": [
              {
                "uuid": "bc875f9d-adc5-40f6-99db-ed8470bda25f",
                "version": "863bcd01c51fcfa2468d604cffec7413",
                "employee_uuid": "d7282d99-ab6b-42f5-ba45-f4a670e886a8",
                "current_compensation_uuid": "2ec164d0-808b-446c-8120-8cfb500945d0",
                "payment_unit": "Year",
                "primary": true,
                "two_percent_shareholder": false,
                "state_wc_covered": null,
                "state_wc_class_code": null,
                "title": "",
                "compensations": [
                  {
                    "uuid": "2ec164d0-808b-446c-8120-8cfb500945d0",
                    "employee_uuid": "d7282d99-ab6b-42f5-ba45-f4a670e886a8",
                    "version": "db7bfb49a4f0893432cb562311bfcad9",
                    "payment_unit": "Year",
                    "flsa_status": "Exempt",
                    "adjust_for_minimum_wage": false,
                    "minimum_wages": [],
                    "job_uuid": "bc875f9d-adc5-40f6-99db-ed8470bda25f",
                    "effective_date": "2025-06-09",
                    "rate": "80000.00"
                  }
                ],
                "rate": "80000.00",
                "hire_date": "2024-06-09"
              }
            ],
            "eligible_paid_time_off": [],
            "terminations": [],
            "garnishments": [],
            "date_of_birth": "2005-06-09",
            "ssn": "",
            "phone": null,
            "work_email": null,
            "member_portal_invitation_status": {
              "status": "sent",
              "token_expired": false,
              "welcome_email_sent_at": "2024-01-15T14:30:00Z",
              "last_password_resent_at": null
            },
            "partner_portal_invitation_sent": true
          }
        },
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the employee in Gusto.",
            "readOnly": true
          },
          "first_name": {
            "type": "string"
          },
          "middle_initial": {
            "type": [
              "string",
              "null"
            ]
          },
          "last_name": {
            "type": "string"
          },
          "email": {
            "type": [
              "string",
              "null"
            ],
            "description": "The personal email address of the employee. This is provided to support syncing users between our system and yours. You may not use this email address for any other purpose (e.g. marketing)."
          },
          "company_uuid": {
            "type": "string",
            "description": "The UUID of the company the employee is employed by.",
            "readOnly": true
          },
          "manager_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the employee's manager.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the employee. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field.",
            "readOnly": true
          },
          "department": {
            "type": [
              "string",
              "null"
            ],
            "description": "The employee's department in the company.",
            "readOnly": true
          },
          "terminated": {
            "type": "boolean",
            "description": "Whether the employee is terminated.",
            "readOnly": true
          },
          "two_percent_shareholder": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether the employee is a two percent shareholder of the company. This field only applies to companies with an S-Corp entity type."
          },
          "work_email": {
            "type": [
              "string",
              "null"
            ],
            "description": "The work email address of the employee. This is provided to support syncing users between our system and yours. You may not use this email address for any other purpose (e.g. marketing)."
          },
          "onboarded": {
            "type": "boolean",
            "description": "Whether the employee has completed onboarding.",
            "readOnly": true
          },
          "onboarding_status": {
            "description": "The current onboarding status of the employee",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "onboarding_completed",
                  "admin_onboarding_incomplete",
                  "self_onboarding_pending_invite",
                  "self_onboarding_invited",
                  "self_onboarding_invited_started",
                  "self_onboarding_invited_overdue",
                  "self_onboarding_completed_by_employee",
                  "self_onboarding_awaiting_admin_review"
                ]
              },
              {
                "type": "null"
              }
            ],
            "readOnly": true
          },
          "onboarding_documents_config": {
            "type": "object",
            "description": "Configuration for an employee onboarding documents during onboarding",
            "properties": {
              "uuid": {
                "type": [
                  "string",
                  "null"
                ],
                "description": "The UUID of the onboarding documents config",
                "readOnly": true
              },
              "i9_document": {
                "type": "boolean",
                "description": "Whether to include Form I-9 for an employee during onboarding",
                "readOnly": true
              }
            }
          },
          "jobs": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Job"
            }
          },
          "eligible_paid_time_off": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Paid-Time-Off"
            }
          },
          "terminations": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Termination"
            }
          },
          "garnishments": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Garnishment"
            }
          },
          "custom_fields": {
            "type": "array",
            "description": "Custom fields are only included for the employee if the include param has the custom_fields value set",
            "items": {
              "$ref": "#/components/schemas/Employee-Custom-Field"
            }
          },
          "date_of_birth": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": true
          },
          "has_ssn": {
            "type": "boolean",
            "description": "Indicates whether the employee has an SSN in Gusto."
          },
          "ssn": {
            "type": "string",
            "description": "Deprecated. This field always returns an empty string."
          },
          "phone": {
            "type": [
              "string",
              "null"
            ]
          },
          "preferred_first_name": {
            "type": [
              "string",
              "null"
            ],
            "description": ""
          },
          "payment_method": {
            "type": "string",
            "description": "The employee's payment method",
            "enum": [
              "Direct Deposit",
              "Check"
            ],
            "default": "Check",
            "nullable": false
          },
          "current_employment_status": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "full_time",
                  "part_time_under_twenty_hours",
                  "part_time_twenty_plus_hours",
                  "variable",
                  "seasonal"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The current employment status of the employee. Full-time employees work 30+ hours per week. Part-time employees are split into two groups: those that work 20-29 hours a week, and those that work under 20 hours a week. Variable employees have hours that vary each week. Seasonal employees are hired for 6 months of the year or less.",
            "readOnly": true
          },
          "historical": {
            "type": "boolean",
            "nullable": false
          },
          "employee_code": {
            "type": "string",
            "description": "The short format code of the employee",
            "nullable": false,
            "readOnly": true
          },
          "department_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the department the employee is under"
          },
          "title": {
            "type": "string",
            "nullable": false
          },
          "hired_at": {
            "type": "string",
            "nullable": false,
            "format": "date",
            "description": "The date when the employee was hired to the company"
          },
          "hidden_ssn": {
            "type": "string",
            "nullable": false
          },
          "flsa_status": {
            "$ref": "#/components/schemas/Flsa-Status-Type"
          },
          "applicable_tax_ids": {
            "type": "array",
            "nullable": false,
            "items": {
              "type": "number"
            }
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
            "description": "Whether an external partner portal invitation webhook has been sent for this employee. Only included when the include param has the portal_invitations value set."
          }
        },
        "required": [
          "uuid",
          "first_name",
          "last_name"
        ],
        "readOnly": true
      },
      "Job": {
        "title": "Job",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the job.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee to which the job belongs.",
            "readOnly": true
          },
          "hire_date": {
            "type": "string",
            "readOnly": false,
            "description": "The date when the employee was hired or rehired for the job."
          },
          "title": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false,
            "default": null,
            "description": "The title for the job."
          },
          "primary": {
            "type": "boolean",
            "description": "Whether this is the employee's primary job. The value will be set to true unless an existing job exists for the employee.",
            "readOnly": true
          },
          "rate": {
            "type": "string",
            "description": "The employee's pay rate for this job (e.g., hourly wage or annual salary). This is sensitive compensation data and requires the `compensations:read` scope.",
            "readOnly": true
          },
          "payment_unit": {
            "type": [
              "string",
              "null"
            ],
            "description": "How the employee is paid for this job (e.g., Hour, Week, Month, Year, Paycheck). This is sensitive compensation data and requires the `compensations:read` scope.",
            "readOnly": true
          },
          "current_compensation_uuid": {
            "type": "string",
            "description": "The UUID of the current active compensation record for this job. Requires the `compensations:read` scope.",
            "readOnly": true
          },
          "two_percent_shareholder": {
            "type": "boolean",
            "description": "Whether the employee owns at least 2% of the company.",
            "readOnly": false
          },
          "state_wc_covered": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "Whether this job is eligible for workers' compensation coverage in the state of Washington (WA).",
            "readOnly": false
          },
          "state_wc_class_code": {
            "type": [
              "string",
              "null"
            ],
            "description": "The risk class code for workers' compensation in Washington state. Please visit [Washington state's Risk Class page](https://www.lni.wa.gov/insurance/rates-risk-classes/risk-classes-for-workers-compensation/risk-class-lookup#/) to learn more.",
            "readOnly": false
          },
          "compensations": {
            "type": "array",
            "description": "The compensation history for this job, including pay rate, payment unit, FLSA status, and effective dates. This is sensitive pay information and requires the `compensations:read` scope.",
            "items": {
              "$ref": "#/components/schemas/Compensation"
            },
            "readOnly": true
          },
          "location_uuid": {
            "type": "string",
            "nullable": false,
            "description": "The uuid of the employee's work location."
          },
          "location": {
            "$ref": "#/components/schemas/Location"
          }
        },
        "description": "The representation of a job in Gusto.",
        "required": [
          "uuid"
        ],
        "x-examples": {
          "example": {
            "uuid": "d6d1035e-8a21-4e1d-89d5-fa894f9aff97",
            "version": "gr78930htutrz444kuytr3s5hgxykuveb523fwl8sir",
            "employee_uuid": "948daac8-4355-4ece-9e2a-229898accb22",
            "hire_date": "2020-01-20",
            "title": "Account Director",
            "primary": true,
            "rate": "78000.00",
            "payment_unit": "Year",
            "current_compensation_uuid": "ea8b0b90-1112-4f9d-bb93-bf029bc8537a",
            "two_percent_shareholder": false,
            "state_wc_covered": null,
            "state_wc_class_code": null,
            "compensations": [
              {
                "uuid": "ea8b0b90-1112-4f9d-bb93-bf029bc8537a",
                "version": "98jr3289h3298hr9329gf9egskt3tjaj",
                "job_uuid": "d6d1035e-8a21-4e1d-89d5-fa894f9aff97",
                "employee_uuid": "948daac8-4355-4ece-9e2a-229898accb22",
                "rate": "78000.00",
                "payment_unit": "Year",
                "flsa_status": "Exempt",
                "effective_date": "2020-01-20",
                "adjust_for_minimum_wage": false,
                "minimum_wages": []
              }
            ]
          },
          "secondary_job": {
            "uuid": "a1b2c3d4-5678-9012-abcd-ef1234567890",
            "version": "hj29fh3298hf9832hf98h32f89h32f89h32f9832",
            "employee_uuid": "948daac8-4355-4ece-9e2a-229898accb22",
            "hire_date": "2020-01-20",
            "title": "Senior Consultant",
            "primary": false,
            "rate": "25.00",
            "payment_unit": "Hour",
            "current_compensation_uuid": "b2c3d4e5-6789-0123-bcde-f12345678901",
            "two_percent_shareholder": false,
            "state_wc_covered": null,
            "state_wc_class_code": null,
            "compensations": [
              {
                "uuid": "b2c3d4e5-6789-0123-bcde-f12345678901",
                "version": "93jr2398h23r9832rg9832rg98ewrg98e",
                "job_uuid": "a1b2c3d4-5678-9012-abcd-ef1234567890",
                "employee_uuid": "948daac8-4355-4ece-9e2a-229898accb22",
                "rate": "25.00",
                "payment_unit": "Hour",
                "flsa_status": "Nonexempt",
                "effective_date": "2020-01-20",
                "adjust_for_minimum_wage": false,
                "minimum_wages": []
              }
            ]
          }
        }
      },
      "Compensation": {
        "type": "object",
        "description": "The representation of compensation in Gusto.",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the compensation in Gusto.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "job_uuid": {
            "type": "string",
            "description": "The UUID of the job to which the compensation belongs.",
            "readOnly": true
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee to which the compensation belongs.",
            "readOnly": true
          },
          "rate": {
            "type": "string",
            "readOnly": false,
            "description": "The dollar amount paid per payment unit."
          },
          "payment_unit": {
            "type": "string",
            "readOnly": false,
            "description": "The unit accompanying the compensation rate. If the employee is an owner, rate should be 'Paycheck'.",
            "enum": [
              "Hour",
              "Week",
              "Month",
              "Year",
              "Paycheck"
            ]
          },
          "flsa_status": {
            "$ref": "#/components/schemas/Flsa-Status-Type"
          },
          "title": {
            "type": "string",
            "description": "The job title for this compensation."
          },
          "effective_date": {
            "type": "string",
            "readOnly": false,
            "description": "The effective date for this compensation. For the first compensation, this defaults to the job's hire date."
          },
          "adjust_for_minimum_wage": {
            "type": "boolean",
            "description": "Indicates if the compensation could be adjusted to minimum wage during payroll calculation.",
            "readOnly": true
          },
          "minimum_wages": {
            "type": "array",
            "readOnly": false,
            "description": "The minimum wages associated with the compensation.",
            "items": {
              "type": "object",
              "properties": {
                "uuid": {
                  "type": "string",
                  "description": "The UUID of the minimum wage."
                },
                "wage": {
                  "type": "string",
                  "description": "The wage amount."
                },
                "effective_date": {
                  "type": "string",
                  "description": "The effective date of the minimum wage."
                }
              }
            }
          }
        },
        "required": [
          "uuid"
        ],
        "x-examples": {
          "success_status": {
            "uuid": "db4d41e5-813c-477e-bfae-38da2ae5e7a3",
            "version": "56d00c178bc7393b2a206ed6a86afcb4",
            "job_uuid": "c1fdb417-c34a-43a7-92f3-5e6c20c1d7a4",
            "employee_uuid": "a7e8f9bc-0d12-4e56-b789-012345678901",
            "rate": "70000.00",
            "payment_unit": "Year",
            "flsa_status": "Exempt",
            "effective_date": "2023-01-01",
            "adjust_for_minimum_wage": false,
            "minimum_wages": [],
            "title": "Software Engineer"
          },
          "hourly_compensation": {
            "uuid": "e5f6a7b8-c9d0-1234-e5f6-a7b8c9d01234",
            "version": "98b7a6c5d4e3f2a1b0c9d8e7f6a5b4c3",
            "job_uuid": "d2e5f8a1-b4c7-4d90-a3e6-f9b2c5d8e1a4",
            "employee_uuid": "b8f9a0bc-1e23-4f67-c890-123456789012",
            "rate": "25.00",
            "payment_unit": "Hour",
            "flsa_status": "Nonexempt",
            "effective_date": "2023-01-01",
            "adjust_for_minimum_wage": false,
            "minimum_wages": [],
            "title": "Associate"
          },
          "minimum_wage_adjusted": {
            "uuid": "a4d9ba9c-32cc-4cc1-a5bc-6ef4cd653e7a",
            "version": "cc59bd3879d655fb940a1f6b675f2ad9",
            "job_uuid": "d8f8fbe7-496d-4b69-86f0-1e2d1b73a086",
            "rate": "5.00",
            "payment_unit": "Hour",
            "flsa_status": "Nonexempt",
            "effective_date": "2018-12-11",
            "adjust_for_minimum_wage": true,
            "minimum_wages": [
              {
                "uuid": "edeea5af-ecd6-4b1c-b5de-5cff2d302738",
                "wage": "7.25",
                "effective_date": "2018-12-11"
              }
            ]
          }
        }
      },
      "Paid-Time-Off": {
        "type": "object",
        "description": "The representation of paid time off in Gusto.",
        "properties": {
          "name": {
            "description": "The name of the paid time off type.",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "Vacation Hours",
                  "Sick Hours",
                  "Holiday Hours"
                ]
              },
              {
                "type": "null"
              }
            ],
            "readOnly": true
          },
          "policy_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The name of the time off policy.",
            "readOnly": true
          },
          "policy_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the time off policy.",
            "readOnly": true
          },
          "accrual_unit": {
            "type": [
              "string",
              "null"
            ],
            "example": "Hour",
            "description": "The unit the PTO type is accrued in.",
            "readOnly": true
          },
          "accrual_rate": {
            "type": [
              "string",
              "null"
            ],
            "description": "The number of accrual units accrued per accrual period.",
            "readOnly": true
          },
          "accrual_method": {
            "type": [
              "string",
              "null"
            ],
            "example": "unlimited",
            "description": "The accrual method of the time off policy",
            "readOnly": true
          },
          "accrual_period": {
            "type": [
              "string",
              "null"
            ],
            "example": "Year",
            "description": "The frequency at which the PTO type is accrued.",
            "readOnly": true
          },
          "accrual_balance": {
            "type": [
              "string",
              "null"
            ],
            "description": "The number of accrual units accrued.",
            "readOnly": true
          },
          "maximum_accrual_balance": {
            "type": [
              "string",
              "null"
            ],
            "description": "The maximum number of accrual units allowed. A null value signifies no maximum.",
            "readOnly": true
          },
          "paid_at_termination": {
            "type": "boolean",
            "description": "Whether the accrual balance is paid to the employee upon termination.",
            "readOnly": true
          }
        }
      },
      "Termination": {
        "type": "object",
        "description": "The representation of a termination in Gusto.",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the termination object.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee to which this termination is attached.",
            "readOnly": true
          },
          "active": {
            "type": "boolean",
            "description": "Whether the employee's termination has gone into effect.",
            "readOnly": true
          },
          "cancelable": {
            "type": "boolean",
            "description": "Whether the employee's termination is cancelable. Cancelable is true if `run_termination_payroll` is false and `effective_date` is in the future.",
            "readOnly": true
          },
          "effective_date": {
            "type": "string",
            "readOnly": false,
            "description": "The employee's last day of work."
          },
          "run_termination_payroll": {
            "type": "boolean",
            "readOnly": false,
            "description": "If true, the employee should receive their final wages via an off-cycle payroll. If false, they should receive their final wages on their current pay schedule."
          }
        },
        "required": [
          "uuid"
        ],
        "x-examples": {
          "terminated_employee": {
            "uuid": "da441196-43a9-4d23-ad5d-f37ce6bb99c0",
            "employee_uuid": "da441196-43a9-4d23-ad5d-f37ce6bb99c0",
            "version": "d487dd0b55dfcacdd920ccbdaeafa351",
            "active": true,
            "cancelable": false,
            "effective_date": "2024-01-15",
            "run_termination_payroll": false
          },
          "cancelable_termination": {
            "uuid": "da441196-43a9-4d23-ad5d-f37ce6bb99c0",
            "employee_uuid": "da441196-43a9-4d23-ad5d-f37ce6bb99c0",
            "version": "d487dd0b55dfcacdd920ccbdaeafa351",
            "active": false,
            "cancelable": true,
            "effective_date": "2024-06-15",
            "run_termination_payroll": false
          }
        }
      },
      "Garnishment": {
        "description": "Garnishments, or employee deductions, are fixed amounts or percentages deducted from an employee’s pay. They can be deducted a specific number of times or on a recurring basis. Garnishments can also have maximum deductions on a yearly or per-pay-period bases. Common uses for garnishments are court-ordered payments for child support or back taxes. Some companies provide loans to their employees that are repaid via garnishments.",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the garnishment in Gusto.",
            "readOnly": true
          },
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee to which this garnishment belongs.",
            "readOnly": true
          },
          "active": {
            "type": "boolean",
            "default": true,
            "description": "Whether or not this garnishment is currently active."
          },
          "amount": {
            "type": "string",
            "format": "float",
            "readOnly": false,
            "description": "The amount of the garnishment. Either a percentage or a fixed dollar amount. Represented as a float, e.g. \"8.00\"."
          },
          "description": {
            "type": "string",
            "readOnly": false,
            "description": "The description of the garnishment."
          },
          "court_ordered": {
            "type": "boolean",
            "readOnly": false,
            "description": "Whether the garnishment is court ordered."
          },
          "times": {
            "type": [
              "integer",
              "null"
            ],
            "readOnly": false,
            "default": null,
            "description": "The number of times to apply the garnishment. Ignored if recurring is true."
          },
          "recurring": {
            "type": "boolean",
            "readOnly": false,
            "default": false,
            "description": "Whether the garnishment should recur indefinitely."
          },
          "annual_maximum": {
            "format": "float",
            "readOnly": false,
            "default": null,
            "description": "The maximum deduction per annum. A null value indicates no maximum. Represented as a float, e.g. \"200.00\".",
            "type": [
              "string",
              "null"
            ]
          },
          "total_amount": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "readOnly": false,
            "default": null,
            "description": "A maximum total deduction for the lifetime of this garnishment. A null value indicates no maximum."
          },
          "pay_period_maximum": {
            "type": [
              "string",
              "null"
            ],
            "format": "float",
            "default": null,
            "description": "The maximum deduction per pay period. A null value indicates no maximum. Represented as a float, e.g. \"16.00\"."
          },
          "deduct_as_percentage": {
            "type": "boolean",
            "readOnly": false,
            "default": false,
            "description": "Whether the amount should be treated as a percentage to be deducted per pay period."
          },
          "garnishment_type": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "child_support",
                  "federal_tax_lien",
                  "state_tax_lien",
                  "student_loan",
                  "creditor_garnishment",
                  "federal_loan",
                  "other_garnishment"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The specific type of garnishment for court ordered garnishments."
          },
          "child_support": {
            "$ref": "#/components/schemas/Garnishment-Child-Support"
          }
        },
        "required": [
          "uuid"
        ],
        "x-examples": {
          "Example": {
            "uuid": "4c7841a2-1363-497e-bc0f-664703c7484f",
            "version": "52b7c567242cb7452e89ba2bc02cb476",
            "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
            "active": true,
            "amount": "8.00",
            "description": "Company loan to employee",
            "court_ordered": false,
            "times": 5,
            "recurring": false,
            "annual_maximum": null,
            "total_amount": null,
            "pay_period_maximum": "100.00",
            "deduct_as_percentage": true,
            "garnishment_type": null,
            "child_support": null
          },
          "Create-Example": {
            "uuid": "4c7841a2-1363-497e-bc0f-664703c7484f",
            "version": "52b7c567242cb7452e89ba2bc02cb476",
            "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
            "active": true,
            "amount": "150.00",
            "description": "Back taxes",
            "court_ordered": true,
            "times": null,
            "recurring": true,
            "annual_maximum": null,
            "total_amount": null,
            "pay_period_maximum": null,
            "deduct_as_percentage": false,
            "garnishment_type": null,
            "child_support": null
          },
          "Child-Support-Example": {
            "uuid": "4c7841a2-1363-497e-bc0f-664703c7481a",
            "version": "52b7c567242cb7452e89ba2bc02cb383",
            "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
            "active": true,
            "amount": "40.00",
            "description": "Child support - AZ28319",
            "court_ordered": true,
            "times": null,
            "recurring": true,
            "annual_maximum": null,
            "total_amount": null,
            "pay_period_maximum": "400.00",
            "deduct_as_percentage": true,
            "garnishment_type": "child_support",
            "child_support": {
              "state": "AZ",
              "payment_period": "Monthly",
              "case_number": "AZ28319",
              "order_number": null,
              "remittance_number": null,
              "fips_code": "04000"
            }
          },
          "Garnishment-List": [
            {
              "uuid": "4c7841a2-1363-497e-bc0f-664703c7484f",
              "version": "52b7c567242cb7452e89ba2bc02cb476",
              "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
              "active": true,
              "amount": "8.00",
              "description": "Company loan to employee",
              "court_ordered": false,
              "times": 5,
              "recurring": false,
              "annual_maximum": null,
              "total_amount": null,
              "pay_period_maximum": "100.00",
              "deduct_as_percentage": true,
              "garnishment_type": null,
              "child_support": null
            },
            {
              "uuid": "4c7841a2-1363-497e-bc0f-664703c7481a",
              "version": "52b7c567242cb7452e89ba2bc02cb383",
              "employee_uuid": "a6b53294-f871-4db2-bbd4-8c3d1fe56440",
              "active": true,
              "amount": "40.00",
              "description": "Child support - AZ28319",
              "court_ordered": true,
              "times": null,
              "recurring": true,
              "annual_maximum": null,
              "total_amount": null,
              "pay_period_maximum": "400.00",
              "deduct_as_percentage": true,
              "garnishment_type": "child_support",
              "child_support": {
                "state": "AZ",
                "payment_period": "Monthly",
                "case_number": "AZ28319",
                "order_number": null,
                "remittance_number": null,
                "fips_code": "04000"
              }
            }
          ]
        }
      },
      "Garnishment-Child-Support": {
        "description": "Additional child support order details",
        "type": [
          "object",
          "null"
        ],
        "properties": {
          "state": {
            "type": "string",
            "readOnly": false,
            "description": "The two letter state abbreviation for the state issuing the child support order. Agency data is available in the `GET /v1/garnishments/child_support` API."
          },
          "payment_period": {
            "type": "string",
            "readOnly": false,
            "enum": [
              "Every week",
              "Every other week",
              "Twice per month",
              "Monthly"
            ],
            "description": "How often the agency collects the withholding amount. e.g. $500 monthly -> `Monthly`."
          },
          "fips_code": {
            "type": "string",
            "description": "The FIPS code associated with the state or county agency issuing the child support order. Agency data is available in the `GET /v1/garnishments/child_support` API.",
            "nullable": false,
            "readOnly": false
          },
          "case_number": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false,
            "description": "Child Support Enforcement Case Number associated with this child support obligation - required for most states. Agency specific requirements are available in the `GET /v1/garnishments/child_support` API."
          },
          "order_number": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false,
            "description": "Order Identifier or Order ID associated with this child support obligation - required for some states. Agency specific requirements are available in the `GET /v1/garnishments/child_support` API."
          },
          "remittance_number": {
            "type": [
              "string",
              "null"
            ],
            "readOnly": false,
            "description": "Child Support Enforcement Remittance ID associated with this child support obligation - required for some states. Agency specific requirements are available in the `GET /v1/garnishments/child_support` API."
          }
        }
      },
      "Employee-Custom-Field": {
        "type": "object",
        "description": "A custom field of an employee",
        "properties": {
          "id": {
            "type": "string"
          },
          "company_custom_field_id": {
            "type": "string",
            "description": "This is the id of the response object from when you get the company custom fields"
          },
          "name": {
            "type": "string"
          },
          "type": {
            "$ref": "#/components/schemas/Custom-Field-Type"
          },
          "description": {
            "type": [
              "string",
              "null"
            ]
          },
          "value": {
            "type": "string"
          },
          "selection_options": {
            "type": [
              "array",
              "null"
            ],
            "description": "An array of options for fields of type radio. Otherwise, null.",
            "items": {
              "type": "string"
            }
          }
        },
        "required": [
          "id",
          "company_custom_field_id",
          "name",
          "type",
          "value"
        ],
        "x-examples": {
          "example_text_field": {
            "id": "ee515986-f3ca-49da-b576-2691b95262f9",
            "company_custom_field_id": "ea7e5d57-6abb-47d7-b654-347c142886c0",
            "name": "employee_level",
            "description": "Employee Level",
            "type": "text",
            "value": "2",
            "selection_options": null
          },
          "example_radio_field": {
            "id": "3796e08d-c2e3-434c-b4de-4ce1893e7b59",
            "company_custom_field_id": "024ec137-6c92-43a3-b061-14a9720531d6",
            "name": "favorite fruit",
            "description": "Which is your favorite fruit?",
            "type": "radio",
            "value": "apple",
            "selection_options": [
              "apple",
              "banana",
              "orange"
            ]
          }
        }
      },
      "Custom-Field-Type": {
        "type": "string",
        "description": "Input type for the custom field.",
        "enum": [
          "text",
          "currency",
          "number",
          "date",
          "radio"
        ]
      },
      "Flsa-Status-Type": {
        "type": "string",
        "enum": [
          "Exempt",
          "Salaried Nonexempt",
          "Nonexempt",
          "Owner",
          "Commission Only Exempt",
          "Commission Only Nonexempt"
        ],
        "description": "The FLSA status for this compensation. Salaried ('Exempt') employees are paid a fixed salary every pay period. Salaried with overtime ('Salaried Nonexempt') employees are paid a fixed salary every pay period, and receive overtime pay when applicable. Hourly ('Nonexempt') employees are paid for the hours they work, and receive overtime pay when applicable. Commissioned employees ('Commission Only Exempt') earn wages based only on commission. Commissioned with overtime ('Commission Only Nonexempt') earn wages based on commission, and receive overtime pay when applicable. Owners ('Owner') are employees that own at least twenty percent of the company. "
      },
      "Historical-Employee-Body": {
        "type": "object",
        "description": "Request body for creating or updating a **historical employee**—someone who already separated from the company and must appear on year-to-date or tax filings without receiving ongoing payroll.\n\nSend this object under the JSON root key `employee`. All dates are ISO 8601 (`YYYY-MM-DD`). Use a `work_address.location_uuid` returned from your company locations API for an active work site.\n",
        "properties": {
          "first_name": {
            "type": "string",
            "description": "Legal first name as it appears on government-issued identification.",
            "example": "Soren"
          },
          "middle_initial": {
            "type": "string",
            "description": "Single middle initial, if any.",
            "example": "A"
          },
          "last_name": {
            "type": "string",
            "description": "Legal last name as it appears on government-issued identification.",
            "example": "Kierkegaard"
          },
          "preferred_first_name": {
            "type": "string",
            "description": "Preferred given name for display; omit when the same as legal first name.",
            "example": "Angel"
          },
          "date_of_birth": {
            "type": "string",
            "format": "date",
            "description": "Date of birth (YYYY-MM-DD).",
            "example": "1995-05-05"
          },
          "ssn": {
            "type": "string",
            "pattern": "[0-9]{9}",
            "description": "Nine-digit U.S. Social Security number **without** dashes or spaces. Must pass Gusto/SSA validation in production; use a valid test SSN in sandbox environments.\n",
            "example": "123456294"
          },
          "work_address": {
            "type": "object",
            "description": "Primary work location for this historical employment row.",
            "required": [
              "location_uuid"
            ],
            "properties": {
              "location_uuid": {
                "type": "string",
                "format": "uuid",
                "description": "UUID of a company work location from the company locations response.",
                "example": "1da85d35-1910-40a7-9c1f-8e2b3d4c5a6f"
              }
            }
          },
          "home_address": {
            "type": "object",
            "description": "Residential address on file for tax withholding and compliance mail.",
            "properties": {
              "street_1": {
                "type": "string",
                "description": "Street address line 1.",
                "example": "55 Mission St"
              },
              "street_2": {
                "type": [
                  "string",
                  "null"
                ],
                "description": "Apartment, suite, unit, or building (optional).",
                "example": "Floor 3"
              },
              "city": {
                "type": "string",
                "description": "City.",
                "example": "San Francisco"
              },
              "state": {
                "type": "string",
                "description": "Two-letter U.S. state or territory postal abbreviation.",
                "example": "CA"
              },
              "zip": {
                "type": "string",
                "description": "ZIP or ZIP+4.",
                "example": "94105"
              }
            },
            "required": [
              "street_1",
              "city",
              "state",
              "zip"
            ]
          },
          "termination": {
            "type": "object",
            "description": "End of the historical employment period.",
            "required": [
              "effective_date"
            ],
            "properties": {
              "effective_date": {
                "type": "string",
                "format": "date",
                "description": "Last day of employment (termination date). This is recorded on the employment; use the calendar date the person stopped working for the company.",
                "example": "2022-01-01"
              }
            }
          },
          "email": {
            "type": "string",
            "format": "email",
            "description": "Optional. When provided, stored on the employee record for notifications and profile.",
            "example": "soren.kierkegaard@example.com"
          },
          "job": {
            "type": "object",
            "description": "Hire date for the historical job used to build employments and filings.",
            "required": [
              "hire_date"
            ],
            "properties": {
              "hire_date": {
                "type": "string",
                "format": "date",
                "description": "First calendar day the employee was employed in this role at the company.",
                "example": "2020-01-01"
              }
            }
          },
          "employee_state_taxes": {
            "type": "object",
            "description": "Workers' compensation fields for Washington (WA) or Wyoming (WY) when the work address is in those states; omit when not applicable.",
            "properties": {
              "wc_covered": {
                "type": "boolean",
                "description": "Whether this job is eligible for workers' compensation coverage in the states of Washington (WA) or Wyoming (WY).",
                "example": true
              },
              "wc_class_code": {
                "type": "string",
                "description": "The risk class code for workers' compensation in Washington or Wyoming state. For Washington, visit [Washington state's Risk Class page](https://www.lni.wa.gov/insurance/rates-risk-classes/risk-classes-for-workers-compensation/risk-class-lookup#/) to learn more. For Wyoming you can search for the code online using [WY Workforce Services website](https://dws.wyo.gov/dws-division/workers-compensation/) or call the agency at (307) 235-3217.",
                "example": "051000"
              }
            }
          }
        },
        "required": [
          "first_name",
          "last_name",
          "date_of_birth",
          "ssn",
          "work_address",
          "home_address",
          "job",
          "termination"
        ],
        "x-examples": {
          "typical_historical_employee": {
            "first_name": "Soren",
            "middle_initial": "A",
            "last_name": "Kierkegaard",
            "preferred_first_name": "Angel",
            "date_of_birth": "1995-05-05",
            "ssn": "123456294",
            "email": "soren.kierkegaard@example.com",
            "work_address": {
              "location_uuid": "1da85d35-1910-40a7-9c1f-8e2b3d4c5a6f"
            },
            "home_address": {
              "street_1": "55 Mission St",
              "street_2": "Floor 3",
              "city": "San Francisco",
              "state": "CA",
              "zip": "94105"
            },
            "job": {
              "hire_date": "2020-01-01"
            },
            "termination": {
              "effective_date": "2022-01-01"
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
    "/v1/companies/{company_uuid}/historical_employees/{historical_employee_uuid}": {
      "put": {
        "summary": "Update a historical employee",
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
            "description": "The UUID of the company that will employ this historical record.",
            "example": "7b1d0df1-6403-4a06-8768-c1dd7d24d27a",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "historical_employee_uuid",
            "in": "path",
            "required": true,
            "description": "The UUID of the historical employee returned from create or list responses.",
            "example": "a2b3c4d-5e6f-7890-abcd-ef1234567890",
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "put-v1-historical_employees",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Update a historical employee, an employee that was previously dismissed from the company in the current year.\n\nscope: `employees:manage employees:write`",
        "tags": [
          "Employees"
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
                      "$ref": "#/components/schemas/Employee/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee"
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
          },
          "422": {
            "description": "Unprocessable Entity\n\nThis may happen when the body of your request contains errors such as `invalid_attribute_value`, or the request fails due to an `invalid_operation`. See the [Errors Categories](https://docs.gusto.com/embedded-payroll/docs/error-categories) guide for more details.\n",
            "content": {
              "application/json": {
                "examples": {
                  "invalid_attribute": {
                    "value": {
                      "$ref": "#/components/schemas/Unprocessable-Entity-Error-Object/x-examples/invalid_attribute"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Unprocessable-Entity-Error-Object"
                }
              }
            }
          }
        },
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "allOf": [
                  {
                    "$ref": "#/components/schemas/Versionable-Required"
                  },
                  {
                    "$ref": "#/components/schemas/Historical-Employee-Body"
                  }
                ]
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
