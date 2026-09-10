---
updatedAt: 2026-05-26T23:06:49.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Get all contractor documents

Get a list of all contractor's documents

scope: `contractor_documents:read`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Contractor Documents"
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
      "Document": {
        "title": "Document",
        "type": "object",
        "properties": {
          "uuid": {
            "type": "string",
            "description": "The UUID of the document",
            "readOnly": true
          },
          "title": {
            "type": "string",
            "description": "The title of the document",
            "readOnly": true
          },
          "name": {
            "type": "string",
            "description": "The type identifier of the document",
            "readOnly": true
          },
          "recipient_type": {
            "type": "string",
            "description": "The type of recipient associated with the document (will be `Contractor` for Contractor Documents)",
            "enum": [
              "Company",
              "Employee",
              "Contractor"
            ],
            "readOnly": true
          },
          "recipient_uuid": {
            "type": "string",
            "description": "Unique identifier for the recipient associated with the document",
            "readOnly": true
          },
          "pages": {
            "type": "array",
            "description": "List of the document's pages and associated image URLs. This is only returned for documents with `required_signing` = `true`, and can be used for signing preparation.",
            "items": {
              "type": "object",
              "properties": {
                "image_url": {
                  "type": "string",
                  "description": "Image URL for the page"
                },
                "page_number": {
                  "type": "integer",
                  "description": "Page number"
                }
              }
            },
            "readOnly": true
          },
          "fields": {
            "type": "array",
            "description": "List of the document's fields and associated data. Values are set for auto-filled fields. This is only returned for documents with `required_signing` = `true`, and can be used for signing preparation.",
            "items": {
              "type": "object",
              "properties": {
                "key": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "Unique identifier of the field. May be null for custom fields that do not correspond to a known Gusto-managed key mapping."
                },
                "value": {
                  "type": [
                    "string",
                    "null"
                  ],
                  "description": "Auto-filled value of the field"
                },
                "x": {
                  "type": [
                    "integer",
                    "null"
                  ],
                  "description": "X-coordinate location of the field on the page. May be null when the field has no positioning information."
                },
                "y": {
                  "type": [
                    "integer",
                    "null"
                  ],
                  "description": "Y-coordinate location of the field on the page. May be null when the field has no positioning information."
                },
                "width": {
                  "type": [
                    "integer",
                    "null"
                  ],
                  "description": "Width of the field. May be null when the field has no positioning information."
                },
                "height": {
                  "type": [
                    "integer",
                    "null"
                  ],
                  "description": "Height of the field. May be null when the field has no positioning information."
                },
                "page_number": {
                  "type": [
                    "integer",
                    "null"
                  ],
                  "description": "Page number of the field. May be null when the field has no positioning information."
                },
                "data_type": {
                  "type": "string",
                  "description": "The field's data type"
                },
                "required": {
                  "type": "boolean",
                  "description": "Whether the field is required"
                }
              }
            },
            "readOnly": true
          },
          "signed_at": {
            "type": [
              "string",
              "null"
            ],
            "description": "When the document was signed (will be `null` if unsigned)",
            "readOnly": true
          },
          "description": {
            "type": "string",
            "description": "The description of the document",
            "readOnly": true
          },
          "requires_signing": {
            "type": "boolean",
            "description": "A boolean flag that indicates whether the document needs signing or not. Note that this value will change after the document is signed."
          },
          "draft": {
            "type": "boolean",
            "description": "If the document is in a draft state",
            "readOnly": true
          },
          "year": {
            "type": [
              "integer",
              "null"
            ],
            "description": "The year of this document. This value is nullable and will not be present on all documents.",
            "readOnly": true
          },
          "quarter": {
            "type": [
              "integer",
              "null"
            ],
            "description": "The quarter of this document. This value is nullable and will not be present on all documents.",
            "readOnly": true
          }
        },
        "x-examples": {
          "Example": {
            "uuid": "e83b3c20-dc4f-4382-bee3-b478fc42c68b",
            "title": "Taxpayer Identification (Form W-9)",
            "name": "taxpayer_identification_form_w_9",
            "recipient_type": "Contractor",
            "recipient_uuid": "f079c253-29e2-45e2-b384-2cc615c9c568",
            "pages": [
              {
                "image_url": "http://app.gusto-dev.com:3000/assets/document_templates/20/unmapped_template/images/0.jpg",
                "page_number": 0
              },
              {
                "image_url": "http://app.gusto-dev.com:3000/assets/document_templates/20/unmapped_template/images/1.jpg",
                "page_number": 1
              }
            ],
            "fields": [
              {
                "key": "text1596141656513",
                "value": null,
                "x": 69,
                "y": 94,
                "width": 261,
                "height": 13,
                "page_number": 0,
                "data_type": "text",
                "required": true
              },
              {
                "key": "optional_text1596141704672",
                "value": null,
                "x": 69,
                "y": 118,
                "width": 262,
                "height": 13,
                "page_number": 0,
                "data_type": "text",
                "required": false
              }
            ],
            "signed_at": null,
            "description": "Form W-9, Request for Taxpayer Identification Number and Certification",
            "requires_signing": true,
            "draft": false,
            "year": null,
            "quarter": null
          }
        },
        "x-tags": [
          "Documents"
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
    "/v1/contractors/{contractor_uuid}/documents": {
      "get": {
        "summary": "Get all contractor documents",
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
            "name": "contractor_uuid",
            "in": "path",
            "description": "The UUID of the contractor",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "x-gusto-rswag": true,
        "operationId": "get-v1-contractor-documents",
        "security": [
          {
            "CompanyAccessAuth": []
          }
        ],
        "description": "Get a list of all contractor's documents\n\nscope: `contractor_documents:read`",
        "tags": [
          "Contractor Documents"
        ],
        "x-gusto-integration-type": [
          "embedded"
        ],
        "responses": {
          "200": {
            "description": "Example response",
            "content": {
              "application/json": {
                "examples": {
                  "Example": {
                    "value": [
                      {
                        "$ref": "#/components/schemas/Document/x-examples/Example"
                      }
                    ]
                  }
                },
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Document"
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
