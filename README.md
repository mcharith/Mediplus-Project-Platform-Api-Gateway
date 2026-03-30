# Api-Gateway

---

A reactive **API Gateway** built using **Spring Cloud Gateway (WebFlux)**.  
It acts as the single entry point for all client requests, routing traffic to the appropriate microservices discovered via the Service-Registry.

---

## 📖 About

The API Gateway is a critical component in the microservices architecture, responsible for handling all incoming client requests and forwarding them to the appropriate backend services.  
Instead of clients communicating directly with multiple microservices, they interact with a single unified endpoint, simplifying the system design and improving security.

Built with **Spring Cloud Gateway (WebFlux)**, this gateway supports reactive, non-blocking request handling for high performance and scalability.  
It integrates with the **Service-Registry (Eureka)** to dynamically resolve service locations using logical names, eliminating the need for hardcoded URLs.

Additionally, it fetches centralized configuration from the **Config-Server**, applies routing rules, and manages cross-cutting concerns such as CORS, logging, and monitoring.

---

## 🛠️ Tech Stack

| Technology                           | Details                          |
|--------------------------------------|----------------------------------|
| Java                                 | 25                               |
| Spring Boot                          | 4.0.3                            |
| Spring Cloud                         | 2025.1.0                         |
| Spring Cloud Gateway (WebFlux)       | Reactive API routing             |
| Spring Cloud Netflix Eureka Client   | Service discovery                |
| Spring Cloud Config Client           | Fetches config from Config-Server|
| Spring Boot Actuator                 | Health & management endpoints    |

---

## 🔀 Routing Table

All requests go through:

```
http://localhost:7001
```

The gateway forwards them to the appropriate microservice based on the route configuration.

| Route ID              | Path Prefix                | Target Service              |
|----------------------|----------------------------|-----------------------------|
| patient-service      | /api/v1/patient/**         | lb://PATIENT-SERVICE        |
| doctor-service       | /api/v1/doctor/**          | lb://DOCTOR-SERVICE         |
| appointment-service  | /api/v1/appointment/**     | lb://APPOINTMENT-SERVICE    |

---

## ⚙️ Service Details

| Property         | Value                          |
|------------------|--------------------------------|
| Port             | 7001                           |
| Artifact ID      | Api-Gateway                    |
| Group ID         | lk.ijse.eca                    |
| Config Source    | http://localhost:9100          |
| Service Registry | http://localhost:9001/eureka   |

---

## 🌐 CORS Configuration

Cross-Origin Resource Sharing (CORS) is configured globally to allow:

- All origins
- All HTTP methods
- All headers

This setup is suitable for development environments and enables seamless communication with frontend applications (e.g., React / Next.js).

---

## 🚀 Getting Started

### ⚠️ Important

Config-Server and Service-Registry must be running before starting the API Gateway, as it depends on both services for configuration and service discovery.

---

### 🔄 Startup Order

1. Config-Server (9100)
2. Service-Registry (9001)
3. API Gateway (7001)
4. Domain Services (Patient, Doctor, Appointment, etc.)

---

### ▶️ Run the Service

```bash
./mvnw spring-boot:run
```

---

### 🌐 Access the Gateway

```
http://localhost:7001
```