---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an employee benefit

Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee’s enrollment.

Benefits containing PHI are only visible to applications with the `employee_benefits:read:phi` scope.

scope: `employee_benefits:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Employee Benefits"
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
      "Employee-Benefit-Base-Object": {
        "description": "",
        "type": "object",
        "title": "",
        "additionalProperties": true,
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/idempotency) for information on how to use this field."
          },
          "active": {
            "type": "boolean",
            "default": true,
            "description": "Whether the employee benefit is active."
          },
          "employee_deduction": {
            "type": "string",
            "default": "0.00",
            "description": "The amount to be deducted, per pay period, from the employee's pay."
          },
          "deduct_as_percentage": {
            "type": "boolean",
            "default": false,
            "description": "Whether the employee deduction amount should be treated as a percentage to be deducted from each payroll."
          },
          "employee_deduction_annual_maximum": {
            "type": [
              "string",
              "null"
            ],
            "description": "The maximum employee deduction amount per year. A null value signifies no limit."
          },
          "contribution": {
            "type": "object",
            "description": "An object representing the type and value of the company contribution.",
            "properties": {
              "type": {
                "type": "string",
                "description": "The company contribution scheme.\n\n\"amount\": The company contributes a fixed amount per payroll. If elective is true, the contribution is matching, dollar-for-dollar.\n\n\"percentage\": The company contributes a percentage of the payroll amount per payroll period. If elective is true, the contribution is matching, dollar-for-dollar.\n\n\"tiered\": The company contribution varies according to the size of the employee deduction."
              },
              "value": {
                "description": "For the `amount` and `percentage` contribution types, the value of the corresponding amount or percentage.\n\nFor the `tiered` contribution type, an array of tiers.",
                "oneOf": [
                  {
                    "type": "string"
                  },
                  {
                    "type": "object",
                    "properties": {
                      "tiers": {
                        "type": "array",
                        "description": "",
                        "items": {
                          "type": "object",
                          "description": "A single tier of a tiered matching scheme.",
                          "properties": {
                            "rate": {
                              "type": "string",
                              "description": "The percentage of employee deduction within this tier the company contribution will match."
                            },
                            "threshold": {
                              "type": "string",
                              "description": "Specifies the upper limit (inclusive) percentage of the employee contribution that this tier applies to.\n\nUse threshold to define each tier's end point, with tiers applied cumulatively from 0% upwards.\n\nFor example:\n\nIf the first tier has a threshold of \"3\", and `rate` of \"100\", the company will match 100% of employee contributions from 0% up to and including 3% of payroll.\n\nIf the next tier has a threshold of \"5\" and a rate of \"50\", the company will match 50% of contributions from above 3% up to and including 5% of payroll."
                            },
                            "threshold_delta": {
                              "type": "string",
                              "description": "The step up difference between this tier's threshold and the previous tier's threshold. In the first tier, this is equivalent to threshold."
                            }
                          }
                        }
                      }
                    }
                  }
                ]
              }
            }
          },
          "elective": {
            "type": "boolean",
            "description": "Whether the company contribution is elective (aka matching). For \"tiered\" contribution types, this is always true.",
            "default": false
          },
          "company_contribution_annual_maximum": {
            "type": [
              "string",
              "null"
            ],
            "description": "The maximum company contribution amount per year. A null value signifies no limit."
          },
          "limit_option": {
            "type": [
              "string",
              "null"
            ],
            "description": "Some benefits require additional information to determine their limit.\n\n`Family` and `Individual` are applicable to HSA benefit.\n\n`Joint Filing or Single` and `Married and Filing Separately` are applicable to Dependent Care FSA benefit."
          },
          "catch_up": {
            "type": [
              "boolean",
              "null"
            ],
            "default": false,
            "description": "Whether the employee should use a benefit's \"catch up\" rate. Only Roth 401k and 401k benefits use this value for employees over 50."
          },
          "retirement_loan_identifier": {
            "type": [
              "string",
              "null"
            ],
            "description": "Identifier for a 401(k) loan assigned by the 401(k) provider"
          },
          "coverage_amount": {
            "type": [
              "string",
              "null"
            ],
            "description": "The amount that the employee is insured for. Note: company contribution cannot be present if coverage amount is set."
          },
          "deduction_reduces_taxable_income": {
            "description": "Whether the employee deduction reduces taxable income or not. Only valid for Group Term Life benefits. Note: when the value is not \"unset\", coverage amount and coverage salary multiplier are ignored.",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "unset",
                  "reduces_taxable_income",
                  "does_not_reduce_taxable_income"
                ]
              },
              {
                "type": "null"
              }
            ],
            "default": "unset"
          },
          "coverage_salary_multiplier": {
            "type": [
              "string",
              "null"
            ],
            "default": "0.00",
            "description": "The coverage amount as a multiple of the employee's salary. Only applicable for Group Term Life benefits. Note: cannot be set if coverage amount is also set."
          },
          "company_contribution": {
            "type": "string",
            "default": "0.00",
            "description": "The amount to be paid, per pay period, by the company. This field will not appear for tiered contribution types.",
            "deprecated": true
          },
          "contribute_as_percentage": {
            "type": "boolean",
            "default": false,
            "description": "Whether the company_contribution value should be treated as a percentage to be added to each payroll. This field will not appear for tiered contribution types.",
            "deprecated": true
          },
          "effective_date": {
            "type": "string",
            "format": "date",
            "description": "The date the employee benefit will start."
          },
          "expiration_date": {
            "type": [
              "string",
              "null"
            ],
            "format": "date",
            "description": "The date the employee benefit will expire. A null value indicates the benefit will not expire."
          }
        }
      },
      "Employee-Benefit": {
        "description": "The representation of an employee benefit.",
        "type": "object",
        "title": "",
        "x-examples": {
          "Example": {
            "version": "09j3d29jqdpj92109j9j2d90dq",
            "employee_uuid": "73274962-63ce-4e5c-b689-1df8d4df09f4",
            "company_benefit_uuid": "54e37c27-43e6-4ae5-a5b2-e29895a133be",
            "active": true,
            "uuid": "e91ca856-a915-4339-9b18-29f9cd66b031",
            "employee_deduction": "100.00",
            "company_contribution": "100.00",
            "employee_deduction_annual_maximum": "200.00",
            "company_contribution_annual_maximum": "200.00",
            "limit_option": null,
            "retirement_loan_identifier": null,
            "deduct_as_percentage": false,
            "contribute_as_percentage": false,
            "catch_up": false,
            "coverage_amount": null,
            "deduction_reduces_taxable_income": null,
            "coverage_salary_multiplier": "0.00",
            "contribution": {
              "type": "amount",
              "value": "100.00"
            },
            "elective": false,
            "effective_date": "2025-01-01",
            "expiration_date": null
          },
          "Tiered Example": {
            "version": "09j3d29jqdpj92109j9j2d90dq",
            "employee_uuid": "73274962-63ce-4e5c-b689-1df8d4df09f4",
            "company_benefit_uuid": "54e37c27-43e6-4ae5-a5b2-e29895a133be",
            "active": true,
            "uuid": "e91ca856-a915-4339-9b18-29f9cd66b031",
            "employee_deduction": "100.00",
            "employee_deduction_annual_maximum": "200.00",
            "company_contribution_annual_maximum": "200.00",
            "limit_option": null,
            "deduct_as_percentage": false,
            "catch_up": false,
            "coverage_amount": null,
            "deduction_reduces_taxable_income": null,
            "coverage_salary_multiplier": "0.00",
            "elective": true,
            "contribution": {
              "type": "tiered",
              "value": {
                "tiers": [
                  {
                    "rate": "100.0",
                    "threshold": "2.0",
                    "threshold_delta": "2.0"
                  },
                  {
                    "rate": "50.0",
                    "threshold": "5.0",
                    "threshold_delta": "3.0"
                  }
                ]
              }
            },
            "effective_date": "2025-01-01",
            "expiration_date": null
          }
        },
        "allOf": [
          {
            "$ref": "#/components/schemas/Employee-Benefit-Base-Object"
          },
          {
            "type": "object",
            "additionalProperties": true,
            "properties": {
              "employee_uuid": {
                "type": "string",
                "description": "The UUID of the employee to which the benefit belongs.",
                "readOnly": true
              },
              "company_benefit_uuid": {
                "type": "string",
                "description": "The UUID of the company benefit.",
                "readOnly": true
              },
              "uuid": {
                "type": "string",
                "description": "The UUID of the employee benefit.",
                "readOnly": true
              }
            }
          }
        ],
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
    "/v1/employee_benefits/{employee_benefit_id}": {
      "get": {
        "summary": "Get an employee benefit",
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
            "name": "employee_benefit_id",
            "in": "path",
            "description": "The UUID of the employee benefit.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-employee_benefits-employee_benefit_id",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Employee benefits represent an employee enrolled in a particular company benefit. It includes information specific to that employee’s enrollment.\n\nBenefits containing PHI are only visible to applications with the `employee_benefits:read:phi` scope.\n\nscope: `employee_benefits:read`",
        "tags": [
          "Employee Benefits"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Example response",
            "content": {
              "application/json": {
                "examples": {
                  "Example": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Benefit/x-examples/Example"
                    }
                  },
                  "Tiered Example": {
                    "value": {
                      "$ref": "#/components/schemas/Employee-Benefit/x-examples/Tiered Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Employee-Benefit"
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
