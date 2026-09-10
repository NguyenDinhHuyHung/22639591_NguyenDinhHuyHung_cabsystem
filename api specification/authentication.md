# Authentication

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Authentication
  description: 'API module: Authentication'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Authentication
paths:
  /auth/register:
    post:
      tags:
      - Authentication
      summary: Register a new customer
      operationId: registerCustomer
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RegisterRequest'
      responses:
        '201':
          description: Customer registered successfully
        '400':
          $ref: '#/components/responses/BadRequest'
  /auth/login:
    post:
      tags:
      - Authentication
      summary: Login to CAB system
      operationId: login
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginRequest'
      responses:
        '200':
          description: Login successful
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AuthResponse'
        '401':
          $ref: '#/components/responses/Unauthorized'
components:
  responses:
    Unauthorized:
      description: Unauthorized
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
    BadRequest:
      description: Invalid input
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
  schemas:
    Error:
      type: object
      properties:
        errorCode:
          type: string
        message:
          type: string
    RegisterRequest:
      type: object
      required:
      - fullName
      - phone
      - email
      - password
      properties:
        fullName:
          type: string
        phone:
          type: string
        email:
          type: string
          format: email
        password:
          type: string
          format: password
    AuthResponse:
      type: object
      properties:
        accessToken:
          type: string
        tokenType:
          type: string
          example: Bearer
        user:
          $ref: '#/components/schemas/User'
    User:
      type: object
      properties:
        id:
          type: integer
          format: int64
        fullName:
          type: string
        email:
          type: string
          format: email
        phone:
          type: string
        role:
          type: string
          enum:
          - CUSTOMER
          - DRIVER
          - OPERATOR
          - ADMIN
    LoginRequest:
      type: object
      required:
      - email
      - password
      properties:
        email:
          type: string
          format: email
        password:
          type: string
          format: password
```
