---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get contractor payment groups for a company

Returns a list of minimal contractor payment groups within a given time period, including totals but not associated contractor payments.

scope: `payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractor Payment Groups"
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
      "Contractor-Payment-Group-Base": {
        "description": "Base properties for contractor payment groups.",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The unique identifier of the contractor payment group.",
            "readOnly": true
          },
          "company_uuid": {
            "type": "string",
            "description": "The UUID of the company.",
            "readOnly": true
          },
          "check_date": {
            "type": "string",
            "description": "The check date of the contractor payment group.",
            "readOnly": true
          },
          "debit_date": {
            "type": "string",
            "description": "The debit date of the contractor payment group.",
            "readOnly": true
          },
          "status": {
            "type": "string",
            "description": "The status of the contractor payment group.  Will be `Funded` if all payments that should be funded (i.e. have `Direct Deposit` for payment method) are funded.  A group can have status `Funded` while having associated payments that have status `Unfunded`, i.e. payment with `Check` payment method.",
            "enum": [
              "Unfunded",
              "Funded"
            ],
            "readOnly": true
          },
          "creation_token": {
            "type": [
              "string",
              "null"
            ],
            "description": "Token used to make contractor payment group creation idempotent.  Will error if attempting to create a group with a duplicate token.",
            "readOnly": true
          }
        }
      },
      "Contractor-Payment-Group-With-Blockers": {
        "description": "Contractor payment group with submission and credit blockers, but without individual contractor payments.",
        "type": "object",
        "allOf": [
          {
            "$ref": "#/components/schemas/Contractor-Payment-Group-Base"
          },
          {
            "type": "object",
            "properties": {
              "partner_owned_disbursement": {
                "type": [
                  "boolean",
                  "null"
                ],
                "description": "Whether the disbursement is partner owned.",
                "readOnly": true
              },
              "submission_blockers": {
                "type": "array",
                "description": "List of submission blockers for the contractor payment group.",
                "readOnly": true,
                "items": {
                  "$ref": "#/components/schemas/Payroll-Submission-Blocker-Type"
                }
              },
              "credit_blockers": {
                "type": "array",
                "description": "List of credit blockers for the contractor payment group.",
                "readOnly": true,
                "items": {
                  "$ref": "#/components/schemas/Payroll-Credit-Blocker-Type"
                }
              },
              "totals": {
                "type": "object",
                "properties": {
                  "amount": {
                    "type": "string",
                    "description": "The total amount for the group of contractor payments.",
                    "readOnly": true
                  },
                  "debit_amount": {
                    "type": "string",
                    "description": "The total debit amount for the group of contractor payments. Sum of wage & reimbursement amount.",
                    "readOnly": true
                  },
                  "wage_amount": {
                    "type": "string",
                    "description": "The total wage amount for the group of contractor payments.",
                    "readOnly": true
                  },
                  "reimbursement_amount": {
                    "type": "string",
                    "description": "The total reimbursement amount for the group of contractor payments.",
                    "readOnly": true
                  },
                  "check_amount": {
                    "type": "string",
                    "description": "The total check amount for the group of contractor payments.",
                    "readOnly": true
                  }
                },
                "readOnly": true
              }
            }
          }
        ],
        "x-examples": {
          "success": {
            "uuid": "94d9698e-9c95-45d6-b66e-d208258666ab",
            "company_uuid": "5f5aaa38-f517-4f56-85e4-afdb83321663",
            "check_date": "2025-09-22",
            "debit_date": "2025-09-18",
            "status": "Unfunded",
            "creation_token": "94d9698e-9c95-45d6-b66e-d208258666ab",
            "partner_owned_disbursement": false,
            "submission_blockers": [
              {
                "blocker_type": "fast_ach_threshold_exceeded",
                "blocker_name": "Fast ACH Threshold Exceeded",
                "selected_option": "wire_in",
                "status": "resolved",
                "unblock_options": [
                  {
                    "unblock_type": "wire_in",
                    "check_date": "2025-09-22",
                    "metadata": {
                      "wire_in_deadline": "2025-09-22T18:00:00Z",
                      "wire_in_amount": "760000.0"
                    }
                  },
                  {
                    "unblock_type": "move_to_four_day",
                    "check_date": "2025-09-22",
                    "metadata": {
                      "debit_date": "2025-09-16"
                    }
                  }
                ]
              }
            ],
            "credit_blockers": [
              {
                "blocker_type": "waiting_for_wire_in",
                "blocker_name": "Waiting for Wire In",
                "selected_option": "submit_wire",
                "status": "unresolved",
                "unblock_options": [
                  {
                    "unblock_type": "submit_wire",
                    "check_date": "2025-09-22",
                    "metadata": {
                      "wire_in_deadline": "2025-09-22T18:00:00Z",
                      "wire_in_amount": "760000.0",
                      "wire_in_request_uuid": "96ea4784-979a-45aa-9ccb-83be86b6dcea"
                    }
                  }
                ]
              }
            ],
            "totals": {
              "amount": "760000.00",
              "debit_amount": "760000.00",
              "wage_amount": "10000.00",
              "reimbursement_amount": "750000.00",
              "check_amount": "0.00"
            }
          }
        },
        "x-tags": [
          "Contractor Payment Groups"
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
    "/v1/companies/{company_id}/contractor_payment_groups": {
      "get": {
        "summary": "Get contractor payment groups for a company",
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
            "required": true,
            "description": "The UUID of the company",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "start_date",
            "in": "query",
            "required": false,
            "description": "The time period for which to retrieve contractor payment groups. Defaults to 6 months ago.",
            "example": "2020-01-01",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "end_date",
            "in": "query",
            "required": false,
            "description": "The time period for which to retrieve contractor payment groups. Defaults to today's date.",
            "example": "2020-12-31",
            "schema": {
              "type": "string"
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
        "operationId": "get-v1-companies-company_id-contractor_payment_groups",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a list of minimal contractor payment groups within a given time period, including totals but not associated contractor payments.\n\nscope: `payrolls:read`",
        "tags": [
          "Contractor Payment Groups"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "List of Contractor Payment Groups",
            "content": {
              "application/json": {
                "examples": {
                  "success": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Contractor-Payment-Group-With-Blockers/x-examples/success"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Contractor-Payment-Group-With-Blockers"
                  }
                }
              }
            }
          },
          "404": {
            "description": "Not Found\n\nThe requested company does not exist. Make sure the provided UUID is valid.\n",
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
