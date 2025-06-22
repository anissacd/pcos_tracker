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

### Sample Queries

### Join all data
```sql
SELECT *
FROM appointments a
JOIN patients p ON a.patient_id = p.patient_id;
```

### Upcoming follow-ups
```sql
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

### Appointments in date range
```sql
SELECT *
FROM appointments
WHERE appointment_date BETWEEN '2024-06-01' AND '2024-06-30';
```

### CSV Export Instructions

After running a query (such as the join query above), export the results to CSV:

- In pgAdmin:
  - Run the query
  - Right-click on the result grid
  - Select "Save as CSV"


### Concepts Demonstrated

- Relational database structure
- One-to-many relationships (patients to appointments)
- SQL joins and filters
- Exporting SQL results to CSV for reporting
- Healthcare-focused data modeling
