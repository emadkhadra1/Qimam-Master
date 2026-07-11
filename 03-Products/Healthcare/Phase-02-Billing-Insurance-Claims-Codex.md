# Qimam Healthcare - Phase 02 Billing, Insurance, Claims and Accounting Bridge

## Context

Phase 01 created the shared healthcare foundation for Hospital ERP and Clinic ERP.

Phase 02 must build the common financial and insurance backbone that both products will use.

## Objective

Build shared Odoo 19 Community modules for healthcare charge capture, accounting bridge, insurance workflow, claims lifecycle, and future NPHIES readiness.

## Important Rule

Do not duplicate billing or insurance logic in clinic or hospital modules.

Clinic ERP and Hospital ERP must both use the same shared models:
- qimam.healthcare.charge
- qimam.healthcare.insurance.company
- qimam.healthcare.insurance.policy
- qimam.healthcare.authorization
- qimam.healthcare.claim
- qimam.healthcare.claim.line

## Modules to Build

1. qimam_healthcare_billing_core
2. qimam_healthcare_accounting_bridge
3. qimam_healthcare_insurance_core
4. qimam_healthcare_claims_core
5. qimam_healthcare_integration_core

## Dependencies

These modules depend on:
- base
- mail
- product
- account if installed
- qimam_healthcare_base
- qimam_healthcare_patient
- qimam_healthcare_provider
- qimam_healthcare_encounter

Avoid Enterprise-only dependencies.

## Module 1 - qimam_healthcare_billing_core

### Purpose
Create a shared charge capture layer between clinical operations and accounting.

### Main Model
qimam.healthcare.charge

### Fields
- name
- patient_id
- encounter_id
- provider_id
- department_id
- branch_id
- product_id
- service_category
- quantity
- unit_price
- discount
- subtotal
- currency_id
- patient_share_amount
- insurance_share_amount
- insurance_policy_id
- authorization_id
- claim_id
- invoice_id
- invoice_line_id
- state: draft, confirmed, invoiced, cancelled
- notes

### Business Rules
- Charge must be linked to patient and product.
- If encounter exists, patient should be derived from encounter.
- Product price should populate unit price by default.
- Subtotal = quantity * unit_price - discount.
- Patient share + insurance share must not exceed subtotal.
- Only confirmed charges can be invoiced.
- Invoiced charges cannot be edited except by admin.

### Views
- Charge tree view
- Charge form view
- Charges by patient
- Charges by encounter
- Charges by doctor/provider
- Charges by department

### Buttons
- Confirm Charge
- Cancel Charge
- Reset to Draft
- Create Invoice

## Module 2 - qimam_healthcare_accounting_bridge

### Purpose
Create draft Odoo customer invoices from healthcare charges.

### Requirements
- Create draft account.move of type out_invoice.
- Customer should be linked to patient partner.
- Invoice lines must be created from confirmed charges.
- Do not post invoice automatically.
- After invoice creation, update charge state to invoiced.

### Required Traceability Fields on Invoice Line
Add custom fields to account.move.line:
- healthcare_patient_id
- healthcare_encounter_id
- healthcare_provider_id
- healthcare_department_id
- healthcare_charge_id
- healthcare_claim_id
- healthcare_insurance_policy_id

### Wizard
Create wizard:
qimam.healthcare.create.invoice.wizard

Wizard behavior:
- Select patient and/or encounter.
- Load confirmed uninvoiced charges.
- Allow user to select charge lines.
- Create draft invoice.
- Link invoice back to charges.

## Module 3 - qimam_healthcare_insurance_core

### Purpose
Manage insurance master data, patient policy, coverage, and authorizations.

### Models
qimam.healthcare.insurance.company
Fields:
- name
- code
- partner_id
- active
- contact details
- notes

qimam.healthcare.insurance.policy
Fields:
- name
- patient_id
- company_id
- policy_number
- member_id
- class_name
- network_name
- start_date
- end_date
- coverage_percent
- copay_percent
- deductible_amount
- active
- notes

qimam.healthcare.authorization
Fields:
- name
- patient_id
- encounter_id
- insurance_policy_id
- company_id
- authorization_number
- requested_amount
- approved_amount
- patient_share_amount
- insurance_share_amount
- status: draft, requested, approved, partially_approved, rejected, expired, cancelled
- request_date
- approval_date
- expiry_date
- rejection_reason
- external_reference

