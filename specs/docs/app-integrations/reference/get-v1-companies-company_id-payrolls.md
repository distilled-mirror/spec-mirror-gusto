---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all payrolls for a company

Returns a list of payrolls for a company. You can change the payrolls returned by updating the processing_status, payroll_types, start_date, & end_date params.

By default, will return processed, regular payrolls for the past 6 months.

Notes:
* Dollar amounts are returned as string representations of numeric decimals, are represented to the cent.
* end_date can be at most 3 months in the future and start_date and end_date can't be more than 1 year apart.
* Results are paginated. Maximum page size is 100 payrolls per request; the default page size is 25.

scope: `payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Payrolls"
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
      "Payroll-List": {
        "description": "A list of payrolls for a company.",
        "type": "array",
        "x-examples": {
          "success_status": [
            {
              "uuid": "3601a7a2-0562-4e4c-9559-20886658daac",
              "payroll_uuid": "3601a7a2-0562-4e4c-9559-20886658daac",
              "company_uuid": "b43e6012-bf6c-4752-b67b-5c8000595e0e",
              "payroll_status_meta": {
                "cancellable": false,
                "expected_check_date": "2025-06-08",
                "initial_check_date": "2025-06-27",
                "expected_debit_time": "2025-06-12T23:00:00Z",
                "payroll_late": false,
                "initial_debit_cutoff_time": "2025-06-12T23:00:00Z"
              },
              "off_cycle": false,
              "auto_payroll": false,
              "processed": true,
              "processed_date": "2025-06-11",
              "calculated_at": "2025-06-11T19:40:51Z",
              "pay_period": {
                "start_date": "2025-05-20",
                "end_date": "2025-06-04",
                "pay_schedule_uuid": "ded21d08-02d6-41cb-b211-8d8ca02f1c6a"
              },
              "check_date": "2025-06-08",
              "external": false,
              "payroll_deadline": "2025-06-12T23:00:00Z",
              "company_taxes": [],
              "created_at": "2025-06-11T19:40:51Z",
              "partner_owned_disbursement": null
            }
          ]
        },
        "items": {
          "$ref": "#/components/schemas/Payroll"
        }
      },
      "Payroll": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "uuid": "b441a30b-2adb-489e-b7b7-9d094011a3f8",
            "employee_compensations": [],
            "submission_blockers": [],
            "credit_blockers": [],
            "payroll_uuid": "b441a30b-2adb-489e-b7b7-9d094011a3f8",
            "company_uuid": "9aa93530-43d5-484e-b608-33214109420d",
            "off_cycle": false,
            "auto_payroll": false,
            "processed": true,
            "processed_date": "2025-06-16",
            "calculated_at": "2025-06-16T16:58:03Z",
            "pay_period": {
              "start_date": "2025-05-25",
              "end_date": "2025-06-09",
              "pay_schedule_uuid": "40ff5990-0191-4796-9717-32f7dd3e94d5"
            },
            "check_date": "2025-06-13",
            "external": false,
            "payroll_deadline": "2025-06-17T23:00:00Z",
            "totals": {
              "employee_bonuses": "0.00",
              "employee_commissions": "0.00",
              "employee_cash_tips": "0.00",
              "employee_paycheck_tips": "0.00",
              "additional_earnings": "0.00",
              "owners_draw": "0.00",
              "benefits": "0.00",
              "check_amount": "0.00",
              "child_support_debit": "0.00",
              "company_debit": "0.00",
              "deferred_payroll_taxes": "0.00",
              "employee_benefits_deductions": "0.00",
              "employee_taxes": "0.00",
              "employer_taxes": "0.00",
              "gross_pay": "0.00",
              "imputed_pay": "0.00",
              "net_pay": "0.00",
              "net_pay_debit": "0.00",
              "other_deductions": "0.00",
              "reimbursement_debit": "0.00",
              "reimbursements": "0.00",
              "tax_debit": "0.00"
            },
            "payroll_status_meta": {
              "cancellable": false,
              "expected_check_date": "2025-06-13",
              "initial_check_date": "2025-06-13",
              "expected_debit_time": "2025-06-17T23:00:00Z",
              "payroll_late": false,
              "initial_debit_cutoff_time": "2025-06-17T23:00:00Z"
            },
            "processing_request": {
              "status": "submit_success",
              "errors": []
            },
            "created_at": "2025-06-16T16:58:03Z",
            "partner_owned_disbursement": null
          }
        },
        "properties": {
          "payroll_deadline": {
            "$ref": "#/components/schemas/Payroll-Deadline-Type"
          },
          "check_date": {
            "$ref": "#/components/schemas/Payroll-Check-Date-Type"
          },
          "processed": {
            "$ref": "#/components/schemas/Payroll-Processed-Type"
          },
          "processed_date": {
            "$ref": "#/components/schemas/Payroll-Processed-Date-Type"
          },
          "calculated_at": {
            "$ref": "#/components/schemas/Payroll-Calculated-At-Type"
          },
          "uuid": {
            "$ref": "#/components/schemas/Payroll-Payroll-Uuid-Type"
          },
          "payroll_uuid": {
            "$ref": "#/components/schemas/Payroll-Payroll-Uuid-Type"
          },
          "company_uuid": {
            "$ref": "#/components/schemas/Payroll-Company-Uuid-Type"
          },
          "off_cycle": {
            "$ref": "#/components/schemas/Payroll-Off-Cycle-Type"
          },
          "off_cycle_reason": {
            "$ref": "#/components/schemas/Off-Cycle-Reason-Type"
          },
          "auto_payroll": {
            "$ref": "#/components/schemas/Auto-Pilot-Type"
          },
          "external": {
            "$ref": "#/components/schemas/Payroll-External-Type"
          },
          "final_termination_payroll": {
            "$ref": "#/components/schemas/Payroll-Final-Termination-Payroll-Type"
          },
          "withholding_pay_period": {
            "$ref": "#/components/schemas/Payroll-Withholding-Pay-Period-Type"
          },
          "skip_regular_deductions": {
            "$ref": "#/components/schemas/Payroll-Skip-Regular-Deductions-Type"
          },
          "fixed_withholding_rate": {
            "$ref": "#/components/schemas/Payroll-Fixed-Withholding-Rate-Type"
          },
          "pay_period": {
            "$ref": "#/components/schemas/Payroll-Pay-Period-Type"
          },
          "payroll_status_meta": {
            "$ref": "#/components/schemas/Payroll-Payroll-Status-Meta-Type"
          },
          "totals": {
            "$ref": "#/components/schemas/Payroll-Totals-Type"
          },
          "company_taxes": {
            "$ref": "#/components/schemas/Payroll-Company-Taxes-Type"
          },
          "payroll_taxes": {
            "$ref": "#/components/schemas/Payroll-Taxes-Type"
          },
          "payment_speed_changed": {
            "$ref": "#/components/schemas/Payroll-Payment-Speed-Changed-Type"
          },
          "created_at": {
            "$ref": "#/components/schemas/Created-At-Type"
          },
          "submission_blockers": {
            "$ref": "#/components/schemas/Payroll-Submission-Blockers-Type"
          },
          "credit_blockers": {
            "$ref": "#/components/schemas/Payroll-Credit-Blockers-Type"
          },
          "processing_request": {
            "$ref": "#/components/schemas/Payroll-Processing-Request"
          },
          "partner_owned_disbursement": {
            "$ref": "#/components/schemas/Payroll-Partner-Owned-Disbursement-Type"
          }
        }
      },
      "Payroll-Partner-Owned-Disbursement-Type": {
        "type": [
          "boolean",
          "null"
        ],
        "description": "Will money movement for the payroll be performed by the partner rather than by Gusto?"
      },
      "Payroll-Deadline-Type": {
        "type": "string",
        "format": "date-time",
        "description": "A timestamp that is the deadline for the payroll to be run in order for employees to be paid on time.  If payroll has not been run by the deadline, a prepare request will update both the check date and deadline to reflect the soonest employees can be paid and the deadline by which the payroll must be run in order for said check date to be met.",
        "readOnly": true
      },
      "Payroll-Check-Date-Type": {
        "type": "string",
        "description": "The date on which employees will be paid for the payroll.",
        "readOnly": true
      },
      "Payroll-Processed-Type": {
        "type": "boolean",
        "description": "Whether or not the payroll has been successfully processed. Note that processed payrolls cannot be updated. Additionally, a payroll is not guaranteed to be processed just because the payroll deadline has passed. Late payrolls are not uncommon. Conversely, users may choose to run payroll before the payroll deadline.",
        "readOnly": true
      },
      "Payroll-Processed-Date-Type": {
        "type": [
          "string",
          "null"
        ],
        "description": "The date at which the payroll was processed. Null if the payroll isn't processed yet.",
        "readOnly": true
      },
      "Payroll-Calculated-At-Type": {
        "type": [
          "string",
          "null"
        ],
        "format": "date-time",
        "description": "A timestamp of the last valid payroll calculation. Null if there isn't a valid calculation.",
        "readOnly": true
      },
      "Payroll-Payroll-Uuid-Type": {
        "type": "string",
        "description": "The UUID of the payroll.",
        "readOnly": true
      },
      "Payroll-Company-Uuid-Type": {
        "type": "string",
        "description": "The UUID of the company for the payroll.",
        "readOnly": true
      },
      "Payroll-Off-Cycle-Type": {
        "type": "boolean",
        "description": "Indicates whether the payroll is an off-cycle payroll",
        "readOnly": true
      },
      "Off-Cycle-Reason-Type": {
        "anyOf": [
          {
            "type": "string",
            "enum": [
              "Adhoc",
              "Benefit reversal",
              "Bonus",
              "Correction",
              "Dismissed employee",
              "Hired employee",
              "Wage correction",
              "Tax reconciliation",
              "Reversal",
              "Disability insurance distribution",
              "Transition from old pay schedule"
            ]
          },
          {
            "type": "null"
          }
        ],
        "description": "The off-cycle reason. Only included for off-cycle payrolls.",
        "readOnly": true
      },
      "Auto-Pilot-Type": {
        "type": "boolean",
        "description": "Indicates whether the payroll has automatic payroll enabled",
        "readOnly": true
      },
      "Payroll-External-Type": {
        "type": "boolean",
        "description": "Indicates whether the payroll is an external payroll",
        "readOnly": true
      },
      "Payroll-Final-Termination-Payroll-Type": {
        "type": "boolean",
        "description": "Indicates whether the payroll is the final payroll for a terminated employee. Only included for off-cycle payrolls.",
        "readOnly": true
      },
      "Payroll-Skip-Regular-Deductions-Type": {
        "type": [
          "boolean",
          "null"
        ],
        "description": "Block regular deductions and contributions for this payroll.  Only included for off-cycle payrolls.",
        "readOnly": true
      },
      "Payroll-Withholding-Pay-Period-Type": {
        "description": "The payment schedule tax rate the payroll is based on. Only included for off-cycle payrolls.",
        "readOnly": true,
        "anyOf": [
          {
            "type": "string",
            "enum": [
              "Every week",
              "Every other week",
              "Twice per month",
              "Monthly",
              "Quarterly",
              "Semiannually",
              "Annually"
            ]
          },
          {
            "type": "null"
          }
        ]
      },
      "Payroll-Fixed-Withholding-Rate-Type": {
        "type": [
          "boolean",
          "null"
        ],
        "description": "Enable taxes to be withheld at the IRS's required rate of 22% for federal income taxes. State income taxes will be taxed at the state's supplemental tax rate. Otherwise, we'll sum the entirety of the employee's wages and withhold taxes on the entire amount at the rate for regular wages. Only included for off-cycle payrolls.",
        "readOnly": true
      },
      "Payroll-Pay-Period-Type": {
        "type": "object",
        "readOnly": true,
        "properties": {
          "start_date": {
            "type": "string",
            "description": "The start date, inclusive, of the pay period.",
            "readOnly": true
          },
          "end_date": {
            "type": "string",
            "description": "The start date, inclusive, of the pay period.",
            "readOnly": true
          },
          "pay_schedule_uuid": {
            "type": [
              "string",
              "null"
            ],
            "description": "The UUID of the pay schedule for the payroll.",
            "readOnly": true
          }
        }
      },
      "Payroll-Payroll-Status-Meta-Type": {
        "type": "object",
        "description": "Information about the payroll's status and expected dates",
        "properties": {
          "cancellable": {
            "type": "boolean",
            "description": "true if the payroll may be cancelled.",
            "readOnly": true
          },
          "expected_check_date": {
            "type": "string",
            "description": "The date an employee will be paid if the payroll is submitted now.",
            "readOnly": true
          },
          "initial_check_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "The normal check date for the associated pay period. Returns `null` for off-cycle payrolls (not meaningful for off-cycle).",
            "readOnly": true
          },
          "expected_debit_time": {
            "type": "string",
            "description": "The time the employer's account will be debited if the payroll is submitted now.",
            "readOnly": true
          },
          "payroll_late": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "expected_check_date > initial_check_date. Returns `null` for off-cycle payrolls (not meaningful for off-cycle).",
            "readOnly": true
          },
          "initial_debit_cutoff_time": {
            "type": "string",
            "description": "Payroll must be submitted at or before this time to avoid late payroll.",
            "readOnly": true
          }
        }
      },
      "Payroll-Totals-Type": {
        "type": "object",
        "description": "The subtotals for the payroll.",
        "properties": {
          "company_debit": {
            "type": "string",
            "description": "The total company debit for the payroll.",
            "readOnly": true
          },
          "net_pay_debit": {
            "type": "string",
            "minLength": 1,
            "description": "The total company net pay for the payroll."
          },
          "tax_debit": {
            "type": "string",
            "description": "The total tax debit for the payroll.",
            "readOnly": true
          },
          "reimbursement_debit": {
            "type": "string",
            "description": "The total reimbursement debit for the payroll.",
            "readOnly": true
          },
          "child_support_debit": {
            "type": "string",
            "description": "The total child support debit for the payroll.",
            "readOnly": true
          },
          "reimbursements": {
            "type": "string",
            "description": "The total reimbursements for the payroll.",
            "readOnly": true
          },
          "net_pay": {
            "type": "string",
            "description": "The net pay amount for the payroll.",
            "readOnly": true
          },
          "gross_pay": {
            "type": "string",
            "description": "The gross pay amount for the payroll.",
            "readOnly": true
          },
          "employee_bonuses": {
            "type": "string",
            "description": "The total employee bonuses amount for the payroll.",
            "readOnly": true
          },
          "employee_commissions": {
            "type": "string",
            "description": "The total employee commissions amount for the payroll.",
            "readOnly": true
          },
          "employee_cash_tips": {
            "type": "string",
            "description": "The total employee cash tips amount for the payroll.",
            "readOnly": true
          },
          "employee_paycheck_tips": {
            "type": "string",
            "description": "The total employee paycheck tips amount for the payroll.",
            "readOnly": true
          },
          "additional_earnings": {
            "type": "string",
            "description": "The total additional earnings amount for the payroll.",
            "readOnly": true
          },
          "owners_draw": {
            "type": "string",
            "description": "The total owner's draw for the payroll.",
            "readOnly": true
          },
          "check_amount": {
            "type": "string",
            "description": "The total check amount for the payroll.",
            "readOnly": true
          },
          "employer_taxes": {
            "type": "string",
            "description": "The total amount of employer paid taxes for the payroll.",
            "readOnly": true
          },
          "employee_taxes": {
            "type": "string",
            "description": "The total amount of employee paid taxes for the payroll.",
            "readOnly": true
          },
          "benefits": {
            "type": "string",
            "description": "The total amount of company contributed benefits for the payroll.",
            "readOnly": true
          },
          "employee_benefits_deductions": {
            "type": "string",
            "description": "The total amount of employee deducted benefits for the payroll.",
            "readOnly": true
          },
          "imputed_pay": {
            "type": "string",
            "description": "The total amount of imputed pay for the payroll.",
            "readOnly": true
          },
          "deferred_payroll_taxes": {
            "type": "string",
            "description": "The total amount of payroll taxes deferred for the payroll, such as allowed by the CARES act.",
            "readOnly": true
          },
          "other_deductions": {
            "type": "string",
            "description": "The total amount of deductions for the payroll."
          }
        },
        "readOnly": true
      },
      "Payroll-Company-Taxes-Type": {
        "type": "array",
        "uniqueItems": false,
        "description": "An array of taxes applicable to this payroll in addition to taxes included in `employee_compensations`. Only included for processed or calculated payrolls when `taxes` is present in the `include` parameter.",
        "items": {
          "type": "object",
          "properties": {
            "name": {
              "type": "string",
              "description": "The tax name"
            },
            "employer": {
              "type": "boolean",
              "description": "Whether this tax is an employer or employee tax"
            },
            "amount": {
              "type": "string",
              "description": "The amount of this tax for the payroll"
            }
          }
        }
      },
      "Payroll-Taxes-Type": {
        "type": "array",
        "uniqueItems": false,
        "description": "An array of tax totals applicable to this payroll. Only included for processed or calculated payrolls when `payroll_taxes` is present in the `include` parameter.",
        "items": {
          "type": "object",
          "properties": {
            "name": {
              "type": "string",
              "description": "The tax name"
            },
            "employer": {
              "type": "boolean",
              "description": "Whether this tax is an employer or employee tax"
            },
            "amount": {
              "type": "number",
              "description": "The total tax for the payroll"
            }
          }
        }
      },
      "Payroll-Payment-Speed-Changed-Type": {
        "type": "object",
        "description": "Only applicable when a payroll is moved to four day processing instead of fast ach.",
        "properties": {
          "original_check_date": {
            "type": "string",
            "description": "Original check date when fast ach applies.",
            "readOnly": true
          },
          "current_check_date": {
            "type": "string",
            "description": "Current check date.",
            "readOnly": true
          },
          "original_debit_date": {
            "type": "string",
            "description": "Original debit date when fast ach applies.",
            "readOnly": true
          },
          "current_debit_date": {
            "type": "string",
            "description": "Current debit date.",
            "readOnly": true
          },
          "reason": {
            "type": "string",
            "description": "The reason why the payroll is moved to four day.",
            "readOnly": true
          }
        }
      },
      "Created-At-Type": {
        "type": "string",
        "format": "date-time",
        "description": "Datetime for when the resource was created.",
        "readOnly": true
      },
      "Payroll-Submission-Blocker-Type": {
        "type": "object",
        "description": "A blocker that prevents payment submission.",
        "properties": {
          "blocker_type": {
            "type": "string",
            "description": "The type of blocker that's blocking the payment submission.",
            "readOnly": true
          },
          "blocker_name": {
            "type": "string",
            "description": "The name of the submission blocker.",
            "readOnly": true
          },
          "unblock_options": {
            "type": "array",
            "uniqueItems": true,
            "items": {
              "type": "object",
              "properties": {
                "unblock_type": {
                  "type": "string",
                  "description": "The type of unblock option for the submission blocker.",
                  "readOnly": true
                },
                "check_date": {
                  "type": "string",
                  "description": "The payment check date associated with the unblock option.",
                  "readOnly": true
                },
                "metadata": {
                  "type": "object",
                  "additionalProperties": true,
                  "description": "Additional data associated with the unblock option.",
                  "readOnly": true
                }
              }
            },
            "description": "The available options to unblock a submission blocker.",
            "readOnly": true
          },
          "selected_option": {
            "type": [
              "string",
              "null"
            ],
            "description": "The unblock option that's been selected to resolve the submission blocker.",
            "readOnly": false
          },
          "status": {
            "type": "string",
            "description": "The status of the submission blocker.",
            "enum": [
              "unresolved",
              "resolved"
            ],
            "readOnly": true
          }
        }
      },
      "Payroll-Submission-Blockers-Type": {
        "type": "array",
        "description": "Only included for processed or calculated payrolls",
        "uniqueItems": true,
        "items": {
          "$ref": "#/components/schemas/Payroll-Submission-Blocker-Type"
        }
      },
      "Payroll-Credit-Blocker-Unblock-Option-Submit-Wire": {
        "type": "object",
        "description": "Unblock option to resolve a credit blocker by submitting a wire transfer",
        "required": [
          "unblock_type",
          "check_date",
          "metadata"
        ],
        "properties": {
          "unblock_type": {
            "type": "string",
            "enum": [
              "submit_wire"
            ],
            "description": "The type of unblock option for the credit blocker",
            "readOnly": true
          },
          "check_date": {
            "type": "string",
            "description": "The payment check date associated with the unblock option",
            "readOnly": true
          },
          "metadata": {
            "type": "object",
            "required": [
              "wire_in_amount",
              "wire_in_deadline",
              "wire_in_request_uuid"
            ],
            "properties": {
              "wire_in_amount": {
                "type": "string",
                "description": "The amount to be wired in (decimal string)",
                "readOnly": true
              },
              "wire_in_deadline": {
                "type": "string",
                "format": "date-time",
                "description": "Deadline for the wire transfer to be received",
                "readOnly": true
              },
              "wire_in_request_uuid": {
                "type": "string",
                "description": "UUID of the wire in request",
                "readOnly": true
              }
            },
            "readOnly": true
          }
        }
      },
      "Payroll-Credit-Blocker-Unblock-Option-Submit-Bank-Screenshot": {
        "type": "object",
        "description": "Unblock option to resolve a credit blocker by submitting a bank screenshot",
        "required": [
          "unblock_type",
          "check_date",
          "metadata"
        ],
        "properties": {
          "unblock_type": {
            "type": "string",
            "enum": [
              "submit_bank_screenshot"
            ],
            "description": "The type of unblock option for the credit blocker",
            "readOnly": true
          },
          "check_date": {
            "type": "string",
            "description": "The payment check date associated with the unblock option",
            "readOnly": true
          },
          "metadata": {
            "type": "object",
            "required": [
              "information_request_uuid"
            ],
            "properties": {
              "information_request_uuid": {
                "type": "string",
                "description": "UUID of the information request",
                "readOnly": true
              },
              "bank_account_last_four_digits": {
                "type": [
                  "string",
                  "null"
                ],
                "description": "Last 4 digits of the bank account number for the bank screenshot RFI",
                "readOnly": true
              }
            },
            "readOnly": true
          }
        }
      },
      "Payroll-Credit-Blocker-Unblock-Option-Respond-To-High-Risk-Fraud-Rfi": {
        "type": "object",
        "description": "Unblock option to resolve a credit blocker by responding to high risk fraud RFI",
        "required": [
          "unblock_type",
          "check_date",
          "metadata"
        ],
        "properties": {
          "unblock_type": {
            "type": "string",
            "enum": [
              "respond_to_high_risk_fraud_rfi"
            ],
            "description": "The type of unblock option for the credit blocker",
            "readOnly": true
          },
          "check_date": {
            "type": "string",
            "description": "The payment check date associated with the unblock option",
            "readOnly": true
          },
          "metadata": {
            "type": "object",
            "required": [
              "information_request_uuid"
            ],
            "properties": {
              "information_request_uuid": {
                "type": "string",
                "description": "UUID of the information request",
                "readOnly": true
              }
            },
            "readOnly": true
          }
        }
      },
      "Payroll-Credit-Blocker-Unblock-Option-Wait-For-Reverse-Wire": {
        "type": "object",
        "description": "Unblock option to resolve a credit blocker by waiting for reverse wire",
        "required": [
          "unblock_type",
          "check_date",
          "metadata"
        ],
        "properties": {
          "unblock_type": {
            "type": "string",
            "enum": [
              "wait_for_reverse_wire"
            ],
            "description": "The type of unblock option for the credit blocker",
            "readOnly": true
          },
          "check_date": {
            "type": "string",
            "description": "The payment check date associated with the unblock option",
            "readOnly": true
          },
          "metadata": {
            "type": "object",
            "additionalProperties": false,
            "readOnly": true
          }
        }
      },
      "Payroll-Credit-Blocker-Type": {
        "type": "object",
        "description": "A blocker that prevents payment crediting.",
        "properties": {
          "blocker_type": {
            "type": "string",
            "description": "The type of blocker that's blocking the payment from being credited.",
            "readOnly": true
          },
          "blocker_name": {
            "type": "string",
            "description": "The name of the credit blocker.",
            "readOnly": true
          },
          "unblock_options": {
            "type": "array",
            "uniqueItems": true,
            "items": {
              "oneOf": [
                {
                  "$ref": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Submit-Wire"
                },
                {
                  "$ref": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Submit-Bank-Screenshot"
                },
                {
                  "$ref": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Respond-To-High-Risk-Fraud-Rfi"
                },
                {
                  "$ref": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Wait-For-Reverse-Wire"
                }
              ],
              "discriminator": {
                "propertyName": "unblock_type",
                "mapping": {
                  "submit_wire": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Submit-Wire",
                  "submit_bank_screenshot": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Submit-Bank-Screenshot",
                  "respond_to_high_risk_fraud_rfi": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Respond-To-High-Risk-Fraud-Rfi",
                  "wait_for_reverse_wire": "#/components/schemas/Payroll-Credit-Blocker-Unblock-Option-Wait-For-Reverse-Wire"
                }
              }
            },
            "description": "The available options to unblock a credit blocker.",
            "readOnly": true
          },
          "selected_option": {
            "type": [
              "string",
              "null"
            ],
            "description": "The unblock option that's been selected to resolve the credit blocker.",
            "readOnly": false
          },
          "status": {
            "type": "string",
            "description": "The status of the credit blocker",
            "enum": [
              "unresolved",
              "pending_review",
              "resolved",
              "failed"
            ]
          }
        }
      },
      "Payroll-Credit-Blockers-Type": {
        "type": "array",
        "description": "Only included for processed payrolls",
        "uniqueItems": true,
        "items": {
          "$ref": "#/components/schemas/Payroll-Credit-Blocker-Type"
        }
      },
      "Payroll-Processing-Request": {
        "type": [
          "object",
          "null"
        ],
        "properties": {
          "status": {
            "type": "string",
            "description": "The status of the payroll processing request",
            "readOnly": true,
            "enum": [
              "calculating",
              "calculate_success",
              "submitting",
              "submit_success",
              "processing_failed"
            ]
          },
          "errors": {
            "description": "Errors that occurred during async payroll processing",
            "readOnly": true,
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Entity-Error-Object"
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
    "/v1/companies/{company_id}/payrolls": {
      "get": {
        "summary": "Get all payrolls for a company",
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
            "name": "processing_statuses",
            "in": "query",
            "required": false,
            "explode": false,
            "description": "Whether to include processed and/or unprocessed payrolls in the response, defaults to processed, for multiple attributes comma separate the values, i.e. `?processing_statuses=processed,unprocessed`",
            "schema": {
              "type": "array",
              "items": {
                "type": "string",
                "enum": [
                  "processed",
                  "unprocessed"
                ]
              }
            }
          },
          {
            "name": "payroll_types",
            "in": "query",
            "required": false,
            "explode": false,
            "description": "Whether to include regular and/or off_cycle payrolls in the response, defaults to regular, for multiple attributes comma separate the values, i.e. `?payroll_types=regular,off_cycle`",
            "schema": {
              "type": "array",
              "items": {
                "type": "string",
                "enum": [
                  "regular",
                  "off_cycle",
                  "external"
                ]
              }
            }
          },
          {
            "name": "processed",
            "in": "query",
            "required": false,
            "description": "Whether to return processed or unprocessed payrolls",
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "include_off_cycle",
            "in": "query",
            "required": false,
            "description": "Whether to include off cycle payrolls in the response",
            "schema": {
              "type": "boolean"
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
                  "taxes",
                  "payroll_status_meta",
                  "totals",
                  "risk_blockers",
                  "reversals"
                ]
              }
            },
            "description": "Include the requested attribute in the response, for multiple attributes comma separate the values, i.e. `?include=benefits,deductions,taxes`"
          },
          {
            "name": "start_date",
            "in": "query",
            "required": false,
            "example": "2020-01-31",
            "description": "Return payrolls whose pay period is after the start date",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "end_date",
            "in": "query",
            "required": false,
            "example": "2020-01-31",
            "description": "Return payrolls whose pay period is before the end date. If left empty, defaults to today's date.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "date_filter_by",
            "in": "query",
            "required": false,
            "description": "Specifies which date field to use when filtering payrolls with start_date and end_date. This field applies only to regular processed payrolls and defaults to pay period if not provided.",
            "schema": {
              "type": "string",
              "enum": [
                "check_date"
              ]
            },
            "example": "check_date"
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
          },
          {
            "name": "sort_order",
            "in": "query",
            "required": false,
            "description": "A string indicating whether to sort resulting events in ascending (asc) or descending (desc) chronological order. Events are sorted by their `timestamp`. Defaults to asc if left empty.",
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            },
            "example": "asc"
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-payrolls",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a list of payrolls for a company. You can change the payrolls returned by updating the processing_status, payroll_types, start_date, & end_date params.\n\nBy default, will return processed, regular payrolls for the past 6 months.\n\nNotes:\n* Dollar amounts are returned as string representations of numeric decimals, are represented to the cent.\n* end_date can be at most 3 months in the future and start_date and end_date can't be more than 1 year apart.\n* Results are paginated. Maximum page size is 100 payrolls per request; the default page size is 25.\n\nscope: `payrolls:read`",
        "tags": [
          "Payrolls"
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
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-List/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payroll-List"
                }
              }
            }
          },
          "404": {
            "description": "Not Found",
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
