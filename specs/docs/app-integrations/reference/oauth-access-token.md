---
updatedAt: 2026-04-20T21:23:13.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/app-integrations/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# Create a System Access Token or Refresh an Access Token

Creates a system access token or refreshes an oauth access token

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "tags": [
    {
      "name": "Introspection"
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
      "Create-Token-Authentication": {
        "description": "",
        "type": "object",
        "required": [
          "access_token",
          "token_type",
          "expires_in",
          "created_at"
        ],
        "properties": {
          "access_token": {
            "type": "string",
            "description": "A new access token that can be used for subsequent authenticated requests"
          },
          "token_type": {
            "type": "string",
            "default": "Bearer",
            "description": "The literal string 'Bearer'"
          },
          "expires_in": {
            "type": "number",
            "default": 7200,
            "description": "The TTL of this token. After this amount of time, you must hit the refresh token endpoint to continue making authenticated requests."
          },
          "created_at": {
            "type": "number",
            "description": "Datetime for when the new access token is created."
          },
          "refresh_token": {
            "type": [
              "string",
              "null"
            ],
            "description": "A token that must be passed to the refresh token endpoint to get a new authenticated token. Only present when refresh token is provided."
          }
        }
      },
      "Refresh-Token-Authentication": {
        "description": "",
        "type": "object",
        "allOf": [
          {
            "$ref": "#/components/schemas/Create-Token-Authentication"
          },
          {
            "type": "object",
            "properties": {
              "refresh_token": {
                "type": "string",
                "description": "A token that must be passed to the refresh token endpoint to get a new authenticated token."
              },
              "scope": {
                "type": "string",
                "description": "All of the scopes for which the access token provides access."
              }
            }
          }
        ]
      },
      "Authentication": {
        "description": "",
        "type": "object",
        "oneOf": [
          {
            "$ref": "#/components/schemas/Create-Token-Authentication"
          },
          {
            "$ref": "#/components/schemas/Refresh-Token-Authentication"
          }
        ],
        "x-examples": {
          "create_token": {
            "access_token": "As8qKfNObHbwe7abbJqF0WUF6iCQoIW2R664TFzXd-A",
            "token_type": "Bearer",
            "created_at": 1767644464,
            "expires_in": 7200,
            "refresh_token": null
          },
          "refresh_token": {
            "access_token": "As8qKfNObHbwe7abbJqF0WUF6iCQoIW2R664TFzXd-A",
            "refresh_token": "As8qKfNObHbwe7abbJqF0WUF6iCQoIW2R664TFzXd-A",
            "scope": "public payroll:read",
            "token_type": "Bearer",
            "created_at": 1767644464,
            "expires_in": 7200
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
    "/oauth/token": {
      "post": {
        "summary": "Create a System Access Token or Refresh an Access Token",
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
        "operationId": "oauth-access-token",
        "security": [],
        "description": "Creates a system access token or refreshes an oauth access token",
        "tags": [
          "Introspection"
        ],
        "x-gusto-integration-type": [
          "embedded",
          "app-integrations"
        ],
        "responses": {
          "200": {
            "description": "Success",
            "content": {
              "application/json": {
                "examples": {
                  "create_token": {
                    "value": {
                      "$ref": "#/components/schemas/Authentication/x-examples/create_token"
                    }
                  },
                  "refresh_token": {
                    "value": {
                      "$ref": "#/components/schemas/Authentication/x-examples/refresh_token"
                    }
                  }
                },
                "schema": {
                  "$ref": "#/components/schemas/Authentication"
                }
              }
            }
          }
        },
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "oneOf": [
                  {
                    "type": "object",
                    "title": "Refresh Token Request",
                    "required": [
                      "client_id",
                      "client_secret",
                      "grant_type",
                      "refresh_token"
                    ],
                    "properties": {
                      "client_id": {
                        "type": "string",
                        "description": "Your client ID",
                        "example": "qr6L_9FRkbMVL_GdwvrMW6Ef8tcU6NUxjWpOfqXqOG8"
                      },
                      "client_secret": {
                        "type": "string",
                        "description": "Your client secret",
                        "example": "3aQSHRB3596nZhm6NdNBELZ1u9xbZmvCrKpBhbZYq6w"
                      },
                      "grant_type": {
                        "type": "string",
                        "enum": [
                          "refresh_token"
                        ],
                        "description": "Set system_access to create a system access token, refresh_token to refresh an existing token"
                      },
                      "refresh_token": {
                        "type": "string",
                        "descrition": "The refresh token being exchanged for an access token code",
                        "example": "iEjL96L9Pndwmi-xVX3Q-xbrvvhnjHYGX87sopgGJ8E"
                      },
                      "redirect_uri": {
                        "type": "string",
                        "description": "The redirect URI you set up via the Developer Portal"
                      }
                    }
                  },
                  {
                    "type": "object",
                    "title": "System Access Token Request",
                    "required": [
                      "client_id",
                      "client_secret",
                      "grant_type"
                    ],
                    "properties": {
                      "client_id": {
                        "type": "string",
                        "description": "Your client ID",
                        "example": "qr6L_9FRkbMVL_GdwvrMW6Ef8tcU6NUxjWpOfqXqOG8"
                      },
                      "client_secret": {
                        "type": "string",
                        "description": "Your client secret",
                        "example": "3aQSHRB3596nZhm6NdNBELZ1u9xbZmvCrKpBhbZYq6w"
                      },
                      "grant_type": {
                        "type": "string",
                        "description": "Set system_access to create a system access token, refresh_token to refresh an existing token",
                        "enum": [
                          "system_access"
                        ]
                      }
                    }
                  }
                ]
              }
            }
          },
          "required": true
        }
      }
    }
  }
}
```
