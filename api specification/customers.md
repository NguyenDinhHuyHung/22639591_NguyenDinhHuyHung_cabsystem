# Customers

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Customers
  description: 'API module: Customers'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Customers
paths:
  /customers:
    get:
      tags:
      - Customers
      summary: Get list of customers
      operationId: getCustomers
      security:
      - bearerAuth: []
      responses:
        '200':
          description: List of customers
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Customer'
  /customers/{customerId}:
    get:
      tags:
      - Customers
      summary: Get customer by ID
      operationId: getCustomerById
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/CustomerId'
      responses:
        '200':
          description: Customer found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Customer'
        '404':
          $ref: '#/components/responses/NotFound'
    put:
      tags:
      - Customers
      summary: Update customer profile
      operationId: updateCustomer
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/CustomerId'
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CustomerUpdateRequest'
      responses:
        '200':
          description: Customer updated successfully
components:
  schemas:
    Customer:
      type: object
      properties:
        id:
          type: integer
        fullName:
          type: string
        phone:
          type: string
        email:
          type: string
          format: email
        createdAt:
          type: string
          format: date-time
    Error:
      type: object
      properties:
        errorCode:
          type: string
        message:
          type: string
    CustomerUpdateRequest:
      type: object
      properties:
        fullName:
          type: string
        phone:
          type: string
        email:
          type: string
          format: email
  responses:
    NotFound:
      description: Resource not found
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
  parameters:
    CustomerId:
      name: customerId
      in: path
      required: true
      schema:
        type: integer
        format: int64
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
