# Qimam Hospital ERP - Product Requirements Document

## Product Name
Qimam Hospital ERP

## Target Platform
Odoo 19 Community

## Target Market
Saudi Arabia, GCC, Egypt

## Objective
Build a scalable hospital management platform on Odoo 19 Community that connects clinical operations, patient administration, revenue cycle, pharmacy, laboratory, radiology, inpatient care, inventory, purchasing, HR, and accounting.

## Product Positioning
Qimam Hospital ERP is not a simple clinic app. It is an enterprise-grade hospital operating system for medium and large healthcare providers.

## Core Principles
- Patient-centered workflows
- Financially connected operations
- Modular architecture
- Saudi/GCC readiness
- Insurance and claims readiness
- Clinical documentation discipline
- Auditability and security
- Future interoperability with HL7 FHIR, NPHIES, DICOM/PACS, e-prescription, SMS/WhatsApp, and payment gateways

## High-Level Modules
1. Healthcare Master Data
2. Patient Registration and EMPI
3. Appointments and Scheduling
4. Outpatient Department
5. Emergency Department
6. Inpatient and ADT
7. Doctors Workbench / EMR
8. Nursing Workbench
9. Pharmacy
10. Laboratory Information System
11. Radiology Information System
12. Operating Room and Procedures
13. Insurance and Revenue Cycle
14. Billing and Accounting Integration
15. Inventory and Procurement
16. HR and Staff Scheduling
17. Patient Portal
18. Dashboards and BI
19. Security and Audit Trail
20. Integration Layer

## Key Business Workflows

### Patient Journey
Patient registration -> eligibility/pre-authorization -> appointment/triage -> doctor consultation -> orders -> lab/radiology/pharmacy/procedure -> billing -> payment/insurance claim -> discharge/follow-up.

### Inpatient Journey
Admission -> bed assignment -> nursing assessments -> physician rounds -> medication administration -> orders -> consumables -> surgery/procedures -> discharge summary -> final bill -> insurance claim/accounting.

### Revenue Cycle
Encounter creation -> charge capture -> invoice draft -> patient share calculation -> insurance share calculation -> approvals -> invoice posting -> payment -> claim submission -> remittance -> reconciliation -> write-off/denial management.

## Accounting Integration
Use Odoo account.move, account.move.line, product.product, product.template, account.payment, account.journal, stock.valuation.layer where available. Avoid Enterprise-only dependencies. Every chargeable healthcare service must map to an Odoo product with income account, taxes, analytic account, and cost center.

## Core Data Models
- qimam.healthcare.patient
- qimam.healthcare.patient.identifier
- qimam.healthcare.encounter
- qimam.healthcare.appointment
- qimam.healthcare.provider
- qimam.healthcare.department
- qimam.healthcare.specialty
- qimam.healthcare.order
- qimam.healthcare.clinical.note
- qimam.healthcare.diagnosis
- qimam.healthcare.procedure
- qimam.healthcare.medication.order
- qimam.healthcare.lab.order
- qimam.healthcare.lab.result
- qimam.healthcare.radiology.order
- qimam.healthcare.radiology.report
- qimam.healthcare.admission
- qimam.healthcare.bed
- qimam.healthcare.insurance.policy
- qimam.healthcare.claim
- qimam.healthcare.claim.line
- qimam.healthcare.charge
- qimam.healthcare.consent
- qimam.healthcare.audit.log

## Coding Standards
Prepare master data fields for ICD-10/ICD-11, CPT/local procedure codes, LOINC, SNOMED CT, medication codes, and future FHIR mapping.

## MVP Scope
- Patient registration
- Appointments
- OPD consultation
- Diagnosis and prescriptions
- Lab orders and results
- Radiology orders and reports
- Pharmacy dispensing
- Basic insurance policy
- Cash and insurance billing
- Odoo accounting invoices
- Basic stock integration
- User roles and dashboards

## Phase 2
- Inpatient ADT
- Beds and wards
- Nursing workflows
- Medication administration record
- Surgery/OR
- Claim lifecycle
- NPHIES readiness
- Patient portal
- Barcode medication administration

## Phase 3
- HL7 FHIR API
- PACS/DICOM integration
- Advanced BI
- AI clinical documentation assistant
- AI revenue cycle assistant
- Telemedicine
- Mobile apps

## Acceptance Criteria
- Each patient can have multiple identifiers.
- Each clinical encounter must have financial traceability.
- Every chargeable item must create or prepare an invoice line.
- Every invoice line must trace back to encounter/order/provider/department.
- Clinical notes must be auditable and versioned.
- Roles must separate doctor, nurse, cashier, pharmacist, lab technician, radiologist, insurance officer, accountant, and administrator.
- No fake integrations. Use placeholder connector interfaces until official APIs are configured.

## Implementation Note
This product must be developed as multiple Odoo addons, not one large module.