# Dream Bank Loan Scheduler — Requirements Specification

## 1. Purpose

This document describes the functional, integration, data, notification, security, and operational requirements implemented by the current MuleSoft application.

**Source of truth:** the existing Mule application flow and configuration. This document does not introduce new business behavior.

## 2. Scope

The solution automates pre-approved loan-offer processing for active bank customers.

Flow: Scheduler → active customers from Snowflake → eligibility → active-offer check → offer generation → Snowflake persistence → notifications → email audit → logging.

## 3. Actors and Systems

| Actor/System | Responsibility |
|---|---|
| Mule Scheduler | Starts recurring processing |
| Mule application | Orchestrates eligibility, duplicate checking, offer creation and notifications |
| Snowflake | Customer, offer and email-history persistence |
| SMTP server | Sends loan-offer email |
| Amazon SNS | Sends SMS notification |
| HTTP notification service | Sends the configured external notification |
| Operations team | Monitors logs, dependencies and deployments |

## 4. Functional Requirements

### FR-01 — Scheduled execution
The application shall start loan-offer processing through the Mule Scheduler using the configured scheduling strategy.

### FR-02 — Active customer retrieval
The application shall retrieve customers from BANK_CUSTOMER_DATA whose status is ACTIVE.

### FR-03 — Customer-level processing
The application shall process retrieved customers individually.

### FR-04 — Loan eligibility

| Balance | Loan Type |
|---:|---|
| >= ₹500,000 | HOME LOAN |
| >= ₹200,000 and < ₹500,000 | CAR LOAN |
| < ₹200,000 | PERSONAL LOAN |

A missing/null balance is treated as zero by the current transformation.

### FR-05 — Current offer configuration

| Loan Type | Offer Amount | Interest Rate | Tenure |
|---|---:|---:|---:|
| HOME LOAN | ₹5,000,000 | 8.25% | 240 months |
| CAR LOAN | ₹1,000,000 | 9.25% | 84 months |
| PERSONAL LOAN | ₹200,000 | 11.50% | 60 months |

### FR-06 — Active-offer check
Before creating an offer, the application shall query LOAN_OFFERS using account number, loan type and ACTIVE status.

### FR-07 — Offer generation
A generated offer shall contain offer ID, account number, customer ID, customer name, email, mobile number, balance, loan type, offer amount, interest rate and tenure.

### FR-08 — Offer identifier
The current implementation generates an identifier using the OFF- prefix and the current timestamp.

### FR-09 — Offer persistence
New offers shall be inserted into LOAN_OFFERS with ACTIVE status, creation timestamp and an expiry date one month from creation.

### FR-10 — Email notification
The application shall generate an HTML loan-offer email and send it through SMTP. The customer-facing email masks the account number and presents loan type, amount, interest rate and tenure.

### FR-11 — SMS notification
The application shall publish a notification through Amazon SNS using the customer's mobile number.

### FR-12 — HTTP notification
The application shall call the configured HTTP notification service with customer and offer notification details.

### FR-13 — Email audit
The application shall create an EMAIL_HISTORY record containing email ID, account number, email address, subject, status and timestamp.

### FR-14 — Existing offer handling
When an applicable existing active offer is identified, the flow shall notify the customer rather than create another offer.

## 5. Data Requirements

### 5.1 Customer data

The flow consumes:
- CUSTOMER_ID
- FULLNAME
- ACCOUNTNUMBER
- EMAIL
- MOBILENUMBER
- BANKNAME
- BALANCE
- STATUS

### 5.2 Loan offer data

LOAN_OFFERS stores:
- OFFER_ID
- ACCOUNTNUMBER
- CUSTOMERID
- LOAN_TYPE
- OFFER_AMOUNT
- INTEREST_RATE
- TENURE
- STATUS
- CREATED_AT
- EXPIRE_DATE

### 5.3 Email history

EMAIL_HISTORY records:
- Email ID
- Account number
- Email
- Subject
- Status
- Timestamp

## 6. Integration Requirements

### Snowflake
Requires account, warehouse, database, schema, user, password and role configuration.

### SMTP
Requires SMTP host, port, username, password and provider-specific properties.

### Amazon SNS
Requires AWS access credentials and region configuration.

### HTTP notification
Requires HTTP host, method, path and notification token configuration.

## 7. Configuration Requirements

The application uses these configuration groups:
- db.sf.*
- email.*
- aws.*
- http.requester.*
- ultramsg.token

Production credentials and tokens shall not be committed to Git.

## 8. Non-Functional Requirements

### NFR-01 — Traceability
Mule logs shall provide information suitable for execution tracing and correlation-ID based investigation.

### NFR-02 — Security
Credentials and access tokens shall not be committed to source control or unnecessarily exposed in logs.

### NFR-03 — Maintainability
Environment-specific configuration shall remain externalized from business logic.

### NFR-04 — Deployability
The project is configured for Maven packaging with Java 17 and Mule runtime 4.9.0.

## 9. Business Rules

1. Only ACTIVE customers are selected.
2. Balance determines loan category.
3. An ACTIVE offer is checked before creating a new offer.
4. New offers are persisted as ACTIVE.
5. Offer expiry is calculated as one month after creation.
6. Account numbers are masked in customer-facing notifications.
7. Configured email, SNS and HTTP integrations are used for notifications.

## 10. End-to-End Flow

~~~mermaid
flowchart TD
    A[Scheduler] --> B[Read ACTIVE customers]
    B --> C[Process customer]
    C --> D[Determine loan type]
    D --> E[Check existing ACTIVE offer]
    E -->|No applicable offer| F[Generate loan offer]
    F --> G[Persist LOAN_OFFERS]
    G --> H[Email]
    G --> I[Amazon SNS]
    G --> J[HTTP notification]
    H --> K[Persist EMAIL_HISTORY]
    E -->|Existing offer| L[Notify existing offer]
~~~

## 11. Acceptance Criteria

- An ACTIVE customer can be retrieved.
- The correct loan category is derived from balance.
- Existing ACTIVE offers are detected using account and loan type.
- A new offer contains the required attributes.
- The offer is persisted with expected status and expiry.
- Configured notification integrations receive the appropriate message.
- Email history is persisted.
- Execution can be traced through Mule logs.

## 12. Out of Scope

The current implementation does not define:
- Credit-score evaluation
- KYC verification
- Loan disbursement
- Customer authentication
- Human approval workflow
- Dynamic interest-rate calculation
- Production banking-core integration
- A new API contract beyond behavior already present in the repository

## 13. Source Alignment

This specification was derived from the current repository implementation. If the Mule flow changes later, this document should be reviewed so the requirements remain synchronized with implementation.
