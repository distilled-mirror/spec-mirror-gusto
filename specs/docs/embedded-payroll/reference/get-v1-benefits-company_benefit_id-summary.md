---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get company benefit summary by company benefit id.

Returns summary benefit data for the requested company benefit id.

Benefits containing PHI are only visible to applications with the `company_benefits:read:phi` scope.

scope: `company_benefits:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Company Benefits"
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
      "Benefit-Summary": {
        "description": "",
        "type": "object",
        "x-tags": [
          "Company Benefits"
        ],
        "x-examples": {
          "typical_summary": {
            "start_date": "2022-01-01",
            "end_date": "2022-12-31",
            "description": "Simple IRA",
            "company_benefit_deduction": "60.0",
            "company_benefit_contribution": "30.0",
            "employees": [
              {
                "uuid": "54b7114f-f5e2-4f4b-911b-5cd5ad9032b0",
                "company_benefit_deduction": "60.0",
                "company_benefit_contribution": "30.0",
                "benefit_deduction": "660.0",
                "benefit_contribution": "330.0",
                "gross_pay": "18000.0",
                "imputed_pay": "350.0",
                "payroll_benefits": [
                  {
                    "payroll_uuid": "8cc3471b-9da5-47df-88ea-f238c7cb968b",
                    "payroll_type": "Regular",
                    "check_date": "2022-03-01",
                    "gross_pay": "3000.0",
                    "imputed_pay": "70.0",
                    "company_benefit_deduction": "10.0",
                    "company_benefit_contribution": "5.0",
                    "pay_period": {
                      "start_date": "2022-02-01",
                      "end_date": "2022-02-28"
                    }
                  },
                  {
                    "payroll_uuid": "d9d92786-722b-4bf7-bb32-79140418d349",
                    "payroll_type": "Bonus",
                    "check_date": "2022-12-31",
                    "gross_pay": "3000.0",
                    "imputed_pay": "70.0",
                    "company_benefit_deduction": "20.0",
                    "company_benefit_contribution": "10.0",
                    "pay_period": {
                      "start_date": "nil",
                      "end_date": "nil"
                    }
                  }
                ]
              }
            ]
          }
        },
        "properties": {
          "start_date": {
            "type": "string",
            "description": "The start date of benefit summary."
          },
          "end_date": {
            "type": "string",
            "description": "The end date of benefit summary."
          },
          "description": {
            "type": "string",
            "description": "Description of the benefit."
          },
          "company_benefit_deduction": {
            "type": "string",
            "description": "The aggregate of employee deduction for all employees given the period of time and the specific company benefit."
          },
          "company_benefit_contribution": {
            "type": "string",
            "description": "The aggregate of company contribution for all employees given the period of time and the specific company benefit."
          },
          "employees": {
            "type": "array",
            "description": "",
            "items": {
              "type": "object",
              "properties": {
                "uuid": {
                  "type": "string",
                  "description": "The UUID of the employee"
                },
                "company_benefit_deduction": {
                  "type": "string",
                  "description": "The sum of employee deduction for this employee given the period of time and the specific company benefit."
                },
                "company_benefit_contribution": {
                  "type": "string",
                  "description": "The sum of company contribution for this employee given the period of time and the specific company benefit."
                },
                "benefit_deduction": {
                  "type": "string",
                  "description": "The sum of employee benefit deduction for this employee given the period of time and the benefit type."
                },
                "benefit_contribution": {
                  "type": "string",
                  "description": "The sum of company contribution for this employee given the period of time and the benefit type."
                },
                "gross_pay": {
                  "type": "string",
                  "description": "Gross pay for this employee given the period of time."
                },
                "imputed_pay": {
                  "type": "string",
                  "description": "Total imputed pay for this employee given the period of time (not scoped to a benefit type)."
                },
                "payroll_benefits": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "payroll_uuid": {
                        "type": "string"
                      },
                      "payroll_type": {
                        "type": "string",
                        "description": "Whether it is regular or bonus payroll"
                      },
                      "check_date": {
                        "type": "string",
                        "description": "Check date of this payroll."
                      },
                      "gross_pay": {
                        "type": "string",
                        "description": "Gross pay for this employee on the payroll."
                      },
                      "imputed_pay": {
                        "type": "string",
                        "description": "Total imputed pay for this employee on the payroll."
                      },
                      "company_benefit_deduction": {
                        "type": "string",
                        "description": "The employee benefit deduction amount for this employee on the payroll."
                      },
                      "company_benefit_contribution": {
                        "type": "string",
                        "description": "The company contribution amount for this employee on the payroll."
                      },
                      "pay_period": {
                        "type": "object",
                        "properties": {
                          "start_date": {
                            "type": [
                              "string",
                              "null"
                            ],
                            "description": "The beginning of the payroll's pay period."
                          },
                          "end_date": {
                            "type": [
                              "string",
                              "null"
                            ],
                            "description": "The end of the payroll's pay period."
                          }
                        }
                      }
                    }
                  }
                }
              }
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
    "/v1/company_benefits/{company_benefit_id}/summary": {
      "get": {
        "summary": "Get company benefit summary by company benefit id.",
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
            "name": "company_benefit_id",
            "in": "path",
            "description": "The UUID of the company benefit",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "start_date",
            "in": "query",
            "required": false,
            "description": "The start date for which to retrieve company benefit summary",
            "example": "2022-01-01",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "end_date",
            "in": "query",
            "required": false,
            "description": "The end date for which to retrieve company benefit summary. If left empty, defaults to today's date.",
            "example": "2022-12-31",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "detailed",
            "in": "query",
            "required": false,
            "description": "Display employee payroll item summary",
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-benefits-company_benefit_id-summary",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns summary benefit data for the requested company benefit id.\n\nBenefits containing PHI are only visible to applications with the `company_benefits:read:phi` scope.\n\nscope: `company_benefits:read`",
        "tags": [
          "Company Benefits"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Benefit summary response",
            "content": {
              "application/json": {
                "examples": {
                  "typical_summary": {
                    "value": {
                      "$ref": "#/components/schemas/Benefit-Summary/x-examples/typical_summary"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Benefit-Summary"
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
