# Bookings

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Bookings
  description: 'API module: Bookings'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Bookings
paths:
  /bookings:
    post:
      tags:
      - Bookings
      summary: Create a new ride booking
      operationId: createBooking
      security:
      - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/BookingRequest'
      responses:
        '201':
          description: Booking created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Trip'
  /bookings/{bookingId}:
    get:
      tags:
      - Bookings
      summary: Get booking information
      operationId: getBookingById
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/BookingId'
      responses:
        '200':
          description: Booking found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Trip'
  /bookings/{bookingId}/cancel:
    patch:
      tags:
      - Bookings
      summary: Cancel booking
      operationId: cancelBooking
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/BookingId'
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CancelRequest'
      responses:
        '200':
          description: Booking cancelled successfully
components:
  schemas:
    BookingRequest:
      type: object
      required:
      - pickupLocation
      - destinationLocation
      - vehicleType
      properties:
        pickupLocation:
          $ref: '#/components/schemas/Location'
        destinationLocation:
          $ref: '#/components/schemas/Location'
        vehicleType:
          type: string
          enum:
          - MOTORBIKE
          - CAR
          - PREMIUM
        paymentMethod:
          type: string
          enum:
          - CASH
          - ONLINE
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
    Trip:
      type: object
      properties:
        id:
          type: integer
        customerId:
          type: integer
        driverId:
          type: integer
          nullable: true
        vehicleId:
          type: integer
          nullable: true
        pickupLocation:
          $ref: '#/components/schemas/Location'
        destinationLocation:
          $ref: '#/components/schemas/Location'
        status:
          type: string
          enum:
          - REQUESTED
          - SEARCHING_DRIVER
          - DRIVER_ASSIGNED
          - DRIVER_ARRIVING
          - DRIVER_ARRIVED
          - PASSENGER_PICKED_UP
          - IN_PROGRESS
          - COMPLETED
          - CANCELLED
        estimatedFare:
          type: number
          format: double
        createdAt:
          type: string
          format: date-time
    CancelRequest:
      type: object
      properties:
        reason:
          type: string
  parameters:
    BookingId:
      name: bookingId
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
