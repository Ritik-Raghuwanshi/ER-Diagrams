# 🛗 Smart Elevator Control System - Database Design

This project represents a **Smart Elevator Control System** database schema designed to manage elevators across campuses, buildings, and floors with features like request handling, ride assignment, status tracking, and maintenance.

---

## 📌 Overview

The system supports:

- Multi-campus infrastructure
- Hierarchical structure (Campus → Zone → Building → Floor)
- Elevator and shaft management
- Real-time elevator status tracking
- Ride request and assignment system
- Maintenance tracking
- Ride logs and analytics

---

## 🗂️ Database Entities

### 1. Campus
Represents a large area or organization.
- campus_id (PK)
- campus_name
- campus_owner_name
- campus_owner_contact

---

### 2. Zones
Subdivisions within a campus.
- zone_id (PK)
- campus_id (FK)
- zone_name
- zone_location

---

### 3. Buildings
Buildings inside zones.
- building_id (PK)
- zone_id (FK)
- building_name
- building_location

---

### 4. Elevator Shafts
Physical shafts where elevators operate.
- shaft_id (PK)
- building_id (FK)
- shaft dimensions (length, width, height)

---

### 5. Elevators
Core entity representing elevators.
- elevator_id (PK)
- shaft_id (FK)
- building_id (FK)
- floor_id (FK)
- elevator_number
- elevator_company_name
- elevator_capacity
- elevator_category (general, ownerOnly, staffOnly)

---

### 6. Floors
Represents floors in buildings.
- floor_id (PK)
- building_id (FK)
- floor_no
- floor_name
- flags (basement, skyfloor, maintenance floor)

---

### 7. Elevator Status Tracking
Tracks real-time status of elevators.
- elevator_status_tracking_id (PK)
- elevator_id (FK)
- elevator_status (parked, idle, movement, maintenance)

---

### 8. Maintenance Tracking
Records maintenance details.
- maintenance_id (PK)
- elevator_id (FK)
- maintenance_date
- maintenance_duration
- maintenance_cost
- maintenance_done_by

---

### 9. Requests
User elevator requests.
- request_id (PK)
- request_time
- request_direction (up/down)
- request_status
- request_from
- request_to
- elevator_id (FK)
- floor_id (FK)

---

### 10. Ride Assignments
Assigns elevators to requests.
- ride_assign_id (PK)
- request_id (FK)

---

### 11. Ride Logs
Stores ride history.
- ride_log_id (PK)
- ride_assign_id (FK)
- total_ride
- ride_date
- ride_duration

---

## 🔗 Relationships

```txt
1. One Campus → Many Zones
   campus.campus_id < zones.campus_id

2. One Zone → Many Buildings
   zones.zone_id < buildings.zone_id

3. One Building → Many Elevator Shafts
   buildings.building_id < elevators_shafts.building_id

4. One Shaft → Many Elevator
   elevators_shafts.shaft_id < elevators.shaft_id

5. One Building → Many Floors
   buildings.building_id < floors.building_id

6. One Elevator → One Status Records
   elevators.elevator_id - elevator_status_tracking.elevator_id

7. One Elevator → Many Maintenance Records
   elevators.elevator_id < maintenance_tracking.elevator_id

8. One Elevator → Many Requests
   elevators.elevator_id < requests.elevator_id

9. One Request → One Ride Assignment
   requests.request_id - ride_assignments.request_id

10. One Ride Assignment → One Ride Log
    ride_assignments.ride_assign_id - ride_log.ride_assign_id

11. Many Floors ↔ Many Elevators
    floors.floor_id <> elevators.floor_id

12. One Floor → Many Requests
    floors.floor_id < requests.floor_id