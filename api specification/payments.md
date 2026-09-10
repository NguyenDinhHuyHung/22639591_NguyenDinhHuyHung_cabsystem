# Payments

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Payments
  description: 'API module: Payments'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Payments
paths:
  /payments:
    post:
      tags:
      - Payments
      summary: Create payment for completed trip
      operationId: createPayment
      security:
      - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/PaymentRequest'
      responses:
        '201':
          description: Payment created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Payment'
components:
  schemas:
    PaymentRequest:
      type: object
      required:
      - tripId
      - paymentMethod
      properties:
        tripId:
          type: integer
        paymentMethod:
          type: string
          enum:
          - CASH
          - ONLINE
    Payment:
      type: object
      properties:
        id:
          type: integer
        tripId:
          type: integer
        amount:
          type: number
          format: double
        paymentMethod:
          type: string
          enum:
          - CASH
          - ONLINE
        status:
          type: string
          enum:
          - PENDING
          - SUCCESS
          - FAILED
        createdAt:
          type: string
          format: date-time
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
