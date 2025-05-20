# Project Background

Acting as a small database consulting company specializing in developing databases for the medical industry. I have just been awarded the contract to develop a data model for a database application system for a mid-size health insurance company to keep track of health claims, including patient information, provider(doctor) information, information about patient visits to their doctor, as well as prescription drugs prescribed to patients.

## Advanced Data Modeling Requirements and Normalization Standards
- Emphasize modeling for historical Data: include an entity showing a history of previous primary care doctors and the dates that the doctor was assigned to a particular patient.
- Made sure to include all 3 stages of normalization in the ERD
- Included Recursive Relationships
- Modified the ERD to make this distinction using an arc.

Learn more about each of these requirements and Standards [HERE](https://github.com/JordanTolliver-88/Database-Normalization-and-Specialized-Relationship-Modeling-Requirements/blob/main/README.md)

# Determining entities, attributes, UIDs
## Tables include
**PATIENT**
-   Patient ID
-   Name
-   Address
-   Phone
-   Email
-   Insurance ID
-   Insurance Company

**DOCTOR**
-   Doctor ID
-   Name
-   Address
-   Phone
-   Specialization
-   Hospital Affiliation

**HOSPITAL**
-   Hospital ID
-   Name
-   Address
-   Phone

**PRESCRIPTION**
-   RX ID
-   Date Prescribed
-   Dosage
-   Duration
-   Refillable
-   Drug Name
-   Side Effects
-   Benefits

# Relationships

Here, I have written out a SOME of the ERD relationship before displaying it in an Entity Relationship Diagram (ERD), which can be seen below.

- Each **PATIENT** must have one and only one **DOCTOR** (their primary doctor) Each DOCTOR may treat one or more PATIENT.
- Each **DOCTOR** may have one or more **HOSPITAL AFFILIATION**.
- Each **HOSPITAL AFFILIATION** must be for one and only one **DOCTOR**. Each **HOSPITAL** may have one or more **HOSPITAL AFFILIATION**.
- Each HOSPITAL **AFFILIATION** must be for one and only one **HOSPITAL**.
- Each **PATIENT** may be given one or more **PRESCRIPTION**.
- Each **PRESCRIPTION** must be for one and only one **PATIENT**. Each **PATIENT** may have one or more **OFFICE VISIT**.
- Each **OFFICE VISIT** must be for one and only one **PATIENT**. Each **DOCTOR** may preside over one or more **OFFICE VISIT**.
- Each **OFFICE VISIT** must be presided over by one and only one **DOCTOR**. Each **DOCTOR** may prescribe one or more **PRESCRIPTIONS**.
- Each **PRESCRIPTION** must be prescribed by one and only one **DOCTOR**.

![HealthOneERD](https://github.com/user-attachments/assets/31825893-1321-4d00-bc1f-9762461d4372)

# Database creation and Data Insertion using SQL:

## Below is the SQL used to create the database application system for a mid-size health insurance company:

**Here, I started by using SQL to create the databases.**

CREATE DATABASE HealthOne;
USE HealthOne;

**Now that the Database is set up, I can input the required tables while prioritizing Data Modeling Requirements and Normalization Standards as specified [HERE](https://github.com/JordanTolliver-88/Database-Normalization-and-Specialized-Relationship-Modeling-Requirements/blob/main/README.md)**

CREATE TABLE INSURANCE (

<img width="538" alt="INSURANCE" src="https://github.com/user-attachments/assets/dab5cafe-c71e-4eac-b8ee-37db5f17e8bd" />

CREATE TABLE PATIENT (

<img width="714" alt="PAITIENT" src="https://github.com/user-attachments/assets/31e79039-3046-4c17-9e61-bb7261201e34" />

CREATE TABLE DOCTOR (

<img width="442" alt="DOCTOR" src="https://github.com/user-attachments/assets/ab552322-389d-4a33-b5be-8273ba915ddf" />

CREATE TABLE PRIMARY_DOCTOR_HISTORY (

<img width="544" alt="PRIMARY DOC " src="https://github.com/user-attachments/assets/a02826a1-0d90-486e-b6da-3e2a72f3aa5e" />

CREATE TABLE HOSPITAL (

<img width="465" alt="HOSPITAL" src="https://github.com/user-attachments/assets/77e202e6-6ad7-4691-a1a6-27a8b0959ae7" />

CREATE TABLE HOSPITAL_AFFILIATION (

<img width="586" alt="HOSPITAL AFFILIATION" src="https://github.com/user-attachments/assets/846855a1-7904-4d1b-ba25-cacd96e5dcc7" />

CREATE TABLE PRESCRIPTION (

<img width="532" alt="PRESCRIPTION" src="https://github.com/user-attachments/assets/8ee3e587-8ac6-422a-926f-3abc47339a1c" />

CREATE TABLE DRUG (

<img width="426" alt="DRUG" src="https://github.com/user-attachments/assets/258a6925-ce9e-4cf2-89b6-f8e44575a778" />

CREATE TABLE REFFILABLE (

<img width="505" alt="REFFILABLE" src="https://github.com/user-attachments/assets/9594e3fd-5b70-428e-ba8f-25e2fa6f33a6" />

CREATE TABLE NON_REFFILABLE (
 
<img width="502" alt="NON REFUN  copy" src="https://github.com/user-attachments/assets/e9a7e7f0-a423-40ec-a1ec-ae2d6965781f" />

CREATE TABLE OFFICE_VISIT (

<img width="543" alt="office visit" src="https://github.com/user-attachments/assets/3f1f7ec8-f3ca-4676-a6e2-1f9226dc2eb2" />

# Inserting Data into Tables

Now that the database and tables are created, I will insert DUMMY DATA into the tables
 
INSERT INTO INSURANCE (Insurance_Company, Phone) VALUES 
('HealthGuard', '123-456-7890'),
('MediPlus', '123-111-2345'),
('LifeCare', '987-654-3210');

INSERT INTO PATIENT (Name, Address, Phone, Email, Insurance_Company_ID) VALUES 
('John Doe', '123 Elm St', '123-456-7891', 'john.doe@example.com', 1),
('Jane Smith', '456 Maple Rd', '987-654-3211', 'jane.smith@example.com', 2),
('Sam Wilson', '789 Oak Ave', '321-654-9870', 'sam.wilson@example.com', 3);

INSERT INTO DOCTOR (Name, Address, Phone, Specialization) VALUES 
('Dr. Alice Brown', '111 Medical St', '123-321-1234', 'Cardiology'),
('Dr. Bob White', '222 Healing Rd', '432-543-2345', 'General Medicine'),
('Dr. Carol Green', '333 Health Ave', '654-765-3456', 'Pediatrics');

INSERT INTO PRIMARY_DOCTOR_HISTORY (Patient_ID, Start_Date, End_Date, Reason_For_Leaving) VALUES 
(1, '2023-01-10', '2023-12-01', 'Moved to a new location'),
(2, '2022-05-15', '2022-11-10', 'Preferred a specialist'),
(3, '2023-03-20', NULL, '');

INSERT INTO HOSPITAL (Name, Address, Phone) VALUES 
('Central Health Hospital', '987 Medical Blvd', '123-123-1234'),
('Northside Hospital', '654 Recovery Rd', '987-987-9876');

INSERT INTO HOSPITAL_AFFILIATION (Doctor_ID, Hospital_ID, Date_Of_Affiliation) VALUES 
(1, 1, '2022-06-15'),
(2, 2, '2023-02-20'),
(3, 1, '2023-01-12');

INSERT INTO PRESCRIPTION (Doctor_ID, Patient_ID, Date_Prescribed, Dosage, Duration) VALUES 
(1, 1, '2023-11-01', '500 mg', '2 weeks'),
(2, 2, '2023-10-15', '250 mg', '1 month'),
(3, 3, '2023-09-20', '100 mg', '10 days');

INSERT INTO DRUG (Name, Side_Effects, Benefits) VALUES 
('Aspirin', 'Nausea, Headache', 'Pain relief'),
('Ibuprofen', 'Drowsiness, Upset Stomach', 'Anti-inflammatory'),
('Amoxicillin', 'Diarrhea, Allergic Reaction', 'Antibiotic');

INSERT INTO REFFILABLE (RX_ID, Num_Of_Refills, Comments) VALUES 
(1, 2, 'Patient should revisit after refills are used up'),
(2, 3, 'Monitor usage and side effects');

INSERT INTO NON_REFFILABLE (RX_ID, Reason) VALUES 
(3, 'Potential for overuse and allergic reaction');

INSERT INTO OFFICE_VISIT (Patient_ID, Doctor_ID, Date_Of_Visit, Symptoms) VALUES 
(1, 1, '2023-11-05', 'Chest pain and dizziness'),
(2, 2, '2023-10-20', 'Persistent cough and fever'),
(3, 3, '2023-09-25', 'Rash on arms and legs');
