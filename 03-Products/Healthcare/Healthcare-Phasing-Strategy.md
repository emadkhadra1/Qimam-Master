# Healthcare Product Phasing Strategy

## Purpose

This document defines whether Qimam Technology should start Insurance/Claims, NPHIES readiness, AI, Patient Portal, and Mobile App together with the first healthcare modules.

## Executive Decision

Do not build everything fully in the first sprint.

Build the core foundations now, but postpone advanced live integrations and advanced AI/mobile features until the clinical and financial base is stable.

## Phase 1 - Must Start Now

### Core Clinical and Financial Foundation
- Patient master data
- Appointments
- Encounters
- Doctors workbench
- Services and procedures
- Charge capture
- Cash billing
- Basic insurance fields
- Invoice creation bridge
- Accounting traceability

### Why
Insurance, AI, portal, and mobile app all depend on accurate patient, encounter, billing, and authorization data.

## Insurance/Claims

### What It Means
Insurance/Claims covers the full revenue cycle related to insured patients:

- Insurance company master data
- Insurance policy
- Coverage class
- Network
- Eligibility reference
- Pre-authorization request
- Approval number
- Patient share
- Insurance share
- Claim creation
- Claim lines
- Claim submission status
- Rejection/denial reasons
- Resubmission
- Remittance
- Reconciliation with accounting

### Start Now?
Yes, but as internal insurance workflow only.

### Build Now
- Insurance company
- Insurance policy
- Patient policy
- Approval reference
- Patient share / insurance share
- Claim draft
- Claim status
- Link claim to invoice

### Postpone
- Real electronic claim submission
- Automated remittance
- Official payer integration
- Complex contract pricing engine

## NPHIES Readiness

### What It Means
NPHIES readiness means preparing the system data architecture and integration layer so it can later connect to Saudi national health insurance / health information exchange requirements when official integration documentation and testing access are available.

### Start Now?
Yes, as readiness only.

### Build Now
- Integration placeholder module
- Endpoint configuration model
- Message log model
- External reference fields
- Code system mapping
- Claim external ID
- Eligibility external ID
- Authorization external ID
- Request/response log structure
- Disabled-by-default connectors

### Postpone
- Live NPHIES integration
- Production endpoints
- Official API calls
- Certification claims
- Hardcoded formats not verified by official documentation

## AI

### What It Means
AI should support operations, documentation, reporting, and decision assistance. It must not act as an unsupervised medical decision maker.

### Start Now?
Start only the AI architecture and non-clinical/admin AI helpers.

### Build Now
- AI settings model
- AI prompt templates
- AI log model
- AI permissions
- Draft clinical note summarization placeholder
- Billing anomaly assistant placeholder
- Patient communication assistant placeholder

### Postpone
- Diagnosis suggestion
- Treatment recommendation
- Medication recommendation
- Any unsupervised clinical decision-making

## Patient Portal

### What It Means
Patient Portal allows the patient to access digital services:

- Appointments
- Visit summaries
- Invoices and payments
- Lab results
- Radiology reports
- Prescriptions
- Follow-up requests
- Consent forms

### Start Now?
Design now, build after MVP.

### Build Now
- Portal access flags
- Patient email/mobile fields
- Consent fields
- Secure document references
- Portal-ready data model

### Postpone
- Full patient login UX
- Online payment
- Result publishing workflows
- Patient mobile notifications

## Mobile App

### What It Means
Mobile app can target different audiences:

1. Patient app
2. Doctor app
3. Nurse app
4. Admin/manager app

### Start Now?
Do not build the mobile app now.

### Build Now
- API-ready backend structure
- Clean state workflows
- Access control
- REST/FHIR-ready service layer placeholders

### Postpone
- Flutter app
- Native mobile features
- Push notifications
- Offline mode

## Recommended Development Order

1. Clinic ERP MVP
2. Hospital ERP OPD + Billing
3. Basic Insurance Workflow
4. Pharmacy / Lab / Radiology
5. Inpatient and Nursing
6. Claim lifecycle
7. NPHIES readiness layer
8. Patient Portal
9. Mobile App
10. AI assistants

## Codex Rule

Do not build live integrations until business workflows, accounting traceability, and official API documentation are available.

Build foundations and placeholders first, then implement real integrations in separate modules.