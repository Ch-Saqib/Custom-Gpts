# GPT Action Library: Getting Started with Weather.gov

## Introduction

This guide provides instructions for developers building a GPT Action specifically for accessing weather information via Weather.gov. Before you proceed, familiarize yourself with the following foundational topics:

- [Introduction to GPT Actions](#)
- [Introduction to GPT Actions Library](#)
- [Building a GPT Action from Scratch](#)

This particular GPT Action demonstrates how to connect to Weather.gov’s weather forecast service. The Action accepts a user’s question about a specific location, retrieves latitude and longitude coordinates, and then converts these into a weather forecast using the Weather Forecast Office (WFO), x, and y coordinates.

> **Note**: This is a public API and does not require authentication, so set up with `Authentication: None`.

---

## Value & Example Business Use Cases

### Value
Integrating this GPT Action allows users to leverage ChatGPT's natural language processing capabilities to easily access and interpret weather forecasts.

### Example Use Cases
1. **Daily Planning**: Users can plan their day by checking weather patterns.
2. **Visualization**: Users can visualize (e.g., through graphs) upcoming weather conditions to make informed decisions.

---

## Application Information

### Key Links

Explore these resources for more detailed information:

- [Application Website](https://www.weather.gov/)
- [Application API Documentation](https://www.weather.gov/documentation/services-web-api)

---

## ChatGPT Steps

### Custom GPT Instructions

After creating a Custom GPT, use the following instructions in the Instructions panel. For more details on getting started, refer to the [Getting Started Example](#).

```python 
**Context**: A user needs information related to a weather forecast of a specific location.

**Instructions**:
1. The user will provide a lat-long point or a general location or landmark (e.g. New York City, the White House). If the user does not provide one, ask for the relevant location
2. If the user provides a general location or landmark, convert that into a lat-long coordinate. If required, browse the web to look up the lat-long point. 
3. Run the "getPointData" API action and retrieve back the gridId, gridX, and gridY parameters.
4. Apply those variables as the office, gridX, and gridY variables in the "getGridpointForecast" API action to retrieve back a forecast
5. Use that forecast to answer the user's question 

**Additional Notes**: 
- Assume the user uses US weather units (e.g. Farenheit) unless otherwise specified
- If the user says "Let's get started" or "What do I do?", explain the purpose of this Custom GPT
-  If User Ask  About  Irrelevant Question Then  Say I  Only Know About Weather
-  Don't   Answer Irrelevant Questions

```


## OpenAPI Schema

### Once you've created a Custom GPT, copy the text below in the Actions panel. Have questions? Check out Getting Started Example to see how this step works in more detail.

```python
openapi: 3.1.0
info:
  title: NWS Weather API
  description: Access to weather data including forecasts, alerts, and observations.
  version: 1.0.0
servers:
  - url: https://api.weather.gov
    description: Main API Server
paths:
  /points/{latitude},{longitude}:
    get:
      operationId: getPointData
      summary: Get forecast grid endpoints for a specific location
      parameters:
        - name: latitude
          in: path
          required: true
          schema:
            type: number
            format: float
          description: Latitude of the point
        - name: longitude
          in: path
          required: true
          schema:
            type: number
            format: float
          description: Longitude of the point
      responses:
        '200':
          description: Successfully retrieved grid endpoints
          content:
            application/json:
              schema:
                type: object
                properties:
                  properties:
                    type: object
                    properties:
                      forecast:
                        type: string
                        format: uri
                      forecastHourly:
                        type: string
                        format: uri
                      forecastGridData:
                        type: string
                        format: uri

  /gridpoints/{office}/{gridX},{gridY}/forecast:
    get:
      operationId: getGridpointForecast
      summary: Get forecast for a given grid point
      parameters:
        - name: office
          in: path
          required: true
          schema:
            type: string
          description: Weather Forecast Office ID
        - name: gridX
          in: path
          required: true
          schema:
            type: integer
          description: X coordinate of the grid
        - name: gridY
          in: path
          required: true
          schema:
            type: integer
          description: Y coordinate of the grid
      responses:
        '200':
          description: Successfully retrieved gridpoint forecast
          content:
            application/json:
              schema:
                type: object
                properties:
                  properties:
                    type: object
                    properties:
                      periods:
                        type: array
                        items:
                          type: object
                          properties:
                            number:
                              type: integer
                            name:
                              type: string
                            startTime:
                              type: string
                              format: date-time
                            endTime:
                              type: string
                              format: date-time
                            temperature:
                              type: integer
                            temperatureUnit:
                              type: string
                            windSpeed:
                              type: string
                            windDirection:
                              type: string
                            icon:
                              type: string
                              format: uri
                            shortForecast:
                              type: string
                            detailedForecast:
                              type: string
```


## FAQ & Troubleshooting

### Are there integrations that you’d like us to prioritize? Are there errors in our integrations? File a PR or issue in our github, and we’ll take a look.


---

This README provides a foundation for building and deploying a GPT Action for Weather.gov. Happy coding!
