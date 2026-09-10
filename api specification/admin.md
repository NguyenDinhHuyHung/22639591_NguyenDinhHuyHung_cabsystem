# Admin

``` yaml
openapi: 3.0.3
info:
  title: CAB - Online Ride Booking System API - Admin
  description: 'API module: Admin'
  version: 1.0.0
servers:
- url: http://localhost:8080/api/v1
  description: Local Development Server
tags:
- name: Admin
paths:
  /admin/dashboard:
    get:
      tags:
      - Admin
      summary: Get system dashboard
      operationId: getDashboard
      security:
      - bearerAuth: []
      responses:
        '200':
          description: Dashboard information
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Dashboard'
components:
  schemas:
    Dashboard:
      type: object
      properties:
        totalCustomers:
          type: integer
        totalDrivers:
          type: integer
        totalTrips:
          type: integer
        completedTrips:
          type: integer
        cancelledTrips:
          type: integer
        totalRevenue:
          type: number
          format: double
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
