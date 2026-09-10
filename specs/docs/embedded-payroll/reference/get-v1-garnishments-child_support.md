---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get child support garnishment data

Agency data and requirements to be used for creating child support garnishments

scope: `garnishments:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Garnishments"
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
      "Child-Support-Data": {
        "description": "Child Support agency data",
        "type": "object",
        "properties": {
          "agencies": {
            "type": "array",
            "description": "State child support agencies",
            "items": {
              "type": "object",
              "properties": {
                "state": {
                  "type": "string",
                  "description": "Two letter state abbreviation"
                },
                "name": {
                  "type": "string",
                  "description": "Name of state child support agency"
                },
                "manual_payment_required": {
                  "type": "boolean",
                  "description": "Specifies if remitting payment to the agency is required outside of Gusto. If true, Gusto includes garnishment amounts for this agency in payroll calculation, but does not debit for or remit payment to the agency automatically. As of September 2024, only garnishments for South Carolina Integrated Child Support Services require manual payment. "
                },
                "fips_codes": {
                  "type": "array",
                  "description": "FIPS codes for state or county child support orders",
                  "items": {
                    "type": "object",
                    "properties": {
                      "code": {
                        "type": "string",
                        "description": "FIPS code for state or county"
                      },
                      "county": {
                        "type": [
                          "string",
                          "null"
                        ],
                        "description": "Name of county in the state for the corresponding FIPS code. When `null` the FIPS code applies state wide."
                      }
                    }
                  }
                },
                "required_attributes": {
                  "type": "array",
                  "description": "Describes which child support case identifying attributes are required for this agency. While most agencies only require a single identifier, some (e.g. OH) require multiple identifiers.",
                  "items": {
                    "type": "object",
                    "properties": {
                      "key": {
                        "type": "string",
                        "description": "A required attribute when creating a garnishment for this state agency. The current values are listed as an enum; though unlikely, values could be added if state agency requirements change in the future.",
                        "enum": [
                          "case_number",
                          "order_number",
                          "remittance_number"
                        ]
                      },
                      "label": {
                        "type": "string",
                        "description": "A human readable name of the attribute, e.g. CSE Case Number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "x-examples": {
          "Example": {
            "agencies": [
              {
                "state": "AK",
                "name": "Alaska Child Support Services Division",
                "manual_payment_required": false,
                "fips_codes": [
                  {
                    "county": null,
                    "code": "0200000"
                  }
                ],
                "required_attributes": [
                  {
                    "key": "case_number",
                    "label": "CSE Case Number"
                  }
                ]
              },
              {
                "state": "OH",
                "name": "Ohio Office of Child Support Enforcement",
                "manual_payment_required": false,
                "fips_codes": [
                  {
                    "county": null,
                    "code": "39000"
                  }
                ],
                "required_attributes": [
                  {
                    "key": "case_number",
                    "label": "CSE Case Number"
                  },
                  {
                    "key": "order_number",
                    "label": "Order Identifier"
                  }
                ]
              }
            ]
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
    "/v1/garnishments/child_support": {
      "get": {
        "summary": "Get child support garnishment data",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-garnishments-child_support",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Agency data and requirements to be used for creating child support garnishments\n\nscope: `garnishments:read`",
        "tags": [
          "Garnishments"
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
                      "$ref": "#/components/schemas/Child-Support-Data/x-examples/Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Child-Support-Data"
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
