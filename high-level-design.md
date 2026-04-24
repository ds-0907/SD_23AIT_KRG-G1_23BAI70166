# High Level Design

## System Architecture Diagram
![Architecture](<img width="7498" height="4816" alt="System Architecture Diagram" src="https://github.com/user-attachments/assets/ef8383c1-7375-4685-8d8d-e9e9c39ecc2a" />)

## End-to-End Ride Flow

![Sequence](<img width="8192" height="4742" alt="Sequence Diagram" src="https://github.com/user-attachments/assets/9ac4ac4b-d3db-461a-98d1-c5ec9a432139" />)

---

## Components

### 1. API Gateway
- Entry point for all clients
- Handles:
  - Authentication
  - Rate limiting
  - Routing to services

---

### 2. User Service
- Manages riders and drivers
- Stores profile, rating, and identity data

---

### 3. Ride Service (Core Business Logic)
- Manages ride lifecycle
- Handles:
  - Ride creation
  - Driver assignment
  - Status transitions

---

### 4. Location Service (High Throughput)
- Ingests driver location updates
- Publishes events to Kafka
- Updates geo-index

---

### 5. Kafka (Event Streaming)
- Buffers high-frequency updates
- Decouples ingestion from processing
- Ensures scalability

---

### 6. Redis (Geo Index)
- Stores real-time driver locations
- Supports GEO queries (radius search)
- Used for low-latency reads

---

### 7. Database (Primary Storage)
- Stores:
  - Users
  - Rides
  - Historical data
- Typically PostgreSQL / Cassandra

---

### 8. Notification Service
- Push notifications / WebSockets
- Real-time updates for:
  - Driver assignment
  - Ride status

---

## Key Design Decisions

- Separate **read-heavy (Redis)** and **write-heavy (Kafka)** paths
- Use **event-driven architecture** for scalability
- Keep services **stateless** for horizontal scaling
