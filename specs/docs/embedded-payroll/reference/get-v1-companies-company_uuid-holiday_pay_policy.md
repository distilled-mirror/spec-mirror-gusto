---
updatedAt: 2026-04-20T21:24:47.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get a company's holiday pay policy

Get a company's holiday pay policy

scope: `holiday_pay_policies:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Holiday Pay Policies"
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
      "Holiday-Pay-Policy": {
        "type": "object",
        "x-examples": {
          "success_status": {
            "version": "1b37938b017c7fd7116bada007072290",
            "company_uuid": "b7845189-f12b-4378-918a-d2b9de3dc4ea",
            "federal_holidays": {
              "new_years_day": {
                "selected": true,
                "name": "New Year's Day",
                "date": "January 1"
              },
              "mlk_day": {
                "selected": true,
                "name": "Martin Luther King, Jr. Day",
                "date": "Third Monday in January"
              },
              "presidents_day": {
                "selected": false,
                "name": "Presidents' Day",
                "date": "Third Monday in February"
              },
              "memorial_day": {
                "selected": true,
                "name": "Memorial Day",
                "date": "Last Monday in May"
              },
              "juneteenth": {
                "selected": false,
                "name": "Juneteenth",
                "date": "June 19"
              },
              "independence_day": {
                "selected": true,
                "name": "Independence Day",
                "date": "July 4"
              },
              "labor_day": {
                "selected": false,
                "name": "Labor Day",
                "date": "First Monday in September"
              },
              "columbus_day": {
                "selected": false,
                "name": "Columbus Day (Indigenous Peoples' Day)",
                "date": "Second Monday in October"
              },
              "veterans_day": {
                "selected": true,
                "name": "Veterans Day",
                "date": "November 11"
              },
              "thanksgiving": {
                "selected": true,
                "name": "Thanksgiving",
                "date": "Fourth Thursday in November"
              },
              "christmas_day": {
                "selected": true,
                "name": "Christmas Day",
                "date": "December 25"
              }
            },
            "employees": [
              {
                "uuid": "1ca3cd25-3eda-48c6-ac88-f0e7fb91a15a"
              }
            ]
          }
        },
        "description": "Representation of a Holiday Pay Policy",
        "properties": {
          "version": {
            "type": "string",
            "description": "The current version of the object. See the [versioning guide](https://docs.gusto.com/embedded-payroll/docs/versioning#object-layer) for information on how to use this field."
          },
          "company_uuid": {
            "type": "string",
            "description": "A unique identifier for the company owning the holiday pay policy"
          },
          "federal_holidays": {
            "type": "object",
            "description": "List of the eleven supported federal holidays and their details",
            "properties": {
              "new_years_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "mlk_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "presidents_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "memorial_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "juneteenth": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "independence_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "labor_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "columbus_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "veterans_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "thanksgiving": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              },
              "christmas_day": {
                "type": "object",
                "properties": {
                  "selected": {
                    "type": "boolean"
                  },
                  "name": {
                    "type": "string"
                  },
                  "date": {
                    "type": "string"
                  }
                }
              }
            }
          },
          "employees": {
            "type": "array",
            "description": "List of employee uuids under a holiday pay policy",
            "items": {
              "type": "object",
              "properties": {
                "uuid": {
                  "type": "string"
                }
              }
            }
          }
        },
        "required": [
          "version",
          "company_uuid",
          "federal_holidays",
          "employees"
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
    "/v1/companies/{company_uuid}/holiday_pay_policy": {
      "get": {
        "summary": "Get a company's holiday pay policy",
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
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-companies-company_uuid-holiday_pay_policy",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get a company's holiday pay policy\n\nscope: `holiday_pay_policies:read`",
        "tags": [
          "Holiday Pay Policies"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "successful",
            "content": {
              "application/json": {
                "examples": {
                  "success_status": {
                    "value": {
                      "$ref": "#/components/schemas/Holiday-Pay-Policy/x-examples/success_status"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Holiday-Pay-Policy"
                }
              }
            }
          },
          "204": {
            "description": "no policy exists"
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
