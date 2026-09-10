---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get an external payroll

Get an external payroll for a given company.

scope: `external_payrolls:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "External Payrolls"
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
      "External-Payroll": {
        "description": "The representation of an external payroll.",
        "type": "object",
        "x-tags": [
          "External Payrolls"
        ],
        "title": "",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the external payroll.",
            "readOnly": true
          },
          "company_uuid": {
            "type": "string",
            "description": "The UUID of the company.",
            "readOnly": true
          },
          "check_date": {
            "type": "string",
            "description": "External payroll's check date.",
            "readOnly": true
          },
          "payment_period_start_date": {
            "type": "string",
            "description": "External payroll's pay period start date.",
            "readOnly": true
          },
          "payment_period_end_date": {
            "type": "string",
            "description": "External payroll's pay period end date.",
            "readOnly": true
          },
          "status": {
            "type": "string",
            "enum": [
              "unprocessed",
              "processed"
            ],
            "description": "The status of the external payroll. The status will be `unprocessed` when the external payroll is created and transition to `processed` once tax liabilities are entered and finalized.  Once in the `processed` status all actions that can edit an external payroll will be disabled.",
            "readOnly": true
          },
          "external_payroll_items": {
            "type": "array",
            "description": "External payroll items for employees",
            "readOnly": true,
            "items": {
              "type": "object",
              "properties": {
                "employee_uuid": {
                  "type": "string"
                },
                "earnings": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "amount": {
                        "type": "string",
                        "format": "float"
                      },
                      "hours": {
                        "type": "string",
                        "format": "float"
                      },
                      "earning_type": {
                        "type": "string"
                      },
                      "earning_id": {
                        "type": "integer"
                      }
                    }
                  }
                },
                "benefits": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "benefit_id": {
                        "type": "integer"
                      },
                      "company_contribution_amount": {
                        "type": "string",
                        "format": "float"
                      },
                      "employee_deduction_amount": {
                        "type": "string",
                        "format": "float"
                      }
                    }
                  }
                },
                "taxes": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "tax_id": {
                        "type": "integer"
                      },
                      "amount": {
                        "type": "string",
                        "format": "float"
                      }
                    }
                  }
                }
              }
            }
          },
          "applicable_earnings": {
            "type": "array",
            "description": "Applicable earnings based on company provisioning.",
            "readOnly": true,
            "items": {
              "type": "object",
              "properties": {
                "earning_type": {
                  "type": "string"
                },
                "earning_id": {
                  "type": "number"
                },
                "name": {
                  "type": "string"
                },
                "input_type": {
                  "type": "string"
                },
                "category": {
                  "type": "string"
                }
              }
            }
          },
          "applicable_benefits": {
            "type": [
              "array",
              "null"
            ],
            "description": "Applicable benefits based on company provisioning.",
            "readOnly": true,
            "items": {
              "type": "object",
              "properties": {
                "id": {
                  "type": "integer"
                },
                "description": {
                  "type": "string"
                },
                "active": {
                  "type": "boolean"
                }
              }
            }
          },
          "applicable_taxes": {
            "type": "array",
            "description": "Applicable taxes based on company provisioning.",
            "readOnly": true,
            "items": {
              "type": "object",
              "properties": {
                "id": {
                  "type": "integer"
                },
                "name": {
                  "type": "string"
                },
                "employer_tax": {
                  "type": "boolean",
                  "description": "Some taxes may have an amount withheld from the employee and an amount withheld from the employer, e.g. Social Security. A `true` value indicates this is the employer's amount."
                },
                "resident_tax": {
                  "type": "boolean",
                  "description": "Some taxes may have different rates or reporting requirements depending on if the employee is a resident or non-resident of the tax jurisdiction."
                }
              }
            }
          },
          "metadata": {
            "type": "object",
            "description": "Stores metadata of the external payroll.",
            "readOnly": true,
            "properties": {
              "deletable": {
                "type": "boolean",
                "description": "Determines if the external payroll can be deleted.",
                "readOnly": true
              }
            }
          }
        },
        "x-examples": {
          "Example": {
            "uuid": "c5fdae57-5483-4529-9aae-f0edceed92d4",
            "company_uuid": "bcb305b0-2855-4025-8d22-e484a9e6b7c9",
            "check_date": "2022-06-03",
            "payment_period_start_date": "2022-05-15",
            "payment_period_end_date": "2022-05-30",
            "status": "unprocessed",
            "external_payroll_items": [
              {
                "employee_uuid": "44f7cba9-7a3d-4f08-b7bd-6fcf5211f8ca",
                "earnings": [
                  {
                    "amount": "10000.0",
                    "hours": "0.0",
                    "earning_type": "CompanyPayType",
                    "earning_id": 1
                  },
                  {
                    "amount": "500.0",
                    "hours": "0.0",
                    "earning_type": "CompanyEarningType",
                    "earning_id": 4
                  }
                ],
                "benefits": [
                  {
                    "benefit_id": 22,
                    "company_contribution_amount": "100.0",
                    "employee_deduction_amount": "50.0"
                  },
                  {
                    "benefit_id": 25,
                    "company_contribution_amount": "0.0",
                    "employee_deduction_amount": "300.0"
                  }
                ],
                "taxes": [
                  {
                    "tax_id": 1,
                    "amount": "400.0"
                  },
                  {
                    "tax_id": 2,
                    "amount": "60.0"
                  }
                ]
              }
            ],
            "applicable_earnings": [
              {
                "earning_type": "CompanyPayType",
                "earning_id": 1,
                "name": "Regular Wages",
                "input_type": "amount",
                "category": "default"
              },
              {
                "earning_type": "CompanyEarningType",
                "earning_id": 4,
                "name": "Cash Tips",
                "input_type": "amount",
                "category": "default"
              }
            ],
            "applicable_benefits": [
              {
                "id": 22,
                "description": "Kaiser",
                "active": true
              },
              {
                "id": 25,
                "description": "HSA",
                "active": true
              }
            ],
            "applicable_taxes": [
              {
                "id": 1,
                "name": "Federal Income Tax",
                "employer_tax": false,
                "resident_tax": false
              },
              {
                "id": 2,
                "name": "Social Security",
                "employer_tax": false,
                "resident_tax": false
              }
            ],
            "metadata": {
              "deletable": true
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
    "/v1/companies/{company_uuid}/external_payrolls/{external_payroll_id}": {
      "get": {
        "summary": "Get an external payroll",
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
            "description": "The UUID of the company",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "external_payroll_id",
            "in": "path",
            "description": "The UUID of the external payroll",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-external-payroll",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "tags": [
          "External Payrolls"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "description": "Get an external payroll for a given company.\n\nscope: `external_payrolls:read`",
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "Example": {
                    "value": {
                      "$ref": "#/components/schemas/External-Payroll/x-examples/Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/External-Payroll"
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
