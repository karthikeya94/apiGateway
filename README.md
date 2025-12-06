# API Gateway Service

## Overview
The **API Gateway Service** acts as the single entry point for all microservices in the ecosystem. It provides a unified interface for clients, handling routing, load balancing, and service discovery integration. Built with **Spring Cloud Gateway**, it dynamically routes requests to the appropriate backend services registered with the Eureka Server.

## Features
- **Centralized Entry Point**: All external requests go through the gateway, simplifying the client-side logic.
- **Dynamic Routing**: Automatically routes requests to microservices based on service IDs registered in Eureka.
- **Service Discovery Integration**: Seamlessly integrates with **Eureka Server** to discover available service instances.
- **Load Balancing**: Distributes traffic across multiple instances of a service using client-side load balancing.
- **Path Rewriting**: Automatically strips prefixes (e.g., `/api/compliance`) before forwarding requests to the downstream services.

## Tech Stack
- **Java 17**
- **Spring Boot 3.5.7**
- **Spring Cloud Gateway**
- **Spring Cloud Netflix Eureka Client**
- **Maven**

## Configuration
The service is configured in `application.yml`. Key configurations include:

- **Server Port**: `8082`
- **Application Name**: `api-gateway`
- **Eureka Server URL**: `http://localhost:8761/eureka/`

### Routing Rules
The gateway is configured with the following routes:

| Service Name | Path Predicate | Target Service ID |
| :--- | :--- | :--- |
| **Compliance Service** | `/api/compliance/**` | `compliance-regulatory-service` |
| **Fraud Detection Service** | `/api/fraud/**` | `fraud-detection-service` |
| **Notification Service** | `/api/notification/**` | `notification-service` |
| **Risk Scoring Service** | `/api/risk/**` | `risk-scoring-service` |
| **Transaction Ingestion** | `/api/ingestion/**` | `transaction-ingestion-service` |
| **Transaction Orchestration** | `/api/orchestration/**` | `transaction-orchestration-service` |

*Note: The gateway strips the first 2 path segments (e.g., `/api/compliance`) before forwarding the request.*

## Getting Started

### Prerequisites
- Java 17 or higher
- Maven
- **Eureka Server** must be running on port `8761`.

### Installation
1. Clone the repository.
2. Navigate to the `api-gateway` directory.

### Running the Service
You can run the service using Maven:

```bash
mvn spring-boot:run
```

Or build the JAR and run it:

```bash
mvn clean package
java -jar target/api-gateway-0.0.1-SNAPSHOT.jar
```

The service will start on **http://localhost:8082**.

## Usage
Once the gateway and all microservices are running, you can access them via the gateway URL:

- **Compliance**: `http://localhost:8082/api/compliance/...`
- **Fraud**: `http://localhost:8082/api/fraud/...`
- **Notification**: `http://localhost:8082/api/notification/...`
- **Risk**: `http://localhost:8082/api/risk/...`
- **Ingestion**: `http://localhost:8082/api/ingestion/...`
- **Orchestration**: `http://localhost:8082/api/orchestration/...`

## Health Check
You can check the status of the gateway and its connection to Eureka by accessing the actuator endpoints (if enabled) or checking the logs for successful registration with the Eureka Server.
