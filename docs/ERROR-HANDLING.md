# Error Handling and Operational Behavior

This document describes how to review failures around the existing flow without changing its business logic.

## Failure areas

| Area | What to verify | Operational action |
|---|---|---|
| Scheduler | Job starts at the configured interval | Check Mule application logs |
| Snowflake read | Active customers are returned | Verify connectivity, database, schema and permissions |
| Eligibility | Customer follows the intended balance branch | Test with synthetic boundary values |
| Duplicate check | Existing ACTIVE offer is detected | Verify account number, loan type and status |
| Offer insert | New offer is persisted | Check LOAN_OFFERS and database permissions |
| Email | Notification is accepted by SMTP | Check SMTP configuration and provider response |
| SNS | SMS publish succeeds | Check AWS credentials, region and SNS permissions |
| HTTP notification | External notification request succeeds | Check endpoint, token configuration and response |
| Email history | Audit row is inserted | Check EMAIL_HISTORY and database permissions |

## Observability

The application already uses Mule loggers and a Log4j2 pattern containing the Mule processor path and correlation ID. Use those values when tracing an execution.

## Troubleshooting sequence

1. Identify the scheduler execution in the Mule logs.
2. Capture the correlation ID.
3. Determine whether the failure occurred before or after offer persistence.
4. Check the relevant external dependency.
5. Verify configuration without printing secrets.
6. Re-run with synthetic data after the dependency is restored.

## Security rule

Never put credentials, access tokens, or customer information into logs or issue reports.
