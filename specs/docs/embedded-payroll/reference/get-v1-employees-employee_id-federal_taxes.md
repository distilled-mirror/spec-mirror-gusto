---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get federal taxes for an employee

Returns federal tax information for an employee. The response structure varies based on the w4_data_type (pre_2020_w4 or rev_2020_w4).

scope: `employee_federal_taxes:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employee Tax Setup"
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
      "Employee-Federal-Tax-Pre2020": {
        "title": "Employee-Federal-Tax-Pre2020",
        "type": "object",
        "description": "Federal tax information for employees using the pre-2020 W4 form.",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee."
          },
          "employee_id": {
            "type": "integer",
            "description": "The internal ID of the employee."
          },
          "company_id": {
            "type": "integer",
            "description": "The internal ID of the company."
          },
          "w4_data_type": {
            "type": "string",
            "description": "The version of w4 form.",
            "enum": [
              "pre_2020_w4"
            ]
          },
          "filing_status": {
            "type": [
              "string",
              "null"
            ],
            "description": "It determines which tax return form an individual will use and is an important factor in computing taxable income. One of:\n- Single\n- Married\n- Head of Household\n- Exempt from withholding\n- Married, but withhold as Single"
          },
          "federal_withholding_allowance": {
            "type": [
              "number",
              "null"
            ],
            "description": "An exemption from paying a certain amount of income tax. May be null when filing_status is \"Exempt from withholding\"."
          },
          "additional_withholding": {
            "type": "string",
            "description": "An additional withholding dollar amount."
          }
        },
        "required": [
          "version",
          "w4_data_type",
          "additional_withholding"
        ],
        "x-tags": [
          "Employee Tax Setup"
        ]
      },
      "Employee-Federal-Tax-Rev2020": {
        "title": "Employee-Federal-Tax-Rev2020",
        "type": "object",
        "description": "Federal tax information for employees using the revised 2020 W4 form.",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "employee_uuid": {
            "type": "string",
            "description": "The UUID of the employee."
          },
          "employee_id": {
            "type": "integer",
            "description": "The internal ID of the employee."
          },
          "company_id": {
            "type": "integer",
            "description": "The internal ID of the company."
          },
          "w4_data_type": {
            "type": "string",
            "description": "The version of w4 form.",
            "enum": [
              "rev_2020_w4"
            ]
          },
          "filing_status": {
            "type": [
              "string",
              "null"
            ],
            "description": "It determines which tax return form an individual will use and is an important factor in computing taxable income. One of:\n- Single\n- Married\n- Head of Household\n- Exempt from withholding"
          },
          "extra_withholding": {
            "type": [
              "string",
              "null"
            ],
            "description": "An employee can request an additional amount to be withheld from each paycheck."
          },
          "two_jobs": {
            "type": [
              "boolean",
              "null"
            ],
            "description": "If there are only two jobs (i.e., you and your spouse each have a job, or you have two), you can set it to true."
          },
          "dependents_amount": {
            "type": [
              "string",
              "null"
            ],
            "description": "A dependent is a person other than the taxpayer or spouse who entitles the taxpayer to claim a dependency exemption."
          },
          "other_income": {
            "type": [
              "string",
              "null"
            ],
            "description": "Other income amount."
          },
          "deductions": {
            "type": [
              "string",
              "null"
            ],
            "description": "Deductions other than the standard deduction to reduce withholding."
          }
        },
        "required": [
          "version",
          "w4_data_type",
          "filing_status",
          "extra_withholding",
          "two_jobs",
          "dependents_amount",
          "other_income",
          "deductions"
        ],
        "x-tags": [
          "Employee Tax Setup"
        ]
      },
      "Employee-Federal-Tax": {
        "title": "Employee-Federal-Tax",
        "type": "object",
        "description": "Federal tax information for an employee. The response structure varies based on the w4_data_type field.",
        "oneOf": [
          {
            "$ref": "#/components/schemas/Employee-Federal-Tax-Pre2020"
          },
          {
            "$ref": "#/components/schemas/Employee-Federal-Tax-Rev2020"
          }
        ],
        "discriminator": {
          "propertyName": "w4_data_type",
          "mapping": {
            "pre_2020_w4": "#/components/schemas/Employee-Federal-Tax-Pre2020",
            "rev_2020_w4": "#/components/schemas/Employee-Federal-Tax-Rev2020"
          }
        },
        "x-examples": {
          "rev_2020_w4": {
            "version": "56a489ce86ed6c1b0f0cecc4050a0b01",
            "filing_status": "Single",
            "two_jobs": false,
            "dependents_amount": "1000.0",
            "other_income": "10.0",
            "deductions": "11.0",
            "extra_withholding": "9.0",
            "w4_data_type": "rev_2020_w4",
            "employee_uuid": "7d70e6b0-9889-4060-9eef-aafabc14e2f2",
            "employee_id": 1,
            "company_id": 1
          },
          "rev_2020_w4_married_two_jobs": {
            "version": "63859768485e218ccf8a449bb60f14ed",
            "w4_data_type": "rev_2020_w4",
            "filing_status": "Married",
            "two_jobs": true,
            "dependents_amount": "2000.0",
            "other_income": "20.0",
            "deductions": "11.0",
            "extra_withholding": "9.0",
            "employee_uuid": "8d70e6b0-9889-4060-9eef-aafabc14e2f2",
            "employee_id": 2,
            "company_id": 1
          }
        },
        "x-tags": [
          "Employee Tax Setup"
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
    "/v1/employees/{employee_uuid}/federal_taxes": {
      "get": {
        "summary": "Get federal taxes for an employee",
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
            "name": "employee_uuid",
            "in": "path",
            "description": "The UUID of the employee",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employees-employee_id-federal_taxes",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns federal tax information for an employee. The response structure varies based on the w4_data_type (pre_2020_w4 or rev_2020_w4).\n\nscope: `employee_federal_taxes:read`",
        "tags": [
          "Employee Tax Setup"
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
                  "rev_2020_w4": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Federal-Tax/x-examples/rev_2020_w4"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Federal-Tax"
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
