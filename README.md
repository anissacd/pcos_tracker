### pcos_tracker
SQL-based project to track PCOS appointments and follow-ups

### PCOS Appointment and Follow-Up Tracker (PostgreSQL)

### Project Summary
This project simulates a healthcare data system for tracking appointments and follow-up needs among patients with Polycystic Ovary Syndrome (PCOS). It demonstrates relational database design and SQL analysis using realistic patient and appointment data.

### Database Structure

### patients
- patient_id (Primary Key)
- first_name
- last_name
- birth_date
- gender (Only 'Female' or 'Other')
- race_ethnicity

### appointments
- appointment_id (Primary Key)
- patient_id (Foreign Key to patients)
- appointment_date
- provider_type (e.g., OB-GYN, Endocrinologist)
- visit_reason
- follow_up_needed (BOOLEAN)

### Key SQL Queries

### Join Patients and Appointments
```sql
SELECT 
  CONCAT(patients.first_name, ' ', patients.last_name) AS full_name,
  appointments.provider_type,
  appointments.appointment_date,
  appointments.visit_reason,
  appointments.follow_up_needed
FROM appointments
JOIN patients ON appointments.patient_id = patients.patient_id;
```

### Count Appointments Needing Follow-Up
```sql
SELECT COUNT(*) AS total_follow_ups
FROM appointments
WHERE follow_up_needed = TRUE;
```

### Appointments by Provider Type
```sql
SELECT provider_type, COUNT(*) AS total
FROM appointments
GROUP BY provider_type;
```

### Appointments in June 2024
```sql
SELECT 
  patients.first_name || ' ' || patients.last_name AS full_name,
  appointment_date,
  provider_type
FROM appointments
JOIN patients ON appointments.patient_id = patients.patient_id
WHERE appointment_date BETWEEN '2024-06-01' AND '2024-06-30';
```

### Tools Used
- PostgreSQL
- pgAdmin
- SQL
- Optional: Tableau or Excel for visualization

### Project Highlights
- Designed and normalized a relational healthcare database
- Used SQL to generate insights about follow-up needs and provider trends
- Demonstrated filtering, joining, grouping, and date-based analysis
- Built a clean structure that can scale to include labs, diagnoses, or treatment tracking

### Possible Extensions
- Add diagnosis or treatment tables
- Track lab result trends
- Build visual dashboards in Tableau or Excel
- Export results to CSV or create database views for reporting
