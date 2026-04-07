# 🏋️ Fitness Influencer Coaching Platform

## 📌 Overview
This ER diagram represents a **Fitness Influencer Coaching Platform** where trainers provide fitness, diet, and consultation services to clients.  

Initially, coaching happens through DMs and calls, but this system helps manage everything in a structured way:
- Client onboarding  
- Fitness & diet plans  
- Live sessions  
- Subscriptions & payments  
- Progress tracking  

---

## 🧑‍🤝‍🧑 Core Entities

### 1. Users
This is the base entity for all people in the system.
- Stores basic details like name, email, phone, password
- A user can be either a **Trainer** or a **Client**

---

### 2. Trainers
Represents fitness coaches.
- Linked to `users`
- Stores:
  - Experience
  - Specialization
  - Salary
  - Personal training fees

👉 One trainer can handle **multiple clients**

---

### 3. Clients
Represents customers taking coaching services.
- Linked to `users`
- Assigned to a trainer

---

## Coaching Features

### 4. Plans
Different types of services offered:
- Diet Plans
- Fitness Plans
- Live Sessions

Includes:
- Plan name
- Type (`diet`, `fitness`, `livesessions`)
- Price & discount

---

### 5. Diet Plans
Custom diet plans created by trainers.
- Linked to:
  - Trainer
  - Client
  - Plan
- Includes:
  - Diet description
  - Type (`veg`, `nonveg`)

---

### 6. Live Sessions
Online sessions conducted by trainers.
- Includes:
  - Session name
  - Duration
  - Date & timing
- Linked to:
  - Trainer
  - Plan

---

### 7. Consultation Sessions
1-on-1 paid consultation calls.
- Between trainer and client
- Includes:
  - Date & time
  - Consultation fees

---

## Tracking & Monitoring

### 8. Progress Reports
Tracks client improvement over time.
- Combines:
  - Check-ins
  - Body measurements
  - Trainer notes

---

### 9. Body Measurements
Stores physical stats:
- Height
- Weight
- BMI

---

### 10. Check-ins
Tracks attendance/activity:
- Check-in time
- Check-out time

---

### 11. Trainer Notes
Feedback or guidance given by trainers:
- Notes for specific clients
- Helps in tracking performance & improvement

---

## Business & Payments

### 12. Subscriptions
Represents plans purchased by clients.
- Types:
  - Weekly
  - Monthly
  - Yearly
- Linked to:
  - Client
  - Plan

---

### 13. Payments
Handles all transactions.
- Includes:
  - Payment status (`success`, `pending`, `rejected`)
  - Amount
  - Payment gateway
- Linked to:
  - Client
  - Subscription

---

## 🔗 Relationships Summary

- One **User → Trainer / Client**
- One **Trainer → Many Clients**
- One **Client → Many Check-ins, Measurements, Notes**
- One **Plan → Many Live Sessions & Diet Plans**
- One **Client → Many Subscriptions**
- One **Subscription → One Plan**
- One **Subscription → Many Payments**
- One **Trainer ↔ Client → Consultation Sessions**

---

## 🚀 Real-World Flow

1. User signs up → becomes Client or Trainer  
2. Client selects a Plan → creates Subscription  
3. Payment is processed  
4. Trainer provides:
   - Diet Plan  
   - Live Sessions  
   - Consultation  
5. Client progress is tracked via:
   - Check-ins  
   - Body measurements  
   - Notes  

---
