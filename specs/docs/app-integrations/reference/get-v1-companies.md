---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a company

Get a company.

The employees:read scope is required to return home_address and non-work locations.
The company_admin:read scope is required to return primary_payroll_admin.
The signatories:read scope is required to return primary_signatory.

scope: `companies:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Companies"
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
      "Company-Address": {
        "description": "The representation of a company's address in Gusto.",
        "type": "object",
        "properties": {
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
          "inactive": {
            "type": "boolean",
            "description": "The status of the location. Inactive locations have been deleted, but may still have historical data associated with them.",
            "readOnly": true
          },
          "active": {
            "type": "boolean",
            "description": "The status of the location. Inactive locations have been deleted, but may still have historical data associated with them.",
            "readOnly": true
          }
        }
      },
      "Company": {
        "title": "Company",
        "type": "object",
        "description": "The representation of a company in Gusto.",
        "properties": {
          "ein": {
            "type": "string",
            "description": "The Federal Employer Identification Number of the company.",
            "readOnly": true
          },
          "entity_type": {
            "description": "The tax payer type of the company.",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "C-Corporation",
                  "S-Corporation",
                  "Sole proprietor",
                  "LLC",
                  "LLP",
                  "Limited partnership",
                  "Co-ownership",
                  "Association",
                  "Trusteeship",
                  "General partnership",
                  "Joint venture",
                  "Non-Profit"
                ]
              },
              {
                "type": "null"
              }
            ],
            "readOnly": true
          },
          "contractor_only": {
            "type": "boolean",
            "description": "Whether the company only supports contractors."
          },
          "tier": {
            "type": [
              "string",
              "null"
            ],
            "description": "The Gusto product tier of the company (not applicable to Embedded partner managed companies).",
            "readOnly": true,
            "enum": [
              "simple",
              "plus",
              "premium",
              "core",
              "complete",
              "concierge",
              "contractor_only",
              "basic"
            ]
          },
          "is_suspended": {
            "type": "boolean",
            "description": "Whether or not the company is suspended in Gusto. Suspended companies may not run payroll."
          },
          "company_status": {
            "type": "string",
            "description": "The status of the company in Gusto. \"Approved\" companies are approved to run payroll from a risk and compliance perspective. However, an approved company may still need to resolve other [payroll blockers](https://docs.gusto.com/embedded-payroll/docs/payroll-blockers) to be able to run payroll. \"Not Approved\" companies may not yet run payroll with Gusto and may need to complete onboarding or contact support. \"Suspended\" companies may not run payroll with Gusto. In order to unsuspend their account, the company must contact support.",
            "enum": [
              "Approved",
              "Not Approved",
              "Suspended"
            ],
            "readOnly": true
          },
          "uuid": {
            "type": "string",
            "description": "A unique identifier of the company in Gusto.",
            "readOnly": true
          },
          "name": {
            "type": "string",
            "description": "The name of the company.",
            "readOnly": true
          },
          "slug": {
            "type": "string",
            "description": "The slug of the name of the company.",
            "readOnly": true
          },
          "trade_name": {
            "type": [
              "string",
              "null"
            ],
            "description": "The trade name of the company.",
            "readOnly": true
          },
          "is_partner_managed": {
            "type": "boolean",
            "description": "Whether the company is fully managed by a partner via the API",
            "readOnly": true
          },
          "is_high_risk_business": {
            "type": "boolean",
            "description": "Whether or not Gusto has identified the company as representing a high fraud risk.",
            "readOnly": true
          },
          "is_marijuana_business": {
            "type": "boolean",
            "description": "Whether or not the company is a marijuana-related business.",
            "readOnly": true
          },
          "pay_schedule_type": {
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "single",
                  "hourly_salaried",
                  "by_employee",
                  "by_department"
                ]
              },
              {
                "type": "null"
              }
            ],
            "description": "The pay schedule assignment type.",
            "readOnly": true
          },
          "join_date": {
            "type": [
              "string",
              "null"
            ],
            "description": "Company's first invoiceable event date",
            "readOnly": true
          },
          "funding_type": {
            "description": "Company's default funding type",
            "anyOf": [
              {
                "type": "string",
                "enum": [
                  "ach",
                  "reverse_wire",
                  "wire_in",
                  "partner_disbursement",
                  "rtp",
                  "line_of_credit"
                ]
              },
              {
                "type": "null"
              }
            ]
          },
          "locations": {
            "type": "array",
            "uniqueItems": false,
            "description": "The locations of the company.",
            "items": {
              "$ref": "#/components/schemas/Company-Address"
            },
            "readOnly": true
          },
          "compensations": {
            "type": "object",
            "description": "The available company-wide compensation rates for the company.",
            "properties": {
              "hourly": {
                "type": "array",
                "uniqueItems": true,
                "description": "The available hourly compensation rates for the company.",
                "items": {
                  "type": "object",
                  "properties": {
                    "uuid": {
                      "type": [
                        "string",
                        "null"
                      ],
                      "description": "The UUID of the hourly compensation rate.",
                      "readOnly": true
                    },
                    "name": {
                      "type": "string",
                      "description": "The name of the hourly compensation rate.",
                      "example": "Overtime",
                      "readOnly": true
                    },
                    "multiple": {
                      "type": "number",
                      "description": "The amount multiplied by the base rate of a job to calculate compensation.",
                      "example": 1.5,
                      "readOnly": true
                    }
                  },
                  "readOnly": true
                },
                "readOnly": true
              },
              "fixed": {
                "type": "array",
                "uniqueItems": true,
                "description": "The available fixed compensation rates for the company.",
                "items": {
                  "type": "object",
                  "properties": {
                    "uuid": {
                      "type": [
                        "string",
                        "null"
                      ],
                      "description": "The UUID of the fixed compensation.",
                      "readOnly": true
                    },
                    "name": {
                      "type": "string",
                      "description": "The name of the fixed compensation.",
                      "example": "Bonus"
                    }
                  },
                  "readOnly": true
                },
                "readOnly": true
              },
              "paid_time_off": {
                "type": "array",
                "uniqueItems": true,
                "description": "The available types of paid time off for the company.",
                "items": {
                  "type": "object",
                  "properties": {
                    "uuid": {
                      "type": [
                        "string",
                        "null"
                      ],
                      "description": "The UUID of the paid time off type.",
                      "readOnly": true
                    },
                    "name": {
                      "type": "string",
                      "example": "Vacation Hours",
                      "description": "The name of the paid time off type.",
                      "readOnly": true
                    }
                  },
                  "readOnly": true
                },
                "readOnly": true
              }
            },
            "readOnly": true
          },
          "primary_signatory": {
            "type": [
              "object",
              "null"
            ],
            "description": "The primary signatory of the company.",
            "properties": {
              "uuid": {
                "type": "string",
                "readOnly": true,
                "description": "The UUID of the company's primary signatory."
              },
              "first_name": {
                "type": "string",
                "readOnly": true,
                "description": "The company's primary signatory's first name."
              },
              "middle_initial": {
                "type": [
                  "string",
                  "null"
                ],
                "readOnly": true,
                "description": "The company's primary signatory's middle initial."
              },
              "last_name": {
                "type": "string",
                "readOnly": true,
                "description": "The company's primary signatory's last name."
              },
              "phone": {
                "type": "string",
                "readOnly": true,
                "description": "The company's primary signatory's phone number."
              },
              "email": {
                "type": "string",
                "readOnly": true,
                "description": "The company's primary signatory's email address."
              },
              "home_address": {
                "type": "object",
                "properties": {
                  "street_1": {
                    "type": "string",
                    "readOnly": true
                  },
                  "street_2": {
                    "type": [
                      "string",
                      "null"
                    ],
                    "readOnly": true
                  },
                  "city": {
                    "type": "string",
                    "readOnly": true
                  },
                  "state": {
                    "type": "string",
                    "readOnly": true
                  },
                  "zip": {
                    "type": "string",
                    "readOnly": true
                  },
                  "country": {
                    "type": "string",
                    "readOnly": true
                  }
                },
                "readOnly": true,
                "description": "The company's primary signatory's home address."
              }
            },
            "readOnly": true
          },
          "primary_payroll_admin": {
            "type": "object",
            "description": "The primary payroll admin of the company.",
            "properties": {
              "first_name": {
                "type": "string",
                "readOnly": true,
                "description": "The company's primary payroll admin's first name."
              },
              "last_name": {
                "type": "string",
                "readOnly": true,
                "description": "The company's primary payroll admin's last name."
              },
              "phone": {
                "type": [
                  "string",
                  "null"
                ],
                "readOnly": true,
                "description": "The company's primary payroll admin's phone number."
              },
              "email": {
                "type": "string",
                "readOnly": true,
                "description": "The company's primary payroll admin's email address."
              }
            }
          }
        },
        "x-examples": {
          "success_status": {
            "uuid": "c7a07c73-a703-4462-9343-1b181182b6e0",
            "name": "Shoppe Studios LLC",
            "trade_name": "Record Shoppe",
            "is_partner_managed": true,
            "tier": "complete",
            "locations": [
              {
                "street_1": "412 Kiera Stravenue",
                "street_2": "Suite 391",
                "city": "San Francisco",
                "state": "CA",
                "zip": "94107",
                "country": "USA",
                "active": true
              },
              {
                "street_1": "644 Fay Vista",
                "street_2": "Suite 842",
                "city": "Richmond",
                "state": "VA",
                "zip": "23218",
                "country": "USA",
                "active": true
              }
            ],
            "ein": "00-0000001",
            "entity_type": "C-Corporation",
            "pay_schedule_type": "by_department",
            "join_date": "2024-01-15",
            "funding_type": "ach",
            "slug": "shoppe-studios-llc",
            "is_suspended": false,
            "company_status": "Approved",
            "is_high_risk_business": false,
            "is_marijuana_business": false,
            "contractor_only": false,
            "compensations": {
              "hourly": [
                {
                  "uuid": "7da6b57d-22f9-11f1-ad28-0242ac100003",
                  "name": "Overtime",
                  "multiple": 1.5
                },
                {
                  "uuid": "7da6b5ec-22f9-11f1-ad28-0242ac100003",
                  "name": "Double overtime",
                  "multiple": 2
                },
                {
                  "uuid": "7da6b22f-22f9-11f1-ad28-0242ac100003",
                  "name": "Regular",
                  "multiple": 1
                },
                {
                  "uuid": "7da6b3ac-22f9-11f1-ad28-0242ac100003",
                  "name": "Outstanding vacation",
                  "multiple": 1
                },
                {
                  "uuid": "7da6b532-22f9-11f1-ad28-0242ac100003",
                  "name": "Holiday",
                  "multiple": 1
                },
                {
                  "uuid": "7da6b44e-22f9-11f1-ad28-0242ac100003",
                  "name": "Emergency sick - self care",
                  "multiple": 1
                },
                {
                  "uuid": "7da6b49d-22f9-11f1-ad28-0242ac100003",
                  "name": "Emergency sick - caring for others",
                  "multiple": 1
                },
                {
                  "uuid": "7da6b4e6-22f9-11f1-ad28-0242ac100003",
                  "name": "FMLA Public Health Emergency Leave",
                  "multiple": 1
                }
              ],
              "fixed": [
                {
                  "uuid": "7da68d82-22f9-11f1-ad28-0242ac100003",
                  "name": "Bonus"
                },
                {
                  "uuid": "7da69024-22f9-11f1-ad28-0242ac100003",
                  "name": "Commission"
                },
                {
                  "uuid": "7da69104-22f9-11f1-ad28-0242ac100003",
                  "name": "Paycheck Tips"
                },
                {
                  "uuid": "7da6918f-22f9-11f1-ad28-0242ac100003",
                  "name": "Cash Tips"
                },
                {
                  "uuid": "7da69216-22f9-11f1-ad28-0242ac100003",
                  "name": "Correction Payment"
                },
                {
                  "uuid": "7da692a6-22f9-11f1-ad28-0242ac100003",
                  "name": "Severance"
                },
                {
                  "uuid": "7da69356-22f9-11f1-ad28-0242ac100003",
                  "name": "Minimum Wage Adjustment"
                },
                {
                  "uuid": null,
                  "name": "Reimbursement"
                }
              ],
              "paid_time_off": [
                {
                  "uuid": "7dcdcb77-22f9-11f1-ad28-0242ac100003",
                  "name": "Vacation Hours"
                },
                {
                  "uuid": "7dcdcc8b-22f9-11f1-ad28-0242ac100003",
                  "name": "Sick Hours"
                },
                {
                  "uuid": null,
                  "name": "Holiday Hours"
                }
              ]
            },
            "primary_signatory": {
              "uuid": "2d7cd96f-e2fb-4db7-8c04-99ef531b4527",
              "first_name": "Alda",
              "middle_initial": "",
              "last_name": "Carter",
              "phone": "4160000000",
              "email": "louie.hessel7757869450111547@zemlak.biz",
              "home_address": {
                "street_1": "524 Roob Divide",
                "street_2": "Suite 565",
                "city": "San Francisco",
                "state": "CA",
                "zip": "94107",
                "country": "USA"
              }
            },
            "primary_payroll_admin": {
              "first_name": "Ian",
              "last_name": "Labadie",
              "phone": "1-565-710-7559",
              "email": "louie.hessel7757869450111547@zemlak.biz"
            }
          }
        },
        "x-tags": [
          "Companies"
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
    "/v1/companies/{company_id}": {
      "get": {
        "summary": "Get a company",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get a company.\n\nThe employees:read scope is required to return home_address and non-work locations.\nThe company_admin:read scope is required to return primary_payroll_admin.\nThe signatories:read scope is required to return primary_signatory.\n\nscope: `companies:read`",
        "tags": [
          "Companies"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Company/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Company"
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
