---
updatedAt: 2026-05-26T23:05:38.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get benefit fields requirements by benefit type

Returns the field requirements for a given benefit type.

scope: `benefits:read`

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
      "Benefit-Type-Requirements": {
        "description": "",
        "type": "object",
        "x-tags": [
          "Company Benefits"
        ],
        "properties": {
          "employee_deduction": {
            "type": "object",
            "description": "The amount to be deducted, per pay period, from the employee's pay.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          },
          "contribution": {
            "type": "object",
            "description": "An object representing the type and value of the company contribution.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          },
          "deduct_as_percentage": {
            "type": "object",
            "description": "Whether the employee deduction amount should be treated as a percentage to be deducted from each payroll.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          },
          "catch_up": {
            "type": "object",
            "description": "Whether the employee should use a benefit’s 'catch up' rate. Only Roth 401k and 401k benefits use this value for employees over 50.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          },
          "limit_option": {
            "type": "object",
            "description": "Some benefits require additional information to determine their limit. For example, for an HSA benefit, the limit option should be either 'Family' or 'Individual'. For a Dependent Care FSA benefit, the limit option should be either 'Joint Filing or Single' or 'Married and Filing Separately'.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          },
          "company_contribution_annual_maximum": {
            "type": "object",
            "description": "The maximum company contribution amount per year. A null value signifies no limit.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          },
          "coverage_salary_multiplier": {
            "type": "object",
            "description": "The coverage amount as a multiple of the employee's salary. Only applicable for Group Term Life benefits. Note: cannot be set if coverage amount is also set.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          },
          "coverage_amount": {
            "type": "object",
            "description": "The amount that the employee is insured for. Note: company contribution cannot be present if coverage amount is set.",
            "properties": {
              "required": {
                "type": "boolean"
              },
              "editable": {
                "type": "boolean"
              },
              "default_value": {
                "type": [
                  "object",
                  "null"
                ],
                "properties": {
                  "value": {
                    "type": "string"
                  },
                  "type": {
                    "type": "string"
                  }
                }
              },
              "choices": {
                "type": [
                  "array",
                  "null"
                ],
                "items": {
                  "type": "string"
                }
              }
            }
          }
        },
        "x-examples": {
          "Example": {
            "employee_deduction": {
              "required": true,
              "editable": true,
              "default_value": null,
              "choices": null
            },
            "contribution": {
              "required": true,
              "editable": true,
              "default_value": null,
              "choices": [
                "amount"
              ]
            },
            "deduct_as_percentage": {
              "required": false,
              "editable": false,
              "default_value": null,
              "choices": null
            },
            "catch_up": {
              "required": false,
              "editable": false,
              "default_value": null,
              "choices": null
            },
            "limit_option": {
              "required": false,
              "editable": false,
              "default_value": null,
              "choices": null
            },
            "company_contribution_annual_maximum": {
              "required": false,
              "editable": false,
              "default_value": null,
              "choices": null
            },
            "coverage_salary_multiplier": {
              "required": false,
              "editable": false,
              "default_value": null,
              "choices": null
            },
            "coverage_amount": {
              "required": false,
              "editable": false,
              "default_value": null,
              "choices": null
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
    "/v1/benefits/{benefit_id}/requirements": {
      "get": {
        "summary": "Get benefit fields requirements by benefit type",
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
            "name": "benefit_id",
            "in": "path",
            "description": "The benefit type in Gusto.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-benefits-benefits_id-requirements",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Returns the field requirements for a given benefit type.\n\nscope: `benefits:read`",
        "tags": [
          "Company Benefits"
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
                  "Example": {
                    "value": {
                      "$ref": "#/components/schemas/Benefit-Type-Requirements/x-examples/Example"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Benefit-Type-Requirements"
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
