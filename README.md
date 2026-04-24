# 💰 FinTrack: Advanced Distributed Financial Microservices

![FinTrack Hero Banner](/home/raven/.gemini/antigravity/brain/0e34cd78-0977-463f-ad0b-5adbc09a1bac/fintrack_hero_banner_1777060816811.png)

FinTrack is a comprehensive financial advisory platform built using a **Microservice Architecture Pattern**. It leverages the full **Spring Cloud** stack to demonstrate distributed configuration, service discovery, and fault tolerance in a high-stakes fintech environment.

## 🏗️ Service Mesh Architecture

FinTrack is composed of multiple functional and infrastructure services working in concert:

```mermaid
graph TD
    Gateway[Zuul API Gateway] --> Auth[Auth Service - OAuth2]
    Gateway --> Account[Account Service]
    Gateway --> Stats[Statistics Service]
    Gateway --> Notif[Notification Service]
    
    subgraph "Infrastructure"
    Config[Config Server]
    Registry[Eureka Registry]
    Bus[Spring Cloud Bus]
    end
    
    Account -.-> Config
    Stats -.-> Config
    Notif -.-> Config
    
    Account --> DB1[(MongoDB)]
    Stats --> DB2[(MongoDB)]
    Notif --> DB3[(MongoDB)]
```

## ⚡ Core Features & Microservices

- **Account Service**: Manages user profiles, income/expense tracking, and savings goals.
- **Statistics Service**: Real-time cash flow analytics and time-series data normalization.
- **Notification Service**: Automated reminders and backup alerts via scheduled workers.
- **Auth Service**: Secure machine-to-machine and user-to-service communication via OAuth2.

## 🔄 Distributed Data Flow

```mermaid
sequenceDiagram
    participant U as User
    participant G as Gateway
    participant A as Auth
    participant S as Stats Service
    participant D as MongoDB

    U->>G: Request Statistics
    G->>A: Validate Token
    A-->>G: Token Valid
    G->>S: GET /statistics/current
    S->>D: Query Normalized Data
    D-->>S: Data Found
    S-->>G: JSON Response
    G-->>U: Render Charts
```

## 🛠️ Infrastructure Stack

- **Service Discovery**: Netflix Eureka
- **Load Balancing**: Netflix Ribbon
- **Fault Tolerance**: Netflix Hystrix (Circuit Breaker)
- **Declarative HTTP**: Feign Clients
- **Config Management**: Spring Cloud Config
- **Tracing**: Spring Cloud Sleuth + Zipkin

## 🚀 Deployment

### Prerequisites
- Docker & Docker Compose
- Maven 3.6+
- 4GB+ RAM

### Quick Start (Production Mode)
```bash
docker-compose up -d
```

### Development Mode (Build from Source)
```bash
mvn package -DskipTests
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up
```

---
*Engineered and Maintained by Saanvi Rajput. A showcase of modern distributed systems.*
