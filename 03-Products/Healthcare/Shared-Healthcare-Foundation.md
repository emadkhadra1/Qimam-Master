# Shared Healthcare Foundation Strategy

## Purpose

Qimam Hospital ERP and Qimam Clinic ERP must not be built as isolated systems. They should share a common healthcare foundation so both products remain integrated, scalable, and reusable.

## Executive Decision

Start the shared foundation immediately.

Do not build AI, Patient Portal, Mobile App, or live NPHIES integration fully in the first sprint. Instead, build the shared backend structures that make all of them possible later without redesign.

## Shared Foundation Modules

These modules should be common and reusable by both Hospital ERP and Clinic ERP:

1. qimam_healthcare_base
2. qimam_healthcare_patient
3. qimam_healthcare_coding
4. qimam_healthcare_provider
5. qimam_healthcare_appointment
6. qimam_healthcare_encounter
7. qimam_healthcare_billing_core
8. qimam_healthcare_insurance_core
9. qimam_healthcare_claims_core
10. qimam_healthcare_integration_core
11. qimam_healthcare_portal_core
12. qimam_healthcare_ai_core
13. qimam_healthcare_api_core
14. qimam_healthcare_audit

## Product-Specific Modules

### Clinic Product Modules
- qimam_clinic_ui
- qimam_clinic_packages
- qimam_clinic_commission
- qimam_clinic_dashboard

### Hospital Product Modules
- qimam_hospital_opd
- qimam_hospital_inpatient
- qimam_hospital_nursing
- qimam_hospital_pharmacy
- qimam_hospital_laboratory
- qimam_hospital_radiology
- qimam_hospital_or
- qimam_hospital_dashboard

## Shared Patient Model

There must be one patient data model used across clinic and hospital modules.

Model:
qimam.healthcare.patient

Requirements:
- Multiple identifiers
- National ID / Iqama / Passport readiness
- Mobile and email
- Date of birth
- Gender
- Emergency contact
- Insurance policies
- Portal access flag
- Consent records
- Medical alerts
- Patient documents

## Shared Encounter Model

There must be one encounter model used for clinic visits, hospital OPD visits, emergency visits, and inpatient episodes.

Model:
qimam.healthcare.encounter

Required fields:
- Patient
- Encounter type: clinic, OPD, emergency, inpatient, telemedicine
- Provider
- Department
- Branch
- Start date
- End date
- State
- Diagnosis
- Orders
- Charges
- Invoice
- Claim

## Shared Billing Core

All clinical and operational charges should flow through one charge model before invoicing.

Model:
qimam.healthcare.charge

Required fields:
- Patient
- Encounter
- Product
- Service category
- Provider
- Department
- Quantity
- Unit price
- Discount
- Patient share
- Insurance share
- Claim reference
- Invoice line reference

## Shared Insurance Core

Insurance must be a shared foundation across clinic and hospital products.

Models:
- qimam.healthcare.insurance.company
- qimam.healthcare.insurance.policy
- qimam.healthcare.insurance.coverage
- qimam.healthcare.authorization
- qimam.healthcare.claim
- qimam.healthcare.claim.line

Start with internal workflow only.

## NPHIES Readiness Core

Build readiness now, not live integration.

Models:
- qimam.healthcare.integration.endpoint
- qimam.healthcare.integration.message
- qimam.healthcare.integration.log
- qimam.healthcare.external.reference
- qimam.healthcare.code.mapping

Fields to add to relevant objects:
- external_id
- external_system
- external_status
- external_request_id
- external_response_id
- last_sync_date

## AI Core

Build AI infrastructure now, not clinical AI automation.

Models:
- qimam.healthcare.ai.provider
- qimam.healthcare.ai.prompt.template
- qimam.healthcare.ai.request
- qimam.healthcare.ai.response
- qimam.healthcare.ai.audit

Rules:
- AI must be permission-controlled.
- AI must log prompts and responses.
- AI must not make final medical decisions.
- AI output must be draft/recommendation only.

Initial safe AI uses:
- Visit summary draft
- Patient file summary
- Billing anomaly explanation
- Claim rejection explanation
- Management report summary
- Patient message draft

## Portal Core

Build portal readiness now.

Patient portal should later support:
- Appointment requests
- Visit summaries
- Prescriptions
- Lab results
- Radiology reports
- Invoices
- Payments
- Consent forms

Build now:
- Portal access flag
- Publish-to-portal flags
- Patient document visibility
- Secure token model placeholder

## API Core

Build backend API readiness for future mobile app and portal.

Models / services:
- API access token placeholder
- API log
- API permission scope
- API response wrapper

Do not expose public APIs until security review.

## Codex Instruction

Start by building shared healthcare foundation modules before product-specific modules.

The Clinic ERP and Hospital ERP must depend on the shared modules, not duplicate patient, billing, insurance, claim, AI, portal, or integration logic.

## Development Order

1. Shared base
2. Patient
3. Provider and departments
4. Coding
5. Appointment
6. Encounter
7. Billing core
8. Insurance core
9. Claims core
10. Accounting bridge
11. Clinic UI modules
12. Hospital OPD modules
13. Pharmacy/Lab/Radiology
14. Inpatient
15. Portal core
16. AI core
17. API core
18. Live integrations