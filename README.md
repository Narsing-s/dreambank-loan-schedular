# 🏦 Dream Bank Loan Scheduler API

## Project Overview

The **Dream Bank Loan Scheduler API** is a MuleSoft-based automation project that generates **pre-approved loan offers** for eligible bank customers. The application runs on a scheduled interval, retrieves active customer data from Snowflake, evaluates loan eligibility based on account balance, generates personalized loan offers, stores them in the database, and sends professional HTML email notifications.

The project prevents duplicate loan offers by validating existing active offers before creating new ones and maintains a complete email history for auditing and reporting.

---

## Features

- ⏰ Automated scheduler for loan offer generation
- 👤 Retrieves active customer records from Snowflake
- 💰 Determines loan eligibility based on account balance
- 🏠 Supports Home Loan, Car Loan, and Personal Loan offers
- 🆔 Generates unique loan offer IDs
- 💾 Stores loan offers in the `LOAN_OFFERS` table
- 🚫 Prevents duplicate active loan offers
- 📧 Sends personalized HTML email notifications
- 📜 Maintains email history in the `EMAIL_HISTORY` table
- 📊 Detailed logging for monitoring and troubleshooting

---

## Technology Stack

- MuleSoft 4
- DataWeave 2.0
- Snowflake Database
- Gmail SMTP
- Mule Scheduler
- Snowflake Connector
- Email Connector

---

## Business Flow

1. Scheduler triggers automatically.
2. Fetch active customer records from Snowflake.
3. Evaluate customer loan eligibility.
4. Check for existing active loan offers.
5. Generate a new loan offer if eligible.
6. Save the loan offer to the database.
7. Generate a professional HTML email.
8. Send the email to the customer.
9. Store email transaction details in the database.
10. Log the execution for monitoring.

---

## Loan Eligibility Rules

| Account Balance | Loan Type | Offer Amount | Interest Rate | Tenure |
|-----------------|-----------|-------------:|--------------:|--------:|
| ₹5,00,000 or above | Home Loan | ₹50,00,000 | 8.25% | 240 Months |
| ₹2,00,000 – ₹4,99,999 | Car Loan | ₹10,00,000 | 9.25% | 84 Months |
| Below ₹2,00,000 | Personal Loan | ₹2,00,000 | 11.50% | 60 Months |

---

## Database Tables

- `BANK_CUSTOMER_DATA`
- `LOAN_OFFERS`
- `EMAIL_HISTORY`

---

## Project Highlights

- Fully automated loan offer generation
- Personalized customer communication
- Duplicate offer prevention
- Email audit and tracking
- Secure Snowflake integration
- Scalable MuleSoft architecture

---

## Future Enhancements

- SMS and WhatsApp notifications
- REST API to view loan offers
- PDF loan offer generation
- Dashboard and reporting
- Multi-channel customer notifications
- API security using OAuth 2.0

---

## Author

**Narsing Rao Beesetti**  
MuleSoft Developer | Integration Engineer
