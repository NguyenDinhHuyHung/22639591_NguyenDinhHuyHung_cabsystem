# Trips

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Trips
  description: 'API module: Trips'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Trips
paths:
  /trips:
    get:
      tags:
      - Trips
      summary: Get list of trips
      operationId: getTrips
      security:
      - bearerAuth: []
      responses:
        '200':
          description: List of trips
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Trip'
  /trips/{tripId}:
    get:
      tags:
      - Trips
      summary: Get trip details
      operationId: getTripById
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/TripId'
      responses:
        '200':
          description: Trip found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Trip'
  /trips/{tripId}/accept:
    patch:
      tags:
      - Trips
      summary: Driver accepts trip request
      operationId: acceptTrip
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/TripId'
      responses:
        '200':
          description: Trip accepted successfully
  /trips/{tripId}/reject:
    patch:
      tags:
      - Trips
      summary: Driver rejects trip request
      operationId: rejectTrip
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/TripId'
      responses:
        '200':
          description: Trip rejected
  /trips/{tripId}/status:
    patch:
      tags:
      - Trips
      summary: Update trip status
      operationId: updateTripStatus
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/TripId'
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/TripStatusRequest'
      responses:
        '200':
          description: Trip status updated successfully
components:
  schemas:
    TripStatusRequest:
      type: object
      required:
      - status
      properties:
        status:
          type: string
          enum:
          - DRIVER_ARRIVING
          - DRIVER_ARRIVED
          - PASSENGER_PICKED_UP
          - IN_PROGRESS
          - COMPLETED
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
  parameters:
    TripId:
      name: tripId
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
