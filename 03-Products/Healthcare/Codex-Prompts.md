# Qimam Healthcare Codex Prompts

## Prompt 1 - Qimam Hospital ERP Foundation

Build an Odoo 19 Community modular healthcare platform named Qimam Hospital ERP.

Architecture rules:
- Do not create one huge module.
- Create a modular addon architecture.
- Use clean Odoo ORM models.
- Use security groups and record rules.
- Support Arabic and English translation files.
- Avoid Enterprise-only dependencies.
- Integrate with Odoo accounting through account.move and product.product when accounting is installed.

Required addons:
1. qimam_healthcare_base
2. qimam_healthcare_patient
3. qimam_healthcare_appointment
4. qimam_healthcare_emr
5. qimam_healthcare_billing
6. qimam_healthcare_insurance
7. qimam_healthcare_pharmacy
8. qimam_healthcare_laboratory
9. qimam_healthcare_radiology
10. qimam_healthcare_inpatient
11. qimam_healthcare_inventory
12. qimam_healthcare_accounting_bridge
13. qimam_healthcare_dashboard
14. qimam_healthcare_integration

Start with Phase 1 only:
- Base master data
- Patient registration
- Appointments
- OPD encounter
- Diagnosis
- Prescription
- Lab order
- Radiology order
- Healthcare charges
- Invoice creation bridge
- Security groups
- Menus and views
- Demo data

Core models:
- qimam.healthcare.patient
- qimam.healthcare.patient.identifier
- qimam.healthcare.provider
- qimam.healthcare.department
- qimam.healthcare.specialty
- qimam.healthcare.encounter
- qimam.healthcare.appointment
- qimam.healthcare.diagnosis
- qimam.healthcare.prescription
- qimam.healthcare.lab.order
- qimam.healthcare.radiology.order
- qimam.healthcare.charge

Accounting bridge requirements:
- Healthcare service must map to product.product.
- Charge lines should generate draft customer invoice account.move.
- Invoice line must carry patient, encounter, provider, department, and service reference fields.
- Do not post invoices automatically.

Security groups:
- Healthcare Admin
- Doctor
- Nurse
- Receptionist
- Cashier
- Insurance Officer
- Lab Technician
- Radiology Technician
- Pharmacist
- Accountant

UI requirements:
- Add Healthcare app root menu.
- Add Patient smart buttons for appointments, encounters, invoices, lab, radiology, prescriptions.
- Add Kanban/list/form views.
- Add basic dashboards.

Technical quality:
- Use state machines for appointment and encounter.
- Add chatter tracking.
- Add audit fields.
- Add constraints for patient identity and appointment time conflicts.
- Add demo data for one hospital, departments, doctors, patients, services, and charges.

Do not implement external NPHIES/FHIR/PACS APIs now. Create placeholder connector models and interface methods only.

## Prompt 2 - Qimam Clinic ERP MVP

Build an Odoo 19 Community addon suite named Qimam Clinic ERP for private clinics and medical centers.

Architecture:
- Lightweight compared to hospital ERP.
- SaaS-ready.
- Easy onboarding.
- Arabic/English support.
- Integrates with Odoo invoices and payments.

Required addons:
1. qimam_clinic_base
2. qimam_clinic_patient
3. qimam_clinic_appointment
4. qimam_clinic_emr
5. qimam_clinic_billing
6. qimam_clinic_packages
7. qimam_clinic_insurance
8. qimam_clinic_inventory
9. qimam_clinic_dashboard

MVP features:
- Patient profile
- Appointment booking
- Queue management
- Doctor consultation
- Diagnosis and prescription
- Medical services and procedures
- Cash billing
- Insurance approval reference
- Package sales and session consumption
- Basic consumables deduction
- Doctor commission report
- Daily revenue dashboard

Core models:
- qimam.clinic.patient
- qimam.clinic.appointment
- qimam.clinic.encounter
- qimam.clinic.prescription
- qimam.clinic.service.order
- qimam.clinic.charge
- qimam.clinic.package
- qimam.clinic.package.line
- qimam.clinic.insurance.policy
- qimam.clinic.claim
- qimam.clinic.commission

Accounting:
- Map consultation/procedure/package to product.product.
- Create customer invoices from charge lines.
- Support patient share and insurance share fields.
- Add analytic tags/cost centers by branch, doctor, and department where possible.

Views:
- Clinic app root menu.
- Reception dashboard.
- Doctor worklist.
- Patient form with smart buttons.
- Appointment calendar.
- Queue board.
- Encounter form.
- Billing wizard.
- Package consumption form.

Security groups:
- Clinic Admin
- Receptionist
- Doctor
- Nurse
- Cashier
- Insurance Officer
- Accountant

Acceptance:
- A receptionist can register a patient and book appointment.
- A doctor can open the encounter and write diagnosis/prescription.
- A cashier can create invoice from visit charges.
- A clinic manager can see daily revenue, visits, doctor productivity, and unpaid invoices.
- Package sessions can be sold and consumed with full traceability.

## Prompt 3 - Common Healthcare Coding Standards

For both Hospital ERP and Clinic ERP, implement reusable healthcare coding master data.

Create a module:
qimam_healthcare_coding

Models:
- qimam.healthcare.code.system
- qimam.healthcare.code
- qimam.healthcare.diagnosis.code
- qimam.healthcare.procedure.code
- qimam.healthcare.lab.code
- qimam.healthcare.medication.code

Support code systems:
- ICD-10 / ICD-11 readiness
- CPT/local procedure codes readiness
- LOINC readiness
- SNOMED CT readiness
- Internal hospital service codes

Rules:
- Do not load copyrighted code databases unless provided by the client.
- Provide demo codes only.
- Make code system extensible.
- Add fields for external code, display name, Arabic name, English name, active, version, and effective date.

## Prompt 4 - Future Integration Layer

Create healthcare integration placeholder framework.

Module:
qimam_healthcare_integration

Purpose:
Prepare for future integration without implementing real external APIs now.

Connectors:
- FHIR Connector placeholder
- NPHIES Connector placeholder
- PACS/DICOM Connector placeholder
- SMS/WhatsApp Connector placeholder
- Payment Gateway Connector placeholder
- E-prescription Connector placeholder

Models:
- qimam.healthcare.integration.endpoint
- qimam.healthcare.integration.message
- qimam.healthcare.integration.log
- qimam.healthcare.fhir.mapping

Requirements:
- Store request/response logs safely.
- Mask patient-sensitive data where possible.
- Add retry status.
- Add connector configuration records.
- Do not hardcode production endpoints.
- Keep all connectors disabled by default.