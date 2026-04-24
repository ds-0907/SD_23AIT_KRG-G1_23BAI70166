# Low Level Design

## Database Schema

### Users Table
|   Column   |    Type   |     Notes    |
|------------|-----------|--------------|
| user_id    | UUID (PK) | Unique ID    |
| name       | VARCHAR   |              |
| phone      | VARCHAR   |              |
| role       | ENUM      | rider/driver |
| rating     | FLOAT     |              |
| created_at | TIMESTAMP |              |

---

### Drivers Table
|    Column    |   Type    |         Notes          |
|--------------|-----------|------------------------|
| driver_id    | UUID (PK) |                        |
| status       | ENUM      | available/busy/offline |
| current_lat  | DOUBLE    |                        |
| current_lng  | DOUBLE    |                        |
| last_updated | TIMESTAMP |                        |

---

### Rides Table
|   Column   |    Type   |       Notes        |
|------------|-----------|--------------------|
| ride_id    | UUID (PK) |                    |
| rider_id   | UUID (FK) |                    |
| driver_id  | UUID (FK) |                    |
| pickup_lat | DOUBLE    |                    |
| pickup_lng | DOUBLE    |                    |
| drop_lat   | DOUBLE    |                    |
| drop_lng   | DOUBLE    |                    |
| status     | ENUM      |                    |
| fare       | DECIMAL   |                    |
| version    | INT       | Optimistic locking |
| created_at | TIMESTAMP |                    |

---

## Class Design / Entities

### Driver
- id
- location
- status

Methods:
- updateLocation(lat, lng)
- setStatus(status)

---

### Rider
- id

Methods:
- requestRide(pickup, drop)

---

### Ride
- id
- rider
- driver
- status

Methods:
- assignDriver()
- startRide()
- completeRide()
- cancelRide()

---

### MatchingService
Methods:
- findNearbyDrivers(location)
- rankDrivers()
- assignDriver()

---

## Concurrency Handling

- Use **optimistic locking (version field)** in Rides table
- Prevent multiple drivers being assigned

---

## Geo Indexing

- Use Redis GEOHASH
- Partition by region for scalability
