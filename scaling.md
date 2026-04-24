# Scaling Strategy

## 1. Load Balancing

- Use L4/L7 load balancers (e.g., NGINX, AWS ALB)
- Distribute requests across multiple stateless service instances
- Auto-scale based on:
  - CPU usage
  - request rate

---

## 2. Caching Strategy

### Redis (Primary Cache)

Used for:
- Driver live locations (Geo index)
- Active ride status

### TTL Strategy
- Driver location expires in 10–30 seconds
- Prevent stale data

### Benefits
- Sub-millisecond reads
- Reduces DB load significantly

---

## 3. Database Scaling

### Read Scaling
- Use read replicas for:
  - Ride history
  - analytics queries

---

### Write Scaling

#### Sharding Strategy
- Partition by:
  - Region (geo-based)
  - ride_id hash

---

### Storage Choices
- OLTP: PostgreSQL
- High-scale writes: Cassandra (optional)

---

## 4. Kafka (Event Streaming)

- Handles millions of location updates/sec
- Decouples ingestion from processing

### Partitioning
- Partition by driver_id
- Ensures ordering per driver

---

## 5. Horizontal Scaling

- All services are stateless
- Can scale independently:
  - Location service → high write scaling
  - Ride service → compute-heavy scaling

---

## 6. Real-Time Optimization

- Use WebSockets / gRPC streaming
- Avoid polling
- Push updates to clients

---

## 7. Fault Tolerance

- Multi-AZ deployment
- Retry with exponential backoff
- Circuit breakers to prevent cascading failures
