# 🍕 food-delivery-backend

> Real-time food delivery REST API with order tracking, restaurant management, and delivery agent assignment.

[![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.2-6DB33F?style=flat-square&logo=springboot)](https://spring.io/projects/spring-boot)
[![WebSocket](https://img.shields.io/badge/WebSocket-STOMP-FF6B35?style=flat-square)](https://stomp.github.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql)](https://postgresql.org)

**Features:** Restaurant catalog · Menu management · Real-time order tracking via WebSocket · Delivery agent assignment · Push notifications · Payment integration · Order history

**Key Endpoints:**
```
POST   /api/v1/orders                    # Place order
GET    /api/v1/orders/{id}/track         # Track order (WebSocket)
GET    /api/v1/restaurants               # List restaurants
GET    /api/v1/restaurants/{id}/menu     # Get restaurant menu
POST   /api/v1/restaurants/{id}/reviews  # Submit review
GET    /api/v1/delivery/agent/active     # Active deliveries [AGENT]
PUT    /api/v1/delivery/{id}/status      # Update delivery status [AGENT]
```

**Folder Structure:**
```
food-delivery-backend/
├── src/main/java/com/blackrootbit/fooddelivery/
│   ├── controller/       # REST + WebSocket controllers
│   ├── service/          # Business logic layer
│   ├── model/            # JPA entities
│   ├── repository/       # Spring Data JPA
│   ├── websocket/        # STOMP message handlers
│   ├── security/         # JWT auth
│   └── config/           # App configuration
├── docker/
│   └── docker-compose.yml
└── .github/workflows/ci.yml
```

**GitHub Topics:** `java` `spring-boot` `food-delivery` `websocket` `rest-api` `postgresql` `docker` `jwt` `real-time`

---

# 🏦 banking-system-api

> Secure core banking API with account management, fund transfers, transaction history, and fraud detection hooks.

[![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.2-6DB33F?style=flat-square&logo=springboot)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql)](https://postgresql.org)
[![AWS](https://img.shields.io/badge/AWS-Deployed-FF9900?style=flat-square&logo=amazonaws)](https://aws.amazon.com)

**Features:** Account creation & management · Fund transfers (internal & external) · Transaction history with pagination · Balance inquiry · Scheduled payments · Interest calculation · Fraud detection hooks · Full audit trail

**Key Endpoints:**
```
POST  /api/v1/accounts                          # Open account
GET   /api/v1/accounts/{id}/balance             # Get balance
POST  /api/v1/transactions/transfer             # Fund transfer
GET   /api/v1/transactions/history              # Transaction history
POST  /api/v1/transactions/deposit              # Deposit funds
POST  /api/v1/transactions/withdraw             # Withdraw funds
GET   /api/v1/accounts/{id}/statement           # Account statement (PDF)
```

**Database Schema Highlights:**
```sql
CREATE TABLE accounts (
    id              BIGSERIAL PRIMARY KEY,
    account_number  VARCHAR(20) UNIQUE NOT NULL,
    user_id         BIGINT REFERENCES users(id),
    account_type    VARCHAR(50),     -- SAVINGS / CURRENT / FIXED
    balance         DECIMAL(15,2) DEFAULT 0.00,
    currency        VARCHAR(3) DEFAULT 'USD',
    status          VARCHAR(20) DEFAULT 'ACTIVE',
    created_at      TIMESTAMP DEFAULT NOW()
);

CREATE TABLE transactions (
    id              BIGSERIAL PRIMARY KEY,
    from_account    BIGINT REFERENCES accounts(id),
    to_account      BIGINT REFERENCES accounts(id),
    amount          DECIMAL(15,2),
    type            VARCHAR(50),     -- TRANSFER / DEPOSIT / WITHDRAWAL
    status          VARCHAR(20),     -- PENDING / COMPLETED / FAILED
    reference_id    VARCHAR(100) UNIQUE,
    created_at      TIMESTAMP DEFAULT NOW()
);
```

**GitHub Topics:** `java` `spring-boot` `banking` `fintech` `rest-api` `postgresql` `security` `docker` `aws`

---

# ⚙️ microservices-order-system

> Distributed order management system using microservices architecture with Kafka event streaming, API Gateway, and Kubernetes deployment.

[![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk)](https://openjdk.org/)
[![Spring Cloud](https://img.shields.io/badge/Spring_Cloud-6DB33F?style=flat-square&logo=spring)](https://spring.io/projects/spring-cloud)
[![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat-square&logo=apachekafka)](https://kafka.apache.org/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes)](https://kubernetes.io)

**Services:**
```
microservices-order-system/
├── api-gateway/              # Spring Cloud Gateway — routing & auth
├── order-service/            # Order CRUD, status lifecycle
├── inventory-service/        # Stock management, reservations
├── payment-service/          # Payment processing, Stripe
├── notification-service/     # Email/SMS via Kafka consumer
├── user-service/             # User management & JWT auth
├── discovery-service/        # Eureka service registry
├── config-server/            # Centralized configuration
├── k8s/                      # Kubernetes manifests
│   ├── deployments/
│   ├── services/
│   └── configmaps/
└── docker-compose.yml        # Local development
```

**Event Flow:**
```
[Client] → [API Gateway] → [Order Service]
                                │
                          Kafka: order.created
                                │
              ┌─────────────────┼─────────────────┐
              ▼                 ▼                   ▼
    [Inventory Service]  [Payment Service]  [Notification Service]
    reserve stock        process payment    send confirmation email
              │                 │
        Kafka: stock.reserved   Kafka: payment.processed
              └────────────────►[Order Service: update status]
```

**GitHub Topics:** `java` `spring-cloud` `microservices` `kafka` `kubernetes` `docker` `api-gateway` `eureka` `distributed-systems`

---
