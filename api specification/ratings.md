# Ratings

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Ratings
  description: 'API module: Ratings'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Ratings
paths:
  /trips/{tripId}/rating:
    post:
      tags:
      - Ratings
      summary: Rate driver after trip completion
      operationId: createRating
      security:
      - bearerAuth: []
      parameters:
      - $ref: '#/components/parameters/TripId'
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RatingRequest'
      responses:
        '201':
          description: Rating created successfully
components:
  schemas:
    RatingRequest:
      type: object
      required:
      - rating
      properties:
        rating:
          type: integer
          minimum: 1
          maximum: 5
        comment:
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
