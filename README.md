# healthcare-sql-project
Patients Table
sql
CREATE TABLE Patients (
patient_id INT PRIMARY KEY,
name VARCHAR(100),
age INT,
gender VARCHAR(10),
contact
_number VARCHAR(15)
);
Doctors Table
sql
CREATE TABLE Doctors (
doctor
_id INT PRIMARY KEY,
name VARCHAR(100),
specialization VARCHAR(50),
contact
_number VARCHAR(15)
);
Appointments Table
sql
CREATE TABLE Appointments (
appointment_id INT PRIMARY KEY,
patient_id INT,
doctor
_id INT,
appointment_date DATE,
FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id)
);
sql
Diagnoses Table
CREATE TABLE Diagnoses (
diagnosis_id INT PRIMARY KEY,
appointment_id INT,
symptoms TEXT,
diagnosis TEXT,
FOREIGN KEY (appointment_id) REFERENCES Appointments(appointment_id)
);
Prescriptions Table
sql
CREATE TABLE Prescriptions (
prescription_id INT PRIMARY KEY,
appointment_id INT,
medicine
_name VARCHAR(100),
dosage VARCHAR(50),
FOREIGN KEY (appointment_id) REFERENCES Appointments(appointment_id)
);
Billing Table
sql
CREATE TABLE Billing (
bill
_id INT PRIMARY KEY,
appointment_id INT,
amount DECIMAL(10,2),
payment_status VARCHAR(20),
FOREIGN KEY (appointment_id) REFERENCES Appointments(appointment_id)
);
3. Insert Sample Data
sql
-- Patients
INSERT INTO Patients VALUES
(1, 'Sathvika', 22, 'Female', '9999912345'),
(2, 'Raj', 30, 'Male', '8888812345');
-- Doctors
INSERT INTO Doctors VALUES
(1, 'Dr. Sharma', 'Cardiology', '7777712345'),
(2, 'Dr. Meena', 'Dermatology', '6666612345');
-- Appointments
INSERT INTO Appointments VALUES
(101, 1, 1, '2025-07-25'),
(102, 2, 2, '2025-07-26');
-- Diagnoses
INSERT INTO Diagnoses VALUES
(1001, 101, 'Chest pain, fatigue', 'Mild Heart Block'),
(1002, 102, 'Skin rash', 'Allergic Reaction');
-- Prescriptions
INSERT INTO Prescriptions VALUES
(201, 101, 'Aspirin', '1 tab/day'),
(202, 102, 'Cetirizine', '1 tab/night');
-- Billing
INSERT INTO Billing VALUES
(301, 101, 1500.00, 'Paid'),
(302, 102, 800.00, 'Unpaid');
4. Useful Queries
1. List all patients and their doctors
sql
SELECT p.name AS patient_name, d.name AS doctor_name, d.specialization
FROM Patients p
JOIN Appointments a ON p.patient_id = a.patient_
id
JOIN Doctors d ON a.doctor
id = d.doctor
_
_id;
2. Get all diagnoses with patient names
sql
SELECT p.name, d.diagnosis, d.symptoms
FROM Diagnoses d
JOIN Appointments a ON d.appointment_id = a.appointment_
id
JOIN Patients p ON a.patient_id = p.patient_id;
3. Show unpaid bills
sql
SELECT p.name, b.amount, b.payment_
status
FROM Billing b
JOIN Appointments a ON b.appointment_id = a.appointment_
id
JOIN Patients p ON a.patient_id = p.patient_
id
WHERE b.payment_status = 'Unpaid';
4. Total revenue collected
sql
SELECT SUM(amount) AS total_
collected
FROM Billing
WHERE payment_status = 'Paid';