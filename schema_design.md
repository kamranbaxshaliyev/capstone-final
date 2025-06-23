Schema Design for Smart Clinic Management System
Overview
This document outlines the MySQL relational database schema design for the Smart Clinic Management System. The schema supports core entities including Doctors, Patients, Admin Users, and Appointments. It defines tables, primary keys, foreign keys, and relationships needed for managing clinic operations effectively.

Tables and Relationships
1. admins
Column	Data Type	Constraints	Description
id	BIGINT	PRIMARY KEY, AUTO_INCREMENT	Unique identifier for admin user
username	VARCHAR(255)	UNIQUE, NOT NULL	Admin username
password	VARCHAR(255)	NOT NULL	Encrypted admin password
role	VARCHAR(50)	NOT NULL	Role designation
created_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP	Record creation timestamp
updated_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP	Last update timestamp

2. doctors
Column	Data Type	Constraints	Description
id	BIGINT	PRIMARY KEY, AUTO_INCREMENT	Unique doctor ID
username	VARCHAR(255)	UNIQUE, NOT NULL	Doctor's username
password	VARCHAR(255)	NOT NULL	Encrypted password
first_name	VARCHAR(100)	NOT NULL	Doctor's first name
last_name	VARCHAR(100)	NOT NULL	Doctor's last name
specialty	VARCHAR(255)	NOT NULL	Doctor's specialty
email	VARCHAR(255)	UNIQUE, NOT NULL	Doctor's email
phone_number	VARCHAR(20)		Contact number
availability	JSON		Structured availability schedule
created_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP	Record creation time
updated_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP	Last update time

3. patients
Column	Data Type	Constraints	Description
id	BIGINT	PRIMARY KEY, AUTO_INCREMENT	Unique patient ID
first_name	VARCHAR(100)	NOT NULL	Patient's first name
last_name	VARCHAR(100)	NOT NULL	Patient's last name
email	VARCHAR(255)	UNIQUE, NOT NULL	Patient's email
phone_number	VARCHAR(20)		Contact number
date_of_birth	DATE		Patient's DOB
address	VARCHAR(255)		Patient's address
created_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP	Record creation time
updated_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP	Last update time

4. appointments
Column	Data Type	Constraints	Description
id	BIGINT	PRIMARY KEY, AUTO_INCREMENT	Unique appointment ID
doctor_id	BIGINT	FOREIGN KEY REFERENCES doctors(id)	Doctor assigned
patient_id	BIGINT	FOREIGN KEY REFERENCES patients(id)	Patient attending
appointment_time	DATETIME	NOT NULL	Scheduled date and time
status	VARCHAR(50)	NOT NULL	Status (scheduled, completed, canceled)
created_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP	Record creation time
updated_at	TIMESTAMP	DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP	Last update time

Relationships
Each appointment references one doctor and one patient.

doctors and patients have one-to-many relationships with appointments.

admins manage the system but are separate from clinical entities.

Additional Notes
The schema uses timestamps to track record creation and updates.

Passwords are stored encrypted and never stored as plaintext.

The availability field in doctors is stored in JSON to allow flexible scheduling.

Foreign key constraints maintain referential integrity between tables.


