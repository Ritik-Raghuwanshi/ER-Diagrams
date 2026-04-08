# 🏥 Clinic Appointment and Diagnostics Platform

## 📌 Overview

This ER diagram represents a **Clinic Appointment and Diagnostics Platform** designed to manage:

* Clinics and their staff
* Doctors and patients
* Appointments and consultations
* Diagnostic tests and reports
* Payments and transactions

The system streamlines the complete flow from **patient registration → appointment → consultation → testing → report generation → payment**.

---

## 🧩 Core Entities

### 🏢 Clinic

Stores clinic details such as name, license, contact, and rating.

* One clinic can have **multiple users**
* Acts as the root entity

---

### 👤 Users

Central entity for all users in the system.

* Can represent:

  * Doctor
  * Patient
  * Staff/Admin
* Each user belongs to one clinic

---

### 👨‍⚕️ Doctors

Represents doctors.

* Linked to:

  * User
  * Department
  * Specialization
* Stores experience, salary, and qualifications

---

### 🧬 Specializations

Defines doctor expertise (e.g., Cardiologist).

* One specialization → Many doctors

---

### 🏬 Departments

Defines clinic departments.

* One department → Many doctors

---

### 🧑‍🦽 Patients

Represents patients.

* Each patient is mapped to a user
* Tracks active status

---

### 📅 Appointments

Handles booking between patient and doctor.

* Includes date, time, and status
* Links one doctor and one patient

---

### 💬 Consultations

Represents actual consultation sessions.

* Linked to appointment
* Includes:

  * Mode (online/offline)
  * Duration
  * Fees
  * Prescription
* Also linked directly to doctor and patient

---

### 🧪 Tests

Represents diagnostic tests.

* Includes:

  * Type (pathology, radiology, etc.)
  * Charges
  * Report status

---

### 🔗 Patient Test Summary (Junction Table)

Connects:

* Patient
* Test
* Consultation

Used to track which test was taken during which consultation.

---

### 📄 Reports

Stores test reports.

* Linked to:

  * Patient test summary
  * Test
* Tracks report lifecycle

---

### 💳 Payments

Handles all transactions.

* Includes:

  * Transaction ID
  * Status
  * Amount
* Used for:

  * Consultation payments
  * Test payments

---
## 🔗 Relationships (Final Refined Version)

### 🏢 Clinic → Users
- **1 : Many**
- One clinic can have multiple users  

---

### 👤 Users → Doctor
- **1 : 1**
- One user can be one doctor  

---

### 👤 Users → Patient
- **1 : 1**
- One user can be one patient  

---

### 👨‍⚕️ Doctor → Specialization
- **1 : Many**
- One doctor can have multiple specializations  

---

### 🏬 Department → Doctors
- **1 : Many**
- One department can have multiple doctors  

---

### 👨‍⚕️ Doctor → Appointments
- **1 : Many**
- One doctor can have multiple appointments  

---

### 🧑‍🦽 Patient → Appointments
- **1 : Many**
- One patient can book multiple appointments  

---

### 📅 Appointment → Consultation
- **1 : 1**
- Each appointment results in one consultation  

---

### 👨‍⚕️ Doctor → Consultations
- **1 : Many**
- One doctor conducts multiple consultations  

---

### 💬 Consultation → Payment
- **1 : 1**
- Each consultation has one payment  

---

### 🧪 Test → Payment
- **1 : 1**
- Each test has one payment  

---

### 🧑‍🦽 Patient → Patient Test Summary
- **1 : 1**
- One patient has one test summary  

---

### 💬 Consultation → Patient Test Summary
- **1 : Many**
- One consultation can include multiple test records  

---

### 🔗 Patient Test Summary → Tests
- **Many : Many**
- One summary can have multiple tests  
- One test can belong to multiple summaries  

---

### 🔗 Patient Test Summary → Reports
- **1 : Many**
- One summary can generate multiple reports  

---

### 🧪 Test → Reports
- **1 : Many**
- One test type can have multiple reports  

---

## 🔄 System Flow

1. Clinic is registered
2. Users are created (doctor/patient)
3. Doctor is assigned specialization & department
4. Patient books appointment
5. Consultation happens
6. Tests are prescribed (if needed)
7. Tests recorded in patient_test_summary
8. Reports generated
9. Payment completed

---

## 🎯 Key Design Highlights

* Centralized **Users table (role-based design)**
* Clear separation between:

  * Appointment (booking)
  * Consultation (actual interaction)
* Scalable for multiple clinics
* Supports diagnostics + consultation together

---

