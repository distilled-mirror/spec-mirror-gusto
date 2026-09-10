---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get compensations for a job

Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one that is active. The current compensation is the one with the most recent `effective_date`.

*Note: Currently the API does not support creating multiple compensations per job - creating a compensation with the same job_uuid as another will fail with a relevant error.*

Use `flsa_status` to determine if an employee is eligible for overtime
By default the API returns only the current compensation - use the `include` parameter to return all compensations.

scope: `compensations:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Jobs and Compensations"
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
    "/v1/jobs/{job_id}/compensations": {
      "get": {
        "summary": "Get compensations for a job",
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
            "name": "job_id",
            "in": "path",
            "description": "The UUID of the job",
            "required": true,
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
          },
          {
            "name": "include",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "all_compensations"
              ]
            },
            "description": "Available options:\n- all_compensations: Include all effective dated compensations for each job instead of only the current compensation\n"
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-jobs-job_id-compensations",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Compensations contain information on how much is paid out for a job. Jobs may have many compensations, but only one that is active. The current compensation is the one with the most recent `effective_date`.\n\n*Note: Currently the API does not support creating multiple compensations per job - creating a compensation with the same job_uuid as another will fail with a relevant error.*\n\nUse `flsa_status` to determine if an employee is eligible for overtime\nBy default the API returns only the current compensation - use the `include` parameter to return all compensations.\n\nscope: `compensations:read`",
        "tags": [
          "Jobs and Compensations"
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
                    "value": [
                      {
                        "$ref": "#/components/schemas/Compensation/x-examples/success_status"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Compensation"
                  }
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
