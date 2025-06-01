# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission 

## Scenario Chosen:
 ### University

## ER Diagram:
![image](https://github.com/user-attachments/assets/b222eec9-eed2-41fa-b55a-1eb977d0b861)


## Entities and Attributes:
- ### Entity 1: USER
**Attributes:** ID (Primary Key), NAME, PHNO, ADDRESS
- ### Entity 2: STUDENT
**Attributes:**  ID (Primary Key), REGNO, NAME, DOB, DEPT, YEAR, YEAR_ENROLLED, CREDITS
- ### Entity 3: PROGRAM
 **Attributes:** PROG_ID (Primary Key), PROG_NAME, CREDIT_POINTS
- ### Entity 4: COURSE
  **Attributes:**  ID (Primary Key), NAME, PREREQUEST, STATUS, ENROLLMENT
- ### Entity 5: REGISTRATION
**Attributes:**  REG_ID (Primary Key), STU_ID, DATE, TYPE ...
...

## Relationships and Constraints:
 ### Relationship 1 - MANAGEMENT
- **Between:**  USER ↔ REGISTRATION
- **Cardinality:**  N from USER to REGISTRATION
- **Participation:**  Total on PATIENT, Partial on DOCTORS
### Relationship 2 - ENROLL
- **Between:** STUDENT ↔ PROGRAM
- **Cardinality:** M:1 (Many Students per Program)
**Participation:** Total on STUDENT, Partial on PROGRAM
### Relationship 3 - CONTAINS
- **Between:**  PROGRAM ↔ COURSE
- **Cardinality:**  1:M from PROGRAM to COURSE
- **Participation:**  Total on COURSE, Partial on PROGRAM
### Relationship 4 - ATTEMPTS
- **Between:** STUDENT ↔ COURSE
- **Cardinality:** M:N
- **Participation:** Partial on both sides
### Relationship 5 - REGISTRATION
- **Between:** STUDENT ↔ REGISTRATION
- **Cardinality:** 1:N from STUDENT to REGISTRATION
- **Participation:** Total on REGISTRATION, Partial on STUDENT
### Relationship 6 - PREREQUEST
- **Between:**  COURSE ↔ COURSE
- **Cardinality:** 1:1 or M:1 (Optional prerequisite per course)
- **Participation:** Optional on both sides ...
...

## Extension - Prerequisite:
...
In the diagram, prerequisites are modeled using the PREREQUEST attribute inside the COURSE
entity. This means a course can mention another course as its required prerequisite. This helps the
university system check if a student is eligible to take a particular course based on past course
completions. By including it as an attribute (not a separate relationship), the design stays simple
and still supports course dependencies in the academic structure.
...
## Design Choices:
- STUDENT and USER separated to distinguish academic and administrative roles. -PROGRAM
and COURSE designed as core academic entities, linked by the CONTAINS relationship.
- REGISTRATION used as a bridge between USER and STUDENT activity tracking.
- ATTEMPTS relationship captures performance metrics across courses.
- PREREQUEST allows course dependency modeling internally without a separate entity.
## RESULT:
**The ER model includes 6 relationships:**  CHECKUP, DETAILED_INFO_ABOUT_THE_PATIENT, OPERATION, REG_PATIENT, ADMIT_PATIENT, and DISCHARGE, each with defined cardinality and participation constraints connecting patients, doctors, departments, and billing details.
