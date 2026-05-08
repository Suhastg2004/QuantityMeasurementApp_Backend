# Quantity Measurement App Backend

A Spring Boot REST API for quantity operations such as comparison, conversion, arithmetic, and operation history across multiple measurement domains.

## Features

- Compare quantities across compatible units
- Convert quantities between compatible units
- Add, subtract, and divide quantities
- Optional arithmetic with target output unit
- Operation history by operation type and measurement type
- Error history tracking (for failed operations)
- Swagger/OpenAPI documentation
- Spring Boot Actuator endpoints

## Tech Stack

- Java 17
- Spring Boot 3.2.4
- Spring Web, Spring Data JPA, Spring Security
- MySQL (primary runtime DB), H2 (optional)
- Maven (wrapper included)

## Supported Measurement Types and Units

- **LengthUnit**: `FEET`, `INCHES`, `YARDS`, `CENTIMETERS`
- **VolumeUnit**: `LITRE`, `MILLILITER`, `GALLON`
- **WeightUnit**: `GRAM`, `KILOGRAM`, `MILLIGRAM`, `POUND`, `TONNE`
- **TemperatureUnit**: `FAHRENHEIT`, `CELSIUS`

## Base API URL

`/api/v1/quantities`

## Main Endpoints

- `POST /compare`
- `POST /convert`
- `POST /add`
- `POST /add-with-target-unit`
- `POST /subtract`
- `POST /subtract-with-target-unit`
- `POST /divide`
- `GET /history/operation/{operation}`
- `GET /history/type/{type}`
- `GET /count/{operation}`
- `GET /history/errored`

## Sample Request Body

```json
{
  "thisQuantityDTO": { "value": 1.0, "unit": "FEET", "measurementType": "LengthUnit" },
  "thatQuantityDTO": { "value": 12.0, "unit": "INCHES", "measurementType": "LengthUnit" },
  "targetQuantityDTO": { "value": 0.0, "unit": "INCHES", "measurementType": "LengthUnit" }
}
```

## Prerequisites

- JDK 17+
- Maven (or use the included Maven Wrapper)
- MySQL running locally (default config uses `quantity_measurement` database)

## Configuration

Default properties are in:

- `quantitymanagementapp/src/main/resources/application.properties`
- `quantitymanagementapp/src/main/resources/application-prod.properties`

> **Important:** Update datasource credentials and URL for your environment before running in production-like mode.
## Run Locally

```bash
cd quantitymanagementapp
./mvnw spring-boot:run
```

Application starts at: `http://localhost:8080`

Windows (PowerShell/CMD):

```powershell
cd quantitymanagementapp
mvnw.cmd spring-boot:run
```

## API Docs and Monitoring

- Swagger UI: `http://localhost:8080/swagger-ui.html`
- OpenAPI JSON: `http://localhost:8080/api-docs`
- Actuator Health: `http://localhost:8080/actuator/health`
- Actuator Metrics: `http://localhost:8080/actuator/metrics`

## Run Tests

```bash
cd quantitymanagementapp
./mvnw test
```

Windows (PowerShell/CMD):

```powershell
cd quantitymanagementapp
mvnw.cmd test
```

Note: Integration tests require DB connectivity based on active datasource configuration.

## Security

Current security configuration allows all requests (`permitAll`) and enables CORS for localhost origins.
This is suitable only for local development/testing. Enable proper authentication and authorization before production deployment.

## Repository Structure

- `quantitymanagementapp/src/main/java` - application source code
- `quantitymanagementapp/src/main/resources` - runtime configuration
- `quantitymanagementapp/src/test/java` - unit and integration tests
