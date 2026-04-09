# 🚗 Comic-Con Parking System - ER Design

This project represents a **Parking Management System database schema** designed to handle parking operations such as venues, parking levels, zones, spots, vehicles, sessions, tickets, and payments.

---

## 📌 Overview

The system supports:

- Multi-venue parking management
- Hierarchical parking structure (Level → Zone → Spot)
- Vehicle tracking and categorization
- Parking sessions with entry/exit tracking
- Ticket generation
- Payment handling

---

## 🗂️ Database Entities

### 1. Venues
Stores parking locations.
- venue_id (PK)
- venue_name
- venue_location

### 2. Parking Levels
Represents floors inside a venue.
- level_id (PK)
- venue_id (FK)
- level_name

### 3. Parking Zones
Subsections of levels.
- zone_id (PK)
- level_id (FK)
- zone_name

### 4. Parking Spots
Actual parking slots.
- spot_id (PK)
- zone_id (FK)
- spot_number
- is_vacant
- spot_category_id (FK)

### 5. Spot Categories
Defines type of parking spots.
- spot_category_id (PK)
- spot_category_name
- spot_charges

### 6. Vehicles
Stores vehicle information.
- vehicle_id (PK)
- vehicle_number
- vehicle_color
- category_id (FK)

### 7. Vehicle Categories
Defines vehicle types.
- category_id (PK)
- category_name

### 8. Parking Sessions
Tracks parking activity.
- parking_session_id (PK)
- vehicle_id (FK)
- spot_id (FK)
- entry_time
- exit_time
- parking_charges

### 9. Parking Tickets
Generated for each session.
- ticket_id (PK)
- vehicle_id (FK)
- parking_session_id (FK)

### 10. Payment Records
Handles payment details.
- payment_id (PK)
- parking_session_id (FK)
- payment_status
- payment_mode
- payment_amount

---

## 🔗 Relationships


1. One Venue → Many Parking Levels
   venues.venue_id < parking_level.venue_id

2. One Parking Level → Many Parking Zones
   parking_level.level_id < parking_zone.level_id

3. One Parking Zone → Many Parking Spots
   parking_zone.zone_id < parking_spots.zone_id

4. One Parking Spot → One Spot Category
   parking_spots.spot_category_id - parking_spots_categories.spot_category_id

5. One Vehicle → Many Parking Tickets
   vehicles.vehicle_id < parking_tickets.vehicle_id

6. One Vehicle → One Vehicle Category
   vehicles.category_id - vehicles_categories.category_id

7. One Ticket → One Parking Session
   parking_tickets.parking_session_id - parking_sessions.parking_session_id

8. One Parking Session → One Payment Record
   parking_sessions.parking_session_id - payment_records.parking_session_id

9. One Parking Session → One Parking Spot
   parking_sessions.spot_id > parking_spots.spot_id

10. One Vehicle → Many Parking Sessions
    vehicles.vehicle_id < parking_sessions.vehicle_id