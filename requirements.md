# Requirements

## Functional Requirements

### Rider Features
- Request a ride with pickup & drop location
- View nearby available drivers in real time
- Track assigned driver location live
- Cancel ride
- View ride history

### Driver Features
- Go online/offline
- Continuously update location (every 2–5 seconds)
- Accept/reject ride requests
- Navigate to pickup/drop location

### System Features
- Match rider with nearest available driver
- Provide ETA and estimated fare
- Maintain ride lifecycle:
  REQUESTED → SEARCHING → ASSIGNED → STARTED → COMPLETED / CANCELLED
- Handle concurrent ride requests efficiently
- Notify users in real time (driver assigned, arrival, trip start/end)

---

## Non-Functional Requirements

### Performance
- Location update latency < 100ms
- Nearby driver query < 200ms
- Ride matching < 500ms

### Scalability
- Support millions of drivers and riders
- Handle high write throughput (location updates every few seconds)

### Availability
- 99.99% uptime
- Graceful degradation under heavy load

### Consistency
- Eventual consistency acceptable for location data
- Strong consistency required for ride assignment

### Reliability
- No duplicate ride assignments
- Fault-tolerant system with retries

### Security
- Authentication (JWT/OAuth)
- Secure APIs (HTTPS)

### Observability
- Logging, metrics, tracing
