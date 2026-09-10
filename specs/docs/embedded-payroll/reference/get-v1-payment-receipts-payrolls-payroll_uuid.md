---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a single payroll receipt

Returns a payroll receipt.

Notes:
* Hour and dollar amounts are returned as string representations of numeric decimals.
* Dollar amounts are represented to the cent.
* If no data has yet be inserted for a given field, it defaults to "0.00" (for fixed amounts).
* Employee compensations are always paginated. Maximum page size is 100 employee compensations per request.
* Responses include the `X-Page`, `X-Total-Count`, `X-Total-Pages`, and `X-Per-Page` pagination headers.

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
      "Payroll-Receipt": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "totals": {
              "company_debit": "0.00",
              "net_pay_debit": "0.00",
              "child_support_debit": "0.00",
              "reimbursement_debit": "0.00",
              "tax_debit": "0.00"
            },
            "taxes": [],
            "employee_compensations": [],
            "licensee": {
              "name": "Gusto, Zenpayroll Inc.",
              "address": "525 20th St",
              "city": "San Francisco",
              "state": "CA",
              "postal_code": "94107",
              "phone_number": "4157778888"
            },
            "payroll_uuid": "9f624c0d-0d4f-499a-993a-846dfa47a48e",
            "company_uuid": "0481a066-e26a-465b-a2c1-933bd5b03a69",
            "name_of_sender": "Kiehn, Conroy and Prohaska",
            "name_of_recipient": "Payroll Recipients",
            "recipient_notice": "Payroll recipients include the employees listed below plus the tax agencies for the taxes listed below.",
            "debit_date": "2025-06-12",
            "license": "ZenPayroll, Inc., dba Gusto is a licensed money transmitter. For more about Gusto’s licenses and your state-specific rights to request information, submit complaints, dispute errors, or cancel transactions, visit our license page.",
            "license_uri": "https://gusto.com/about/licenses",
            "right_to_refund": "https://gusto.com/about/licenses",
            "liability_of_licensee": "https://gusto.com/about/licenses"
          }
        },
        "properties": {
          "payroll_uuid": {
            "type": "string",
            "description": "A unique identifier of the payroll receipt."
          },
          "company_uuid": {
            "type": "string",
            "description": "A unique identifier of the company for the payroll."
          },
          "name_of_sender": {
            "type": "string",
            "description": "The name of the company by whom the payroll was paid"
          },
          "name_of_recipient": {
            "type": "string",
            "description": "Always the fixed string \"Payroll Recipients\""
          },
          "recipient_notice": {
            "type": "string",
            "description": "Always the fixed string \"Payroll recipients include the employees listed below plus the tax agencies for the taxes listed below.\""
          },
          "debit_date": {
            "type": "string",
            "description": "The debit or funding date for the payroll"
          },
          "license": {
            "type": "string",
            "description": "Always the fixed string \"ZenPayroll, Inc., dba Gusto is a licensed money transmitter. For more about Gusto’s licenses and your state-specific rights to request information, submit complaints, dispute errors, or cancel transactions, visit our license page.\""
          },
          "license_uri": {
            "type": "string",
            "description": "URL for the license information for the licensed payroll processor. Always the fixed string \"https://gusto.com/about/licenses\""
          },
          "right_to_refund": {
            "type": "string",
            "description": ""
          },
          "liability_of_licensee": {
            "type": "string",
            "description": ""
          },
          "totals": {
            "type": "object",
            "description": "The subtotals for the payroll.",
            "properties": {
              "company_debit": {
                "type": "string",
                "format": "float",
                "description": "The total company debit for the payroll."
              },
              "net_pay_debit": {
                "type": "string",
                "format": "float",
                "description": "The total company net pay for the payroll."
              },
              "child_support_debit": {
                "type": "string",
                "format": "float",
                "description": "The total child support debit for the payroll."
              },
              "reimbursement_debit": {
                "type": "string",
                "format": "float",
                "description": "The total reimbursements for the payroll."
              },
              "tax_debit": {
                "type": "string",
                "format": "float",
                "description": "The total tax debit for the payroll."
              }
            }
          },
          "taxes": {
            "type": "array",
            "description": "An array of totaled employer and employee taxes for the pay period.",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "description": "The amount paid for this tax."
                },
                "amount": {
                  "type": "string",
                  "format": "float",
                  "description": "The total amount paid by both employer and employee for this tax."
                }
              }
            }
          },
          "employee_compensations": {
            "type": "array",
            "description": "An array of employee compensations and withholdings for this payroll",
            "items": {
              "type": "object",
              "properties": {
                "employee_uuid": {
                  "type": "string",
                  "description": "The UUID of the employee."
                },
                "employee_first_name": {
                  "type": "string",
                  "description": "The first name of the employee."
                },
                "employee_last_name": {
                  "type": "string",
                  "description": "The last name of the employee."
                },
                "payment_method": {
                  "type": "string",
                  "description": "The employee's compensation payment method.",
                  "enum": [
                    "Direct Deposit",
                    "Check"
                  ]
                },
                "net_pay": {
                  "type": "string",
                  "format": "float",
                  "description": "The employee's net pay. Net pay paid by check is available for reference but is not included in the `[\"totals\"][\"net_pay_debit\"]` amount."
                },
                "total_tax": {
                  "type": "string",
                  "format": "float",
                  "description": "The total of employer and employee taxes for the pay period."
                },
                "total_garnishments": {
                  "type": "string",
                  "format": "float",
                  "description": "The total garnishments for the pay period."
                },
                "child_support_garnishment": {
                  "type": "string",
                  "format": "float",
                  "description": "The total child support garnishment for the pay period."
                },
                "total_reimbursement": {
                  "type": "string",
                  "format": "float",
                  "description": "The total reimbursement for the pay period."
                }
              }
            }
          },
          "licensee": {
            "type": "object",
            "description": "The licensed payroll processor",
            "properties": {
              "name": {
                "type": "string",
                "description": "Always the fixed string \"Gusto, Zenpayroll Inc.\""
              },
              "address": {
                "type": "string",
                "description": "Always the fixed string \"525 20th St\""
              },
              "city": {
                "type": "string",
                "description": "Always the fixed string \"San Francisco\""
              },
              "state": {
                "type": "string",
                "description": "Always the fixed string \"CA\""
              },
              "postal_code": {
                "type": "string",
                "description": "Always the fixed string \"94107\""
              },
              "phone_number": {
                "type": "string",
                "description": "Always the fixed string \"4157778888\""
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
    "/v1/payrolls/{payroll_uuid}/receipt": {
      "get": {
        "summary": "Get a single payroll receipt",
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
            "name": "payroll_uuid",
            "in": "path",
            "description": "The UUID of the payroll",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-payment-receipts-payrolls-payroll_uuid",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns a payroll receipt.\n\nNotes:\n* Hour and dollar amounts are returned as string representations of numeric decimals.\n* Dollar amounts are represented to the cent.\n* If no data has yet be inserted for a given field, it defaults to \"0.00\" (for fixed amounts).\n* Employee compensations are always paginated. Maximum page size is 100 employee compensations per request.\n* Responses include the `X-Page`, `X-Total-Count`, `X-Total-Pages`, and `X-Per-Page` pagination headers.\n\nscope: `payrolls:read`",
        "tags": [
          "Payrolls"
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
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Payroll-Receipt/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Payroll-Receipt"
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
