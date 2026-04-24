# API Design

## 1. Request Ride

POST /rides

Request:
{
  "rider_id": "123",
  "pickup": { "lat": 30.7, "lng": 76.7 },
  "drop": { "lat": 30.75, "lng": 76.8 }
}

Response:
{
  "ride_id": "r123",
  "status": "SEARCHING"
}

---

## 2. Update Driver Location

POST /drivers/location

Request:
{
  "driver_id": "d123",
  "lat": 30.72,
  "lng": 76.77
}

Response:
{
  "status": "updated"
}

---

## 3. Get Nearby Drivers

GET /drivers/nearby?lat=30.7&lng=76.7&radius=3

Response:
{
  "drivers": [
    {
      "driver_id": "d1",
      "lat": 30.71,
      "lng": 76.72,
      "distance": 1.2,
      "eta": 3
    }
  ]
}

---

## 4. Accept Ride

POST /rides/{ride_id}/accept

Request:
{
  "driver_id": "d123"
}

Response:
{
  "status": "ASSIGNED"
}

---

## 5. Track Ride

GET /rides/{ride_id}/location

Response:
{
  "driver_location": {
    "lat": 30.72,
    "lng": 76.77
  }
}

---

## Status Codes

- 200 OK → Success
- 201 Created → Resource created
- 400 Bad Request → Invalid input
- 401 Unauthorized → Auth failure
- 404 Not Found → Resource missing
- 409 Conflict → Race condition (multiple drivers)
- 500 Internal Server Error
