---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get tax requirements for a state

Retrieves the detailed tax requirements for a specific state. The response includes requirement sets grouped by
category (e.g., registrations, tax rates, deposit schedules), each containing individual requirements with their
current values, labels, and metadata describing the expected input format.

Use this to build dynamic UIs for tax setup or to read the current tax configuration for a state.

scope: `company_tax_requirements:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Tax Requirements"
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
      "Tax-Requirement": {
        "type": "object",
        "x-examples": {
          "ga-withholding-requirement-example": {
            "key": "71653ec0-00b5-4c66-a58b-22ecf21704c5",
            "applicable_if": [],
            "label": "Withholding Number",
            "description": "If you have run payroll in the past in GA, find your withholding number on notices received from the Georgia Department of Revenue, or call the agency at (877) 423-6711. If you don’t have a number yet, you should <a target='_blank' data-bypass href='https://gtc.dor.ga.gov/_/#1'>register the business online</a>. The last two characters of your ID must be upper case letters.",
            "value": "1233214-AB",
            "editable": true,
            "metadata": {
              "type": "account_number",
              "mask": "#######-^^",
              "prefix": null
            }
          }
        },
        "properties": {
          "key": {
            "$ref": "#/components/schemas/Tax-Requirement-Key"
          },
          "applicable_if": {
            "type": "array",
            "description": "An array of references to other requirements within the requirement set. This requirement is only applicable if all referenced requirements have values matching the corresponding `value`. The primary use-case is dynamically hiding and showing requirements as values change. E.g. Show Requirement-B when Requirement-A has been answered with `false`. To be explicit, an empty array means the requirement is applicable.",
            "items": {
              "type": "object",
              "properties": {
                "key": {
                  "$ref": "#/components/schemas/Tax-Requirement-Key"
                },
                "value": {
                  "description": "The required value of the requirement identified by `key`",
                  "oneOf": [
                    {
                      "type": "boolean"
                    },
                    {
                      "type": "string"
                    },
                    {
                      "type": "number"
                    },
                    {
                      "type": "null"
                    }
                  ]
                }
              }
            }
          },
          "label": {
            "type": "string",
            "description": "A customer facing description of the requirement"
          },
          "description": {
            "type": [
              "string",
              "null"
            ],
            "description": "A more detailed customer facing description of the requirement"
          },
          "value": {
            "$ref": "#/components/schemas/Tax-Requirements-Value"
          },
          "metadata": {
            "$ref": "#/components/schemas/Tax-Requirement-Metadata"
          },
          "editable": {
            "type": "boolean",
            "description": "Whether the value of this requirement can be updated"
          },
          "payroll_blocking": {
            "type": "boolean",
            "description": "Whether this requirement, when blank, would block payroll processing for the company in this state.\nStable across changes to the field's value: a `payroll_blocking: true` field reports `true` whether\ncurrently empty or populated.\n"
          },
          "default_value_applied": {
            "type": "boolean",
            "description": "Whether the current `value` is a default rather than an explicitly set one.\n"
          }
        }
      },
      "Tax-Requirement-Metadata": {
        "type": "object",
        "x-examples": {
          "select-example": {
            "type": "select",
            "options": [
              {
                "label": "Semiweekly",
                "value": "Semi-weekly"
              },
              {
                "label": "Monthly",
                "value": "Monthly"
              },
              {
                "label": "Quarterly",
                "value": "Quarterly"
              }
            ]
          },
          "tax_rate-example": {
            "metadata": {
              "type": "tax_rate",
              "validation": {
                "type": "min_max",
                "min": "0.0004",
                "max": "0.081"
              }
            }
          },
          "radio-example": {
            "metadata": {
              "type": "radio",
              "options": [
                {
                  "label": "No, we cannot reimburse the state—we have to pay SUI taxes quarterly",
                  "short_label": "Not Reimbursable",
                  "value": false
                },
                {
                  "label": "Yes, we can reimburse the state if an employee collects SUI benefits—we don’t have to pay SUI taxes quarterly",
                  "short_label": "Reimbursable",
                  "value": true
                }
              ]
            }
          },
          "account_number-example": {
            "metadata": {
              "type": "account_number",
              "mask": "######-##",
              "prefix": null
            }
          }
        },
        "properties": {
          "type": {
            "type": "string",
            "enum": [
              "text",
              "currency",
              "radio",
              "select",
              "percent",
              "account_number",
              "tax_rate",
              "workers_compensation_rate"
            ],
            "description": "Describes the type of requirement - each type may have additional metadata properties to describe possible values, formats, etc.\n\n- `text`: free-text input, no additional requirements\n- `currency`: a value representing a dollar amount, e.g. `374.55` representing `$374.55`\n- `radio`: choose one of options provided, see `options`\n- `select`: choose one of options provided, see `options`\n- `percent`: A decimal value representing a percentage, e.g. `0.034` representing `3.4%`\n- `account_number`: An account number for a tax agency, more information provided by `mask` and `prefix`\n- `tax_rate`: A decimal value representing a tax rate, e.g. `0.034` representing a tax rate of `3.4%`, see `validation` for additional validation guidance\n- `workers_compensation_rate`: A decimal value representing a percentage, see `risk_class_code`, `risk_class_description`, and `rate_type`\n",
            "readOnly": true
          },
          "options": {
            "type": "array",
            "description": "[for `select` or `radio`] An array of objects describing the possible values.",
            "items": {
              "type": "object",
              "properties": {
                "label": {
                  "type": "string",
                  "description": "A customer facing label for the answer"
                },
                "value": {
                  "oneOf": [
                    {
                      "type": "string"
                    },
                    {
                      "type": "boolean"
                    }
                  ],
                  "description": "The actual value to be submitted"
                },
                "short_label": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "A less verbose label that may sometimes be available"
                }
              },
              "required": [
                "label",
                "value"
              ]
            }
          },
          "risk_class_code": {
            "type": "string",
            "description": "[for `workers_compensation_rate`] The industry risk class code for the rate being requested"
          },
          "risk_class_description": {
            "type": "string",
            "description": "[for `workers_compensation_rate`] A description of the industry risk class for the rate being requested"
          },
          "rate_type": {
            "type": "string",
            "description": "[for `workers_compensation_rate`] The type of rate being collected. Either:\n  - `percent`: A percentage formatted as a decimal, e.g. `0.01` for 1%\n  - `currency_per_hour`: A dollar amount per hour, e.g. `3.24` for $3.24/hr\n",
            "enum": [
              "percent",
              "currency_per_hour"
            ]
          },
          "mask": {
            "type": [
              "string",
              "null"
            ],
            "description": "[for `account_number`] A pattern describing the format of the account number\n\nThe mask is a sequence of characters representing the requirements of the actual account number. Each character in the mask represents a single character in the account number as follows:\n- `#`: a digit (`\\d`)\n- `@`: a upper or lower case letter (`[a-zA-Z]`)\n- `^`: an uppercase letter (`[A-Z]`)\n- `%`: a digit or uppercase letter (`[0-9A-Z]`)\n- any other character represents the literal character\n\nExamples:\n- mask: `WHT-######` represents `WHT-` followed by 5 digits, e.g. `WHT-33421`\n- mask: `%####-^^` supports values of `75544-AB` and `Z7654-HK`\n"
          },
          "prefix": {
            "type": [
              "string",
              "null"
            ],
            "description": "[for `account_number`] A value that precedes the value to be collected - useful for display, but should not be submitted as part of the value. E.g. some tax agencies use an account number that is a company's federal ein plus two digits. In that case the mask would be `##` and the prefix `XXXXX1234`."
          },
          "validation": {
            "type": "object",
            "description": "[for `tax_rate`] Describes the validation required for the tax rate",
            "properties": {
              "type": {
                "type": "string",
                "description": "Describes the type of tax_rate validation rule",
                "enum": [
                  "one_of",
                  "min_max"
                ]
              },
              "min": {
                "type": "string",
                "description": "[for `min_max`] The inclusive lower bound of the tax rate"
              },
              "max": {
                "type": "string",
                "description": "[for `min_max`] The inclusive upper bound of the tax rate"
              },
              "rates": {
                "type": "array",
                "description": "[for `one_of`] The possible, unformatted tax rates for selection.\n- e.g. [\"0.0\", \"0.001\"] representing 0% and 0.1%\n",
                "items": {
                  "type": "string"
                }
              }
            },
            "required": [
              "type"
            ]
          }
        },
        "required": [
          "type"
        ],
        "description": ""
      },
      "Tax-Requirement-Set": {
        "type": "object",
        "x-examples": {
          "tax-requirements-set-ga-registrations-example": {
            "state": "GA",
            "key": "registrations",
            "label": "Registrations",
            "effective_from": null,
            "requirements": [
              {
                "key": "71653ec0-00b5-4c66-a58b-22ecf21704c5",
                "applicable_if": [],
                "label": "Withholding Number",
                "description": "If you have run payroll in the past in GA, find your withholding number on notices received from the Georgia Department of Revenue, or call the agency at (877) 423-6711. If you don’t have a number yet, you should <a target='_blank' data-bypass href='https://gtc.dor.ga.gov/_/#1'>register the business online</a>. The last two characters of your ID must be upper case letters.",
                "value": "1233214-AB",
                "metadata": {
                  "type": "account_number",
                  "mask": "#######-^^",
                  "prefix": null
                }
              },
              {
                "key": "6c0911ab-5860-412e-bdef-6437cd881df5",
                "applicable_if": [],
                "label": "DOL Account Number",
                "description": "If you have run payroll in the past in GA, find your DOL account number on notices received from the Georgia Department of Labor, or call the agency at (404) 232-3300. If you don’t have an account number yet, please <a target='_blank' data-bypass href='https://support.gusto.com/hc/en-us/articles/210139038#registerdol'>follow the instructions here</a> to register your business with the Georgia Dept. of Labor.",
                "value": "474747-88",
                "metadata": {
                  "type": "account_number",
                  "mask": "######-##",
                  "prefix": null
                }
              }
            ]
          }
        },
        "description": "",
        "properties": {
          "state": {
            "$ref": "#/components/schemas/State"
          },
          "key": {
            "$ref": "#/components/schemas/Tax-Requirement-Set-Key"
          },
          "label": {
            "type": "string",
            "description": "Customer facing label for the requirement set, e.g. \"Registrations\""
          },
          "effective_from": {
            "$ref": "#/components/schemas/Tax-Requirement-Effective-From"
          },
          "requirements": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Tax-Requirement"
            }
          }
        }
      },
      "Tax-Requirements-State": {
        "title": "Tax-Requirements-State",
        "type": "object",
        "x-examples": {
          "tax-requirements-state-ga-example": {
            "company_uuid": "6c14eac3-0da2-474d-bda1-786b3602d381",
            "state": "GA",
            "requirement_sets": [
              {
                "state": "GA",
                "key": "registrations",
                "label": "Registrations",
                "effective_from": null,
                "requirements": [
                  {
                    "key": "71653ec0-00b5-4c66-a58b-22ecf21704c5",
                    "applicable_if": [],
                    "label": "Withholding Number",
                    "description": "If you have run payroll in the past in GA, find your withholding number on notices received from the Georgia Department of Revenue, or call the agency at (877) 423-6711. If you don’t have a number yet, you should <a target='_blank' data-bypass href='https://gtc.dor.ga.gov/_/#1'>register the business online</a>. The last two characters of your ID must be upper case letters.",
                    "value": "1233214-AB",
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "account_number",
                      "mask": "#######-^^",
                      "prefix": null
                    }
                  },
                  {
                    "key": "6c0911ab-5860-412e-bdef-6437cd881df5",
                    "applicable_if": [],
                    "label": "DOL Account Number",
                    "description": "If you have run payroll in the past in GA, find your DOL account number on notices received from the Georgia Department of Labor, or call the agency at (404) 232-3300. If you don’t have an account number yet, please <a target='_blank' data-bypass href='https://support.gusto.com/hc/en-us/articles/210139038#registerdol'>follow the instructions here</a> to register your business with the Georgia Dept. of Labor.",
                    "value": "474747-88",
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "account_number",
                      "mask": "######-##",
                      "prefix": null
                    }
                  }
                ]
              },
              {
                "state": "GA",
                "key": "taxrates",
                "label": "Tax Rates",
                "effective_from": "2022-01-01",
                "requirements": [
                  {
                    "key": "suireimbursable",
                    "applicable_if": [],
                    "label": "SUI Reimburser",
                    "description": "Instead of paying state unemployment insurance (SUI) taxes quarterly, some businesses (like non-profits or government organizations) may be allowed to reimburse the state if one of their employees collects unemployment benefits.",
                    "value": false,
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "radio",
                      "options": [
                        {
                          "label": "No, we cannot reimburse the state—we have to pay SUI taxes quarterly",
                          "short_label": "Not Reimbursable",
                          "value": false
                        },
                        {
                          "label": "Yes, we can reimburse the state if an employee collects SUI benefits—we don’t have to pay SUI taxes quarterly",
                          "short_label": "Reimbursable",
                          "value": true
                        }
                      ]
                    }
                  },
                  {
                    "key": "e0ac2284-8d30-4100-ae23-f85f9574868b",
                    "applicable_if": [
                      {
                        "key": "suireimbursable",
                        "value": false
                      }
                    ],
                    "label": "Total Tax Rate",
                    "description": "Haven't received your assigned rate yet? <a target='_blank' data-bypass href='https://support.gusto.com/article/106622236100000/State-unemployment-insurance-(SUI)-tax'>Find the new employer rate</a> and enter it here.",
                    "value": "0.05",
                    "editable": true,
                    "payroll_blocking": true,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "tax_rate",
                      "validation": {
                        "type": "min_max",
                        "min": "0.0004",
                        "max": "0.081"
                      }
                    }
                  }
                ]
              },
              {
                "state": "GA",
                "key": "depositschedules",
                "label": "Deposit Schedules",
                "effective_from": "2022-01-01",
                "requirements": [
                  {
                    "key": "6ddfcbeb-94d3-4003-bfc2-8c6e1ca9f70c",
                    "applicable_if": [],
                    "label": "Deposit Schedule",
                    "description": "Georgia rejects payments made on the wrong schedule. GA employers receive their schedule on a registration verification letter after registering with the Georgia Dept. of Revenue. If you are unsure, call the agency at (877) 423-6711. If you did not register your business yet, please <a target='_blank' data-bypass href='https://gtc.dor.ga.gov/_/#2'>register the business with the Georgia Dept. of Revenue</a>.",
                    "value": "Monthly",
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "select",
                      "options": [
                        {
                          "label": "Semiweekly",
                          "value": "Semi-weekly"
                        },
                        {
                          "label": "Monthly",
                          "value": "Monthly"
                        },
                        {
                          "label": "Quarterly",
                          "value": "Quarterly"
                        }
                      ]
                    }
                  }
                ]
              },
              {
                "state": "GA",
                "key": "depositschedules",
                "label": "Deposit Schedules",
                "effective_from": "2022-07-01",
                "requirements": [
                  {
                    "key": "6ddfcbeb-94d3-4003-bfc2-8c6e1ca9f70c",
                    "applicable_if": [],
                    "label": "Deposit Schedule",
                    "description": "Georgia rejects payments made on the wrong schedule. GA employers receive their schedule on a registration verification letter after registering with the Georgia Dept. of Revenue. If you are unsure, call the agency at (877) 423-6711. If you did not register your business yet, please <a target='_blank' data-bypass href='https://gtc.dor.ga.gov/_/#2'>register the business with the Georgia Dept. of Revenue</a>.",
                    "value": "Monthly",
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "select",
                      "options": [
                        {
                          "label": "Semiweekly",
                          "value": "Semi-weekly"
                        },
                        {
                          "label": "Monthly",
                          "value": "Monthly"
                        },
                        {
                          "label": "Quarterly",
                          "value": "Quarterly"
                        }
                      ]
                    }
                  }
                ]
              }
            ]
          },
          "tax-requirements-metadata-select": {
            "company_uuid": "6c14eac3-0da2-474d-bda1-786b3602d381",
            "state": "GA",
            "requirement_sets": [
              {
                "state": "GA",
                "key": "depositschedules",
                "label": "Deposit Schedules",
                "effective_from": "2022-01-01",
                "requirements": [
                  {
                    "key": "6ddfcbeb-94d3-4003-bfc2-8c6e1ca9f70c",
                    "applicable_if": [],
                    "label": "Deposit Schedule",
                    "description": "The deposit schedule assigned by the state agency.",
                    "value": "Monthly",
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "select",
                      "options": [
                        {
                          "label": "Semiweekly",
                          "value": "Semi-weekly"
                        },
                        {
                          "label": "Monthly",
                          "value": "Monthly"
                        },
                        {
                          "label": "Quarterly",
                          "value": "Quarterly"
                        }
                      ]
                    }
                  }
                ]
              }
            ]
          },
          "tax-requirements-metadata-radio": {
            "company_uuid": "6c14eac3-0da2-474d-bda1-786b3602d381",
            "state": "GA",
            "requirement_sets": [
              {
                "state": "GA",
                "key": "taxrates",
                "label": "Tax Rates",
                "effective_from": "2022-01-01",
                "requirements": [
                  {
                    "key": "suireimbursable",
                    "applicable_if": [],
                    "label": "SUI Reimburser",
                    "description": "Instead of paying state unemployment insurance (SUI) taxes quarterly, some businesses may be allowed to reimburse the state if one of their employees collects unemployment benefits.",
                    "value": false,
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "radio",
                      "options": [
                        {
                          "label": "No, we cannot reimburse the state—we have to pay SUI taxes quarterly",
                          "short_label": "Not Reimbursable",
                          "value": false
                        },
                        {
                          "label": "Yes, we can reimburse the state if an employee collects SUI benefits—we don't have to pay SUI taxes quarterly",
                          "short_label": "Reimbursable",
                          "value": true
                        }
                      ]
                    }
                  }
                ]
              }
            ]
          },
          "tax-requirements-metadata-account-number": {
            "company_uuid": "6c14eac3-0da2-474d-bda1-786b3602d381",
            "state": "GA",
            "requirement_sets": [
              {
                "state": "GA",
                "key": "registrations",
                "label": "Registrations",
                "effective_from": null,
                "requirements": [
                  {
                    "key": "71653ec0-00b5-4c66-a58b-22ecf21704c5",
                    "applicable_if": [],
                    "label": "Withholding Number",
                    "description": "Your state withholding account number.",
                    "value": "1233214-AB",
                    "editable": true,
                    "payroll_blocking": false,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "account_number",
                      "mask": "#######-^^",
                      "prefix": null
                    }
                  }
                ]
              }
            ]
          },
          "tax-requirements-metadata-tax-rate": {
            "company_uuid": "6c14eac3-0da2-474d-bda1-786b3602d381",
            "state": "GA",
            "requirement_sets": [
              {
                "state": "GA",
                "key": "taxrates",
                "label": "Tax Rates",
                "effective_from": "2022-01-01",
                "requirements": [
                  {
                    "key": "e0ac2284-8d30-4100-ae23-f85f9574868b",
                    "applicable_if": [
                      {
                        "key": "suireimbursable",
                        "value": false
                      }
                    ],
                    "label": "Total Tax Rate",
                    "description": "The assigned SUI tax rate for this state.",
                    "value": "0.05",
                    "editable": true,
                    "payroll_blocking": true,
                    "default_value_applied": false,
                    "metadata": {
                      "type": "tax_rate",
                      "validation": {
                        "type": "min_max",
                        "min": "0.0004",
                        "max": "0.081"
                      }
                    }
                  }
                ]
              }
            ]
          }
        },
        "description": "",
        "properties": {
          "company_uuid": {
            "type": "string"
          },
          "state": {
            "$ref": "#/components/schemas/State"
          },
          "requirement_sets": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Tax-Requirement-Set"
            }
          }
        }
      },
      "Tax-Requirements-Value": {
        "description": "The value or \"answer\" for a tax requirement. Type depends on the requirement metadata type (e.g. string for text/account_number, boolean for radio/checkbox, number for percent/currency/tax_rate). Null when the requirement has not been answered.",
        "example": "1233214-AB",
        "oneOf": [
          {
            "type": "boolean"
          },
          {
            "type": "string"
          },
          {
            "type": "number"
          },
          {
            "type": "null"
          }
        ]
      },
      "Tax-Requirement-Set-Key": {
        "title": "Tax-Requirement-Set-Key",
        "type": "string",
        "example": "registrations",
        "description": "An identifier for a set of requirements. A list of requirement sets can contain multiple sets with the same `key` and different `effective_from` values."
      },
      "Tax-Requirement-Key": {
        "title": "Tax-Requirement-Key",
        "type": "string",
        "example": "71653ec0-00b5-4c66-a58b-22ecf21704c5",
        "description": "An identifier for an individual requirement. Uniqueness is guaranteed within a requirement set."
      },
      "Tax-Requirement-Effective-From": {
        "title": "Tax-Requirement-Effective-From",
        "type": [
          "string",
          "null"
        ],
        "example": "2022-01-01",
        "description": "An ISO 8601 formatted date representing the date values became effective. Some requirement sets are effective dated, while others are not. Multiple requirement sets for the same state/key can/will exist with unique effective dates. If a requirement set is has an `effective_from` value, all requirement sets with the same key will also have an `effective_from` value."
      },
      "State": {
        "title": "State",
        "type": "string",
        "example": "GA",
        "description": "One of the two-letter state abbreviations for the fifty United States and the District of Columbia (DC)"
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
    "/v1/companies/{company_uuid}/tax_requirements/{state}": {
      "get": {
        "summary": "Get tax requirements for a state",
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
            "description": "The UUID of the company",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "state",
            "in": "path",
            "required": true,
            "description": "The two-letter state abbreviation",
            "example": "CA",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "scheduling",
            "in": "query",
            "required": false,
            "description": "When true, return \"new\" requirement sets with valid `effective_from` dates that are available to save new effective-dated values.",
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_uuid-tax_requirements-state",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Retrieves the detailed tax requirements for a specific state. The response includes requirement sets grouped by\ncategory (e.g., registrations, tax rates, deposit schedules), each containing individual requirements with their\ncurrent values, labels, and metadata describing the expected input format.\n\nUse this to build dynamic UIs for tax setup or to read the current tax configuration for a state.\n\nscope: `company_tax_requirements:read`",
        "tags": [
          "Tax Requirements"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "tax-requirements-state-ga-example": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Requirements-State/x-examples/tax-requirements-state-ga-example"
                    }
                  },
                  "tax-requirements-metadata-select": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Requirements-State/x-examples/tax-requirements-metadata-select"
                    }
                  },
                  "tax-requirements-metadata-radio": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Requirements-State/x-examples/tax-requirements-metadata-radio"
                    }
                  },
                  "tax-requirements-metadata-account-number": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Requirements-State/x-examples/tax-requirements-metadata-account-number"
                    }
                  },
                  "tax-requirements-metadata-tax-rate": {
                    "value": {
                      "$ref": "#/components/schemas/Tax-Requirements-State/x-examples/tax-requirements-metadata-tax-rate"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Tax-Requirements-State"
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
