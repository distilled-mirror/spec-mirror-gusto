---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a single payroll

Returns a payroll. If payroll is calculated or processed, will return employee_compensations and totals.

Results are paginated, with a maximum page size of 100 employee_compensations.

Notes:
* Hour and dollar amounts are returned as string representations of numeric decimals.
* Hours are represented to the thousands place; dollar amounts are represented to the cent.
* Every eligible compensation is returned for each employee. If no data has yet be inserted for a given field, it defaults to "0.00" (for fixed amounts) or "0.000" (for hours ).
* When include parameter with benefits value is passed, employee_benefits:read scope is required to return benefits
  * Benefits containing PHI are only visible with the `employee_benefits:read:phi` scope

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
      "Payroll-Employee-Compensations-Included": {
        "type": "object",
        "additionalProperties": true,
        "properties": {
          "taxes": {
            "type": "array",
            "uniqueItems": false,
            "description": "An array of employer and employee taxes for the pay period. Only included for processed or calculated payrolls when `taxes` is present in the `include` parameter.",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "minLength": 1
                },
                "employer": {
                  "type": "boolean"
                },
                "amount": {
                  "type": "string",
                  "format": "float"
                }
              },
              "required": [
                "name",
                "employer",
                "amount"
              ],
              "readOnly": true
            },
            "readOnly": true
          },
          "benefits": {
            "type": "array",
            "uniqueItems": false,
            "description": "An array of employee benefits for the pay period. Benefits are only included for processed payroll when the include parameter is present.",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "readOnly": true
                },
                "employee_deduction": {
                  "type": "string",
                  "format": "float",
                  "readOnly": true
                },
                "company_contribution": {
                  "type": "string",
                  "format": "float",
                  "readOnly": true
                },
                "imputed": {
                  "type": "boolean"
                }
              },
              "readOnly": true
            },
            "readOnly": true
          },
          "deductions": {
            "type": "array",
            "uniqueItems": false,
            "description": "An array of employee deductions for the pay period. Only included when `deductions` is present in the `include` parameter.",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "description": "The name of the deduction."
                },
                "amount": {
                  "type": "string",
                  "format": "float",
                  "description": "The amount of the deduction for the pay period."
                },
                "amount_type": {
                  "type": "string",
                  "description": "The amount type of the deduction for the pay period. Only present for unprocessed payrolls.",
                  "enum": [
                    "fixed",
                    "percent"
                  ]
                },
                "uuid": {
                  "type": "string",
                  "description": "The UUID of the deduction. Only present for unprocessed payrolls.",
                  "readOnly": true
                },
                "updatable_via_payroll": {
                  "type": "boolean",
                  "description": "Whether the deduction can be updated via the payroll update endpoint. Only present for unprocessed payrolls.",
                  "readOnly": true
                }
              }
            }
          }
        }
      },
      "Payroll-Employee-Compensations-Base-Type": {
        "type": "object",
        "properties": {
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee.",
            "readOnly": true
          },
          "excluded": {
            "type": "boolean",
            "description": "This employee will be excluded (skipped) from payroll calculation and will not be paid for the payroll. Cancelling a payroll would reset all employees' excluded back to false.",
            "readOnly": true
          },
          "first_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The first name of the employee. Requires `employees:read` scope.",
            "readOnly": true
          },
          "preferred_first_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The preferred first name of the employee. Requires `employees:read` scope.",
            "readOnly": true
          },
          "last_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The last name of the employee. Requires `employees:read` scope.",
            "readOnly": true
          },
          "gross_pay": {
            "type": [
              "string",
              "null"
            ],
            "description": "The employee's gross pay (as a string-formatted decimal, e.g. \"1234.56\"), equal to regular wages + cash tips + payroll tips + any other additional earnings, excluding imputed income. This value is only available for processed payrolls.",
            "readOnly": true
          },
          "net_pay": {
            "type": [
              "string",
              "null"
            ],
            "description": "The employee's net pay (as a string-formatted decimal, e.g. \"1234.56\"), equal to gross_pay - employee taxes - employee deductions or garnishments - cash tips. This value is only available for processed payrolls.",
            "readOnly": true
          },
          "check_amount": {
            "type": [
              "string",
              "null"
            ],
            "description": "The employee's check amount (as a string-formatted decimal, e.g. \"1234.56\"), equal to net_pay + reimbursements. This value is only available for processed payrolls.",
            "readOnly": true
          },
          "payment_method": {
            "description": "The employee's compensation payment method. Is *only* `Historical` when retrieving external payrolls initially run outside of Gusto, then put into Gusto.",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "Direct Deposit",
                  "Check",
                  "Historical"
                ]
              },
              {
                "type": "null"
              }
            ]
          },
          "memo": {
            "type": [
              "string",
              "null"
            ],
            "description": "Custom text that will be printed as a personal note to the employee on a paystub.",
            "readOnly": true
          },
          "fixed_compensations": {
            "type": "array",
            "uniqueItems": false,
            "description": "An array of fixed compensations for the employee. Fixed compensations include tips and bonuses. On regular payrolls, reimbursements are sent via the dedicated `reimbursements` array instead. Off-cycle payrolls continue to include reimbursements in `fixed_compensations`. If this payroll has been processed, only fixed compensations with a value greater than 0.00 are returned. For an unprocessed payroll, all active fixed compensations are returned.",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "description": "The name of the compensation. This also serves as the unique, immutable identifier for this compensation."
                },
                "amount": {
                  "type": "string",
                  "description": "The amount of the compensation for the pay period."
                },
                "job_uuid": {
                  "type": "string",
                  "description": "The UUID of the job for the compensation.",
                  "readOnly": true
                }
              }
            }
          },
          "hourly_compensations": {
            "type": "array",
            "uniqueItems": false,
            "description": "An array of hourly compensations for the employee. Hourly compensations include regular, overtime, and double overtime hours. If this payroll has been processed, only hourly compensations with a value greater than 0.00 are returned. For an unprocessed payroll, all active hourly compensations are returned.",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "description": "The name of the compensation. This also serves as the unique, immutable identifier for this compensation."
                },
                "hours": {
                  "type": "string",
                  "description": "The number of hours to be compensated for this pay period."
                },
                "amount": {
                  "type": "string",
                  "description": "The amount of the compensation. This field is only available after the payroll is calculated and cannot be used for updating hourly compensations."
                },
                "job_uuid": {
                  "type": "string",
                  "description": "The UUID of the job for the compensation.",
                  "readOnly": true
                },
                "compensation_multiplier": {
                  "type": "number",
                  "description": "The amount multiplied by the base rate to calculate total compensation per hour worked.",
                  "readOnly": true
                },
                "flsa_status": {
                  "type": "string",
                  "description": "The FLSA Status of the employee's primary job compensation",
                  "readOnly": true
                }
              }
            }
          },
          "paid_time_off": {
            "type": "array",
            "uniqueItems": false,
            "description": "An array of all paid time off the employee is eligible for this pay period.",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "description": "The name of the PTO. This also serves as the unique, immutable identifier for the PTO."
                },
                "hours": {
                  "type": "string",
                  "description": "The hours of this PTO taken during the pay period."
                },
                "amount": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The dollar amount paid for this PTO entry during the pay period (as a string-formatted decimal, e.g. \"1234.56\"). Only available for processed payrolls.",
                  "readOnly": true
                },
                "final_payout_unused_hours_input": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The outstanding hours paid upon termination. This field is only applicable for termination payrolls."
                }
              }
            }
          },
          "reimbursements": {
            "type": "array",
            "uniqueItems": false,
            "description": "An array of reimbursements for the employee.",
            "items": {
              "type": "object",
              "properties": {
                "amount": {
                  "type": "string",
                  "description": "The dollar amount of the reimbursement for the pay period."
                },
                "description": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The description of the reimbursement. Null for unnamed reimbursements."
                },
                "uuid": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "The UUID of the reimbursement. Null for unnamed reimbursements. This field is only available for unprocessed payrolls.",
                  "readOnly": true
                },
                "recurring": {
                  "type": "boolean",
                  "description": "Whether the reimbursement is recurring. This field is only available for unprocessed payrolls.",
                  "readOnly": true
                }
              },
              "required": [
                "amount",
                "description"
              ]
            }
          },
          "custom_withholdings": {
            "type": "object",
            "description": "The one-time custom withholding overrides applied to this payroll for this employee.\n`federal` is null when no federal one-time override is set; `state` is an empty\narray when no state one-time overrides are set.\n",
            "properties": {
              "federal": {
                "type": [
                  "object",
                  "null"
                ],
                "description": "Federal one-time custom withholding override applied to this payroll.",
                "properties": {
                  "override_type": {
                    "type": "string",
                    "enum": [
                      "one_time"
                    ],
                    "description": "Override mode. Only `one_time` is currently exposed."
                  },
                  "amount": {
                    "type": "string",
                    "description": "The amount that was withheld for this payroll."
                  },
                  "amount_type": {
                    "type": "string",
                    "enum": [
                      "fixed",
                      "percent"
                    ],
                    "description": "How to interpret the amount."
                  }
                }
              },
              "state": {
                "type": "array",
                "description": "State one-time custom withholding overrides applied to this payroll, one entry per state field.",
                "items": {
                  "type": "object",
                  "properties": {
                    "employee_state_field_uuid": {
                      "type": "string",
                      "description": "The UUID of the EmployeeStateField this withholding applies to."
                    },
                    "override_type": {
                      "type": "string",
                      "enum": [
                        "one_time"
                      ],
                      "description": "Override mode. Only `one_time` is currently exposed."
                    },
                    "amount": {
                      "type": "string",
                      "description": "The amount that was withheld for this payroll."
                    },
                    "amount_type": {
                      "type": "string",
                      "enum": [
                        "fixed",
                        "percent"
                      ],
                      "description": "How to interpret the amount."
                    }
                  }
                }
              }
            }
          }
        }
      },
      "Payroll-Employee-Compensations-Type": {
        "allOf": [
          {
            "$ref": "#/components/schemas/Payroll-Employee-Compensations-Base-Type"
          },
          {
            "$ref": "#/components/schemas/Versionable"
          },
          {
            "type": "object",
            "properties": {
              "version": {
                "description": "The current version of this employee compensation. This field is only available for prepared payrolls. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
              },
              "deductions": {
                "type": "array",
                "uniqueItems": false,
                "description": "An array of deductions for the employee. This field is included by default for regular payrolls in version `v2025-06-15` and later.",
                "items": {
                  "type": "object",
                  "properties": {
                    "name": {
                      "type": "string",
                      "description": "The name of the deduction."
                    },
                    "amount": {
                      "type": "number",
                      "description": "The amount of the deduction for the pay period."
                    },
                    "amount_type": {
                      "type": "string",
                      "description": "The amount type of the deduction for the pay period. Only present for unprocessed payrolls.",
                      "enum": [
                        "fixed",
                        "percent"
                      ]
                    },
                    "uuid": {
                      "type": "string",
                      "description": "The UUID of the deduction. Only present for unprocessed payrolls."
                    },
                    "updatable_via_payroll": {
                      "type": "boolean",
                      "description": "Whether the deduction can be updated via the payroll update endpoint. Only present for unprocessed payrolls.",
                      "readOnly": true
                    }
                  }
                }
              }
            }
          }
        ]
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
      },
      "Payroll-Show": {
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
            "processing_request": {
              "status": "submit_success",
              "errors": []
            },
            "created_at": "2025-06-16T16:58:03Z",
            "partner_owned_disbursement": null
          },
          "with_submit_wire_credit_blocker": {
            "uuid": "b441a30b-2adb-489e-b7b7-9d094011a3f8",
            "employee_compensations": [],
            "submission_blockers": [],
            "credit_blockers": [
              {
                "blocker_type": "waiting_for_wire_in",
                "blocker_name": "Waiting for Wire In",
                "unblock_options": [
                  {
                    "unblock_type": "submit_wire",
                    "check_date": "2025-06-13",
                    "metadata": {
                      "wire_in_amount": "15000.00",
                      "wire_in_deadline": "2025-06-12T18:00:00Z",
                      "wire_in_request_uuid": "c1234567-89ab-cdef-0123-456789abcdef"
                    }
                  }
                ],
                "selected_option": null,
                "status": "unresolved"
              }
            ],
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
            "processing_request": {
              "status": "submit_success",
              "errors": []
            },
            "created_at": "2025-06-16T16:58:03Z",
            "partner_owned_disbursement": null
          },
          "with_submit_bank_screenshot_credit_blocker": {
            "uuid": "b441a30b-2adb-489e-b7b7-9d094011a3f8",
            "employee_compensations": [],
            "submission_blockers": [],
            "credit_blockers": [
              {
                "blocker_type": "waiting_for_bank_screenshot",
                "blocker_name": "Waiting for Bank Screenshot",
                "unblock_options": [
                  {
                    "unblock_type": "submit_bank_screenshot",
                    "check_date": "2025-06-13",
                    "metadata": {
                      "information_request_uuid": "d2234567-89ab-cdef-0123-456789abcdef"
                    }
                  }
                ],
                "selected_option": null,
                "status": "unresolved"
              }
            ],
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
            "processing_request": {
              "status": "submit_success",
              "errors": []
            },
            "created_at": "2025-06-16T16:58:03Z",
            "partner_owned_disbursement": null
          },
          "with_respond_to_high_risk_fraud_rfi_credit_blocker": {
            "uuid": "b441a30b-2adb-489e-b7b7-9d094011a3f8",
            "employee_compensations": [],
            "submission_blockers": [],
            "credit_blockers": [
              {
                "blocker_type": "waiting_for_high_risk_fraud_rfi",
                "blocker_name": "Waiting for High Risk Fraud RFI",
                "unblock_options": [
                  {
                    "unblock_type": "respond_to_high_risk_fraud_rfi",
                    "check_date": "2025-06-13",
                    "metadata": {
                      "information_request_uuid": "e3234567-89ab-cdef-0123-456789abcdef"
                    }
                  }
                ],
                "selected_option": null,
                "status": "pending_review"
              }
            ],
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
            "processing_request": {
              "status": "submit_success",
              "errors": []
            },
            "created_at": "2025-06-16T16:58:03Z",
            "partner_owned_disbursement": null
          },
          "with_wait_for_reverse_wire_credit_blocker": {
            "uuid": "b441a30b-2adb-489e-b7b7-9d094011a3f8",
            "employee_compensations": [],
            "submission_blockers": [],
            "credit_blockers": [
              {
                "blocker_type": "waiting_for_reverse_wire",
                "blocker_name": "Waiting for Reverse Wire",
                "unblock_options": [
                  {
                    "unblock_type": "wait_for_reverse_wire",
                    "check_date": "2025-06-13",
                    "metadata": {}
                  }
                ],
                "selected_option": null,
                "status": "resolved"
              }
            ],
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
          },
          "employee_compensations": {
            "type": "array",
            "uniqueItems": false,
            "items": {
              "type": "object",
              "allOf": [
                {
                  "$ref": "#/components/schemas/Payroll-Employee-Compensations-Type"
                },
                {
                  "$ref": "#/components/schemas/Payroll-Employee-Compensations-Included"
                }
              ]
            }
          }
        }
      },
      "Versionable": {
        "type": "object",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
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
    "/v1/companies/{company_id}/payrolls/{payroll_id}": {
      "get": {
        "summary": "Get a single payroll",
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
            "name": "payroll_id",
            "in": "path",
            "description": "The UUID of the payroll",
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
                  "benefits",
                  "deductions",
                  "taxes",
                  "payroll_status_meta",
                  "totals",
                  "risk_blockers",
                  "reversals",
                  "payroll_taxes"
                ]
              }
            },
            "description": "Include the requested attribute in the response, for multiple attributes comma separate the values, i.e. `?include=benefits,deductions,taxes`"
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
            "name": "sort_by",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "pattern": "^(first_name|last_name)(:(asc|desc))?(,(first_name|last_name)(:(asc|desc))?)*$",
              "example": "first_name:asc"
            },
            "description": "Sort employee compensations by one or more fields. Options: first_name, last_name. Append `:asc` or `:desc` to specify direction (e.g., `last_name:asc` or `last_name:asc,first_name:asc`). Defaults to ascending."
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_id-payrolls-payroll_id",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a payroll. If payroll is calculated or processed, will return employee_compensations and totals.\n\nResults are paginated, with a maximum page size of 100 employee_compensations.\n\nNotes:\n* Hour and dollar amounts are returned as string representations of numeric decimals.\n* Hours are represented to the thousands place; dollar amounts are represented to the cent.\n* Every eligible compensation is returned for each employee. If no data has yet be inserted for a given field, it defaults to \"0.00\" (for fixed amounts) or \"0.000\" (for hours ).\n* When include parameter with benefits value is passed, employee_benefits:read scope is required to return benefits\n  * Benefits containing PHI are only visible with the `employee_benefits:read:phi` scope\n\nscope: `payrolls:read`",
        "tags": [
          "Payrolls"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful with wait_for_reverse_wire credit blocker",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Show/x-examples/success_status"
                    }
                  },
                  "with_submit_wire_credit_blocker": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Show/x-examples/with_submit_wire_credit_blocker"
                    }
                  },
                  "with_submit_bank_screenshot_credit_blocker": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Show/x-examples/with_submit_bank_screenshot_credit_blocker"
                    }
                  },
                  "with_respond_to_high_risk_fraud_rfi_credit_blocker": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Show/x-examples/with_respond_to_high_risk_fraud_rfi_credit_blocker"
                    }
                  },
                  "with_wait_for_reverse_wire_credit_blocker": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Show/x-examples/with_wait_for_reverse_wire_credit_blocker"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payroll-Show"
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
