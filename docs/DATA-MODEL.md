# Data Model

The project documents three logical persistence areas.

## BANK_CUSTOMER_DATA

Stores the active customer information used by the scheduler.

Typical logical attributes:

- Customer identifier
- Customer name
- Email/contact information
- Account balance
- Active/customer status

## LOAN_OFFERS

Stores generated pre-approved offers.

Typical logical attributes:

- Loan offer identifier
- Customer identifier
- Loan type
- Offer amount
- Interest rate
- Tenure
- Offer status
- Created timestamp

## EMAIL_HISTORY

Stores notification/audit information.

Typical logical attributes:

- Customer identifier
- Loan offer identifier
- Recipient
- Notification status
- Notification timestamp
- Error/detail information where applicable

## Relationship

```text
BANK_CUSTOMER_DATA
       |
       | customer_id
       v
   LOAN_OFFERS
       |
       | loan_offer_id
       v
  EMAIL_HISTORY
```

The exact physical schema should be treated as environment-specific and configured in the target Snowflake environment.