### Rules
- Policy must belong to one patient.
- Expired policies should not be used by default.
- Authorization can be linked to encounter and charge lines.

## Module 4 - qimam_healthcare_claims_core

### Purpose
Manage claim lifecycle internally before live payer/NPHIES integration.

### Models
qimam.healthcare.claim
Fields:
- name
- patient_id
- encounter_id
- insurance_policy_id
- company_id
- invoice_id
- authorization_id
- claim_date
- submitted_date
- state: draft, ready, submitted, accepted, partially_accepted, rejected, resubmitted, paid, closed, cancelled
- total_amount
- patient_share_amount
- insurance_share_amount
- paid_amount
- rejected_amount
- rejection_reason
- external_claim_id
- external_status
- notes

qimam.healthcare.claim.line
Fields:
- claim_id
- charge_id
- product_id
- quantity
- unit_price
- subtotal
- patient_share_amount
- insurance_share_amount
- approved_amount
- rejected_amount
- rejection_reason
- state

### Buttons
- Prepare Claim
- Submit Internally
- Mark Accepted
- Mark Rejected
- Resubmit
- Register Payment Reference
- Close Claim
- Cancel Claim

### Rules
- Claim lines are generated from invoiced or confirmed insurance-covered charges.
- Claim totals must match claim lines.
- Claim must link back to invoice and charges.

## Module 5 - qimam_healthcare_integration_core

### Purpose
Prepare for NPHIES, payer APIs, FHIR, PACS, payment gateways, SMS/WhatsApp without implementing live integrations now.

### Models
qimam.healthcare.integration.endpoint
Fields:
- name
- integration_type: nphies, payer, fhir, pacs, sms, whatsapp, payment, other
- base_url
- environment: test, production
- active
- auth_type
- notes

qimam.healthcare.integration.message
Fields:
- name
- endpoint_id
- related_model
- related_res_id
- direction: inbound, outbound
- operation
- status: draft, queued, sent, success, failed, cancelled
- request_payload
- response_payload
- request_date
- response_date
- error_message

qimam.healthcare.integration.log
Fields:
- message_id
- level
- message
- timestamp

qimam.healthcare.external.reference
Fields:
- model_name
- res_id
- external_system
- external_id
- external_status
- last_sync_date

### Rules
- Do not hardcode real endpoints.
- All connectors disabled by default.
- Provide demo endpoint only.
- Protect sensitive payloads with proper access rules.

## Security Groups
- Healthcare Billing User
- Healthcare Billing Manager
- Healthcare Insurance Officer
- Healthcare Claims Officer
- Healthcare Accountant
- Healthcare Integration Admin
- Healthcare Admin

## Menus
Create menu structure:
Healthcare
- Billing
  - Charges
  - Create Invoice Wizard
  - Invoices
- Insurance
  - Insurance Companies
  - Patient Policies
  - Authorizations
- Claims
  - Claims
  - Claim Lines
- Integration
  - Endpoints
  - Messages
  - Logs
  - External References
- Configuration
  - Service Categories

## Reports / Dashboards
Add basic pivot/list reports:
- Revenue by doctor/provider
- Revenue by department
- Revenue by service category
- Patient share vs insurance share
- Claims by status
- Rejected claims
- Uninvoiced charges

## Demo Data
Create demo data:
- 2 insurance companies
- 3 patients with policies
- 5 products/services
- 2 encounters
- several charge lines
- 1 authorization
- 1 draft claim

## Acceptance Criteria
- User can create healthcare charge linked to patient/product.
- User can confirm charges.
- User can create draft customer invoice from charges.
- Invoice lines contain healthcare traceability fields.
- User can create patient insurance policy.
- User can create authorization.
- User can create claim from charge lines.
- Claim totals are calculated correctly.
- Integration placeholder records can be created without calling external systems.
- Clinic and hospital modules can reuse these shared modules without duplicated logic.

## Do Not Do
- Do not implement live NPHIES API.
- Do not implement real payer submission.
- Do not post invoices automatically.
- Do not add clinical diagnosis AI.
- Do not build patient mobile app in this phase.
- Do not depend on Odoo Enterprise modules.