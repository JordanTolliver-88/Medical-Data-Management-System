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

Here, I have written out each ERD relationship before displaying it in an Entity Relationship Diagram (ERD), which can be seen below.

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




