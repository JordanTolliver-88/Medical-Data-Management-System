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
    Insurance_Company_ID INT PRIMARY KEY AUTO_INCREMENT,
    Insurance_Company VARCHAR(100) NOT NULL,
    Phone VARCHAR(15)
);

CREATE TABLE PATIENT (
    Patient_ID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100) NOT NULL,
    Address VARCHAR(255),
    Phone VARCHAR(15),
    Email VARCHAR(100),
    Insurance_Company_ID INT,
    FOREIGN KEY (Insurance_Company_ID) REFERENCES INSURANCE(Insurance_Company_ID)
);

CREATE TABLE DOCTOR (
    Doctor_ID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100) NOT NULL,
    Address VARCHAR(255),
    Phone VARCHAR(15),
    Specialization VARCHAR(100)
);

CREATE TABLE PRIMARY_DOCTOR_HISTORY (
    Patient_ID INT,
    Start_Date DATE,
    End_Date DATE,
    Reason_For_Leaving VARCHAR(255),
    PRIMARY KEY (Patient_ID, Start_Date),
    FOREIGN KEY (Patient_ID) REFERENCES PATIENT(Patient_ID)
);

CREATE TABLE HOSPITAL (
    Hospital_ID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100) NOT NULL,
    Address VARCHAR(255),
    Phone VARCHAR(15)
);

CREATE TABLE HOSPITAL_AFFILIATION (
    Doctor_ID INT,
    Hospital_ID INT,
    Date_Of_Affiliation DATE,
    PRIMARY KEY (Doctor_ID, Hospital_ID),
    FOREIGN KEY (Doctor_ID) REFERENCES DOCTOR(Doctor_ID),
    FOREIGN KEY (Hospital_ID) REFERENCES HOSPITAL(Hospital_ID)
);

CREATE TABLE PRESCRIPTION (
    RX_ID INT PRIMARY KEY AUTO_INCREMENT,
    Doctor_ID INT,
    Patient_ID INT,
    Date_Prescribed DATE,
    Dosage VARCHAR(50),
    Duration VARCHAR(50),
    FOREIGN KEY (Doctor_ID) REFERENCES DOCTOR(Doctor_ID),
    FOREIGN KEY (Patient_ID) REFERENCES PATIENT(Patient_ID)
);

CREATE TABLE DRUG (
    Drug_ID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100),
    Side_Effects VARCHAR(255),
    Benefits VARCHAR(255)
);

CREATE TABLE REFFILABLE (
    RX_ID INT,
    Num_Of_Refills INT,
    Comments VARCHAR(255),
    PRIMARY KEY (RX_ID),
    FOREIGN KEY (RX_ID) REFERENCES PRESCRIPTION(RX_ID)
);

CREATE TABLE NON_REFFILABLE (
    RX_ID INT,
    Reason VARCHAR(255),
    PRIMARY KEY (RX_ID),
    FOREIGN KEY (RX_ID) REFERENCES PRESCRIPTION(RX_ID)
);

CREATE TABLE OFFICE_VISIT (
    Patient_ID INT,
    Doctor_ID INT,
    Date_Of_Visit DATE,
    Symptoms VARCHAR(255),
    PRIMARY KEY (Patient_ID, Doctor_ID, Date_Of_Visit),
    FOREIGN KEY (Patient_ID) REFERENCES PATIENT(Patient_ID),
    FOREIGN KEY (Doctor_ID) REFERENCES DOCTOR(Doctor_ID)
);

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
