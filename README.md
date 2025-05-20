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
 
INSERT INTO INSURANCE (

<img width="521" alt="Insurance" src="https://github.com/user-attachments/assets/2ccab85f-c6dc-48cd-bfe8-ad9497ac8e78" />

INSERT INTO PATIENT (

<img width="698" alt="PATIENT copy" src="https://github.com/user-attachments/assets/00218d19-e4fd-4a2e-85fa-f3e99191c0ad" />

INSERT INTO DOCTOR (

<img width="671" alt="DAOCTOR" src="https://github.com/user-attachments/assets/2fd628a0-05d3-4dde-8a11-ee56b2d2e43f" />

INSERT INTO PRIMARY_DOCTOR_HISTORY (

<img width="962" alt="PRIMARY DOC" src="https://github.com/user-attachments/assets/3c105f70-8fb3-4489-97b5-1ced21e16a21" />

INSERT INTO HOSPITAL (

<img width="632" alt="HOSPITAL" src="https://github.com/user-attachments/assets/7b0fa5df-c030-439d-9b01-74202f3363ea" />

INSERT INTO HOSPITAL_AFFILIATION (

<img width="753" alt="HOSPITAL AFFILIATION" src="https://github.com/user-attachments/assets/16b73dad-1d20-446c-8d58-fc7900dcbbae" />

INSERT INTO PRESCRIPTION (

<img width="772" alt="PRESCRIPTION copy" src="https://github.com/user-attachments/assets/8653c8e7-a23f-4e97-a089-b42649acd8ce" />

INSERT INTO DRUG (

<img width="612" alt="DRUG" src="https://github.com/user-attachments/assets/4f0b7bda-c2d6-4469-8c15-2ec1075bb8ec" />

INSERT INTO REFFILABLE (

<img width="588" alt="REFILABLE" src="https://github.com/user-attachments/assets/bcf949a0-375e-4214-a6fc-cf74e3f3dc3b" />

INSERT INTO NON_REFFILABLE (

<img width="562" alt="NON RE" src="https://github.com/user-attachments/assets/52e31fe5-8592-4f00-93ec-bf96ff850b2d" />

INSERT INTO OFFICE_VISIT (

<img width="725" alt="OFFICE VISIT" src="https://github.com/user-attachments/assets/50446696-c3f5-44a8-ba24-b2bf26717d85" />
