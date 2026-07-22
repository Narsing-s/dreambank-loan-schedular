# 🏦 Dream Bank Loan Scheduler API

## Project Overview

The **Dream Bank Loan Scheduler API** is a MuleSoft-based automation project that generates **pre-approved loan offers** for eligible bank customers. The application runs on a scheduled interval, retrieves active customer data from Snowflake, evaluates loan eligibility based on account balance, generates personalized loan offers, stores them in the database, and sends professional HTML email notifications.

The project prevents duplicate loan offers by validating existing active offers before creating new ones and maintains a complete email history for auditing and reporting.

---

## Features

- ⏰ Automated scheduler for loan offer generation
- <img width="2523" height="489" alt="dreambank-loan-scheduler-ss" src="https://github.com/user-attachments/assets/25e61e73-89cd-45e9-b13b-8c2cc4338529" />

- 👤 Retrieves active customer records from Snowflake
- <img width="1800" height="210" alt="image" src="https://github.com/user-attachments/assets/faf4d00f-706c-48c3-a320-ca1e184b4ca3" />

- 💰 Determines loan eligibility based on account balance
- <img width="1752" height="157" alt="image" src="https://github.com/user-attachments/assets/9e4b38b3-f00d-4d00-bd5d-10859bbcd911" />

- 🏠 Supports Home Loan, Car Loan, and Personal Loan offers
- <img width="1746" height="215" alt="image" src="https://github.com/user-attachments/assets/4cfca54e-aca3-4c37-9163-a83be05a4abe" />

- 🆔 Generates unique loan offer IDs
- <img width="657" height="77" alt="image" src="https://github.com/user-attachments/assets/3b0e8571-016f-4fab-9dce-f4eb72203a4f" />

- 💾 Stores loan offers in the `LOAN_OFFERS` table
- <img width="1737" height="197" alt="image" src="https://github.com/user-attachments/assets/6f12d1db-fe0e-4913-9138-7a0b26a73360" />

- 🚫 Prevents duplicate active loan offers
- <img width="961" height="112" alt="image" src="https://github.com/user-attachments/assets/0e6262d1-9425-47e9-b0cb-81a2e17782f2" />

- 📧 Sends personalized HTML email notifications
- <img width="1871" height="830" alt="image" src="https://github.com/user-attachments/assets/6054d502-a005-46a8-b86f-34a47bce6963" />

- 📜 Maintains email history in the `EMAIL_HISTORY` table
- <img width="1702" height="271" alt="image" src="https://github.com/user-attachments/assets/6c8daa3a-4902-4c51-b9e7-a75c6d7fa9c0" />
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
