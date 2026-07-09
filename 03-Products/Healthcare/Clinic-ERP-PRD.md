# Qimam Clinic ERP - Product Requirements Document

## Product Name
Qimam Clinic ERP

## Target Platform
Odoo 19 Community

## Target Market
Private clinics, polyclinics, day-care centers, dental clinics, dermatology clinics, physiotherapy centers, optical clinics, cosmetic centers, and small medical centers in Saudi Arabia, GCC, and Egypt.

## Objective
Build a lightweight, fast, subscription-ready medical center management solution that handles appointments, doctors, patients, consultations, prescriptions, billing, insurance, packages, inventory, and accounting.

## Product Positioning
Qimam Clinic ERP is the simplified healthcare product for smaller healthcare providers that do not need the full enterprise hospital stack.

## Core Modules
1. Clinic Master Data
2. Patient Registration
3. Appointments and Queues
4. Doctor Consultation
5. Prescriptions
6. Lab/Radiology External Orders
7. Procedures and Services
8. Insurance and Approvals
9. Billing and Payments
10. Packages and Memberships
11. Inventory and Consumables
12. Staff Commission
13. Dashboards
14. Patient Communication
15. Accounting Integration

## MVP Scope
- Patient profile
- Appointment booking
- Multi-doctor calendars
- Queue management
- Consultation form
- Diagnosis and prescription
- Procedure/service orders
- Cash billing
- Insurance policy and approval reference
- Odoo invoice creation
- Payment registration
- Basic inventory deduction for consumables
- WhatsApp/SMS placeholders
- Daily revenue dashboard

## Revenue Models
- Consultation fees
- Procedure fees
- Lab/radiology external services
- Packages
- Memberships
- Insurance claims
- Consumables and product sales

## Accounting Integration
All services and procedures must be linked to Odoo products. On billing, the system must create account.move invoices with lines linked to patient, doctor, clinic, department, encounter, and service category.

## Key Workflows

### Cash Visit
Register patient -> book appointment -> check-in -> consultation -> service/procedure -> invoice -> payment -> follow-up.

### Insurance Visit
Register patient -> select insurance policy -> check eligibility/approval reference -> consultation -> charge capture -> patient share/insurance share -> invoice/claim draft -> payment/reconciliation.

### Package Visit
Create package -> sell package -> consume sessions -> track remaining sessions -> generate accounting entries.

## Roles
- Receptionist
- Doctor
- Nurse
- Cashier
- Insurance Officer
- Clinic Manager
- Accountant
- Administrator

## Main Data Models
- qimam.clinic.patient
- qimam.clinic.appointment
- qimam.clinic.encounter
- qimam.clinic.prescription
- qimam.clinic.service.order
- qimam.clinic.package
- qimam.clinic.package.line
- qimam.clinic.insurance.policy
- qimam.clinic.claim
- qimam.clinic.charge
- qimam.clinic.commission

## Differences from Hospital ERP
- No full inpatient ADT in MVP.
- No complex bed/ward management.
- No full nursing MAR in MVP.
- Simpler claim workflow.
- Faster onboarding.
- SaaS-ready subscription packaging.

## Acceptance Criteria
- Clinics can operate daily appointments and billing without accounting manual entry.
- Each invoice must trace back to doctor, patient, service, and encounter.
- Package consumption must be auditable.
- Staff commission report must be available.
- System must support multiple branches and multiple doctors.
- The user interface must be simple enough for small medical centers.