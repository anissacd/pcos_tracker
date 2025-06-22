### PCOS Appointment & Follow-Up Tracker (PostgreSQL)

This project simulates a small-scale healthcare data system for tracking appointments and follow-up needs among patients diagnosed with or suspected to have Polycystic Ovary Syndrome (PCOS). It demonstrates database design, data entry, SQL querying, and data export for visualization or reporting.

### Database Overview

### patients
- patient_id (Primary Key)
- first_name
- last_name
- birth_date
- gender (values: 'Female', 'Other')
- race_ethnicity

### appointments
- appointment_id (Primary Key)
- patient_id (Foreign Key to patients)
- appointment_date
- provider_type
- visit_reason
- follow_up_needed (BOOLEAN)

### visit_types
- visit_reason (Primary Key)
- health_code (e.g., ICD-10 or CPT code)
- cost (NUMERIC)

### Table Creation

```sql
CREATE TABLE patients (
  patient_id SERIAL PRIMARY KEY,
  first_name TEXT,
  last_name TEXT,
  birth_date DATE,
  gender TEXT CHECK (gender IN ('Female', 'Other')),
  race_ethnicity TEXT
);

CREATE TABLE appointments (
  appointment_id SERIAL PRIMARY KEY,
  patient_id INT REFERENCES patients(patient_id),
  appointment_date DATE,
  provider_type TEXT,
  visit_reason TEXT,
  follow_up_needed BOOLEAN
);

CREATE TABLE visit_types (
  visit_reason TEXT PRIMARY KEY,
  health_code TEXT,
  cost NUMERIC(8,2)
);


```
### Sample Queries
### Join All Data
```sql
SELECT *
FROM patients p
JOIN appointments a ON p.patient_id = a.patient_id
JOIN visit_types v ON a.visit_reason = v.visit_reason
ORDER BY a.appointment_date;
```
### Upcoming Follow-Ups
SELECT
  a.appointment_id,
  CONCAT(p.first_name, ' ', p.last_name) AS full_name,
  a.appointment_date,
  a.provider_type,
  a.visit_reason
FROM appointments a
JOIN patients p ON a.patient_id = p.patient_id
WHERE a.follow_up_needed = TRUE;
```


