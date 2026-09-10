# Drivers

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Drivers
  description: 'API module: Drivers'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Drivers
paths:
  /drivers:
    get:
      tags:
      - Drivers
      summary: Get list of drivers
      operationId: getDrivers
      security:
      - bearerAuth: []
      responses:
        '200':
          description: List of drivers
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Driver'
    post:
      tags:
      - Drivers
      summary: Create a new driver
      operationId: createDriver
      security:
      - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/DriverRequest'
      responses:
        '201':
          description: Driver created successfully
  /drivers/{driverId}:
    get:
      tags:
      - Drivers
      summary: Get driver by ID
      operationId: getDriverById
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/DriverId'
      responses:
        '200':
          description: Driver found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Driver'
        '404':
          $ref: '#/components/responses/NotFound'
    put:
      tags:
      - Drivers
      summary: Update driver information
      operationId: updateDriver
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/DriverId'
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/DriverRequest'
      responses:
        '200':
          description: Driver updated successfully
  /drivers/{driverId}/status:
    patch:
      tags:
      - Drivers
      summary: Update driver availability status
      operationId: updateDriverStatus
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/DriverId'
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/DriverStatusRequest'
      responses:
        '200':
          description: Driver status updated
  /drivers/{driverId}/location:
    patch:
      tags:
      - Drivers
      summary: Update driver current location
      operationId: updateDriverLocation
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/DriverId'
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Location'
      responses:
        '200':
          description: Driver location updated
components:
  parameters:
    DriverId:
      name: driverId
      in: path
      required: true
      schema:
        type: integer
        format: int64
  schemas:
    Driver:
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
        status:
          type: string
          enum:
          - ONLINE
          - OFFLINE
          - AVAILABLE
          - BUSY
        rating:
          type: number
          format: float
          example: 4.8
    DriverRequest:
      type: object
      required:
      - fullName
      - phone
      - email
      properties:
        fullName:
          type: string
        phone:
          type: string
        email:
          type: string
          format: email
    Location:
      type: object
      required:
      - latitude
      - longitude
      properties:
        latitude:
          type: number
          format: double
          example: 10.7769
        longitude:
          type: number
          format: double
          example: 106.7009
        address:
          type: string
    DriverStatusRequest:
      type: object
      required:
      - status
      properties:
        status:
          type: string
          enum:
          - ONLINE
          - OFFLINE
          - AVAILABLE
          - BUSY
    Error:
      type: object
      properties:
        errorCode:
          type: string
        message:
          type: string
  responses:
    NotFound:
      description: Resource not found
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
