---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get jobs for an employee

Get all of the jobs that an employee holds.
Note: Compensation data (pay rate, payment unit, and related fields) represents sensitive employee pay information. When retrieving employee job data, these fields (`rate`, `payment_unit`, `current_compensation_uuid`, `compensations`) are only returned when the `compensations:read` scope is included. This allows you to access employee and job metadata without exposing pay rates.

Compensation data in the response requires the `compensations:read` scope.

scope: `jobs:read`

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
    "/v1/employees/{employee_id}/jobs": {
      "get": {
        "summary": "Get jobs for an employee",
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
            "name": "employee_id",
            "in": "path",
            "description": "The UUID of the employee",
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
        "operationId": "get-v1-employees-employee_id-jobs",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get all of the jobs that an employee holds.\nNote: Compensation data (pay rate, payment unit, and related fields) represents sensitive employee pay information. When retrieving employee job data, these fields (`rate`, `payment_unit`, `current_compensation_uuid`, `compensations`) are only returned when the `compensations:read` scope is included. This allows you to access employee and job metadata without exposing pay rates.\n\nCompensation data in the response requires the `compensations:read` scope.\n\nscope: `jobs:read`",
        "tags": [
          "Jobs and Compensations"
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
                  "example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Job/x-examples/example"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Job"
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
