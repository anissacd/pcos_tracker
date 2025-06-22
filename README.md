# pcos_tracker
SQL-based project to track PCOS appointments and follow-ups

# PCOS Appointment and Follow-Up Tracker (PostgreSQL)

## Project Summary
This project simulates a healthcare data system for tracking appointments and follow-up needs among patients with Polycystic Ovary Syndrome (PCOS). It demonstrates relational database design and SQL analysis using realistic patient and appointment data.

## Database Structure

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

## Key SQL Queries

### Join Patients and Appointments

SELECT 
  CONCAT(patients.first_name, ' ',patients.last_name) AS full_name,
  appointments.provider_type,
  appointments.appointment_date,
  appointments.visit_reason,
  appointments.follow_up_needed
FROM appointments
JOIN patients ON appointments.patient_id = patients.patient_id;
