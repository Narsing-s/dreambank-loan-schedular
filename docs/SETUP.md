# Setup and Run Guide

## Prerequisites

- Java 17
- Maven
- Anypoint Studio compatible with the project's Mule runtime
- Snowflake account/database
- SMTP/email configuration
- Credentials/configuration supplied through secure environment properties

The application declares Mule runtime 4.9.0 and Java 17 in `mule-artifact.json`.

## Build

From the repository root:

```bash
mvn clean package
```

For local development, import the project into Anypoint Studio and configure environment-specific connection properties before running it.

## Configuration checklist

Do not commit secrets.

Configure, through the project's existing Mule configuration mechanism:

1. Snowflake connection details.
2. Database/schema/table names.
3. Scheduler interval.
4. Email/SMTP credentials and sender settings.
5. Notification configuration where applicable.
6. HTTP listener/API settings where applicable.

## Verification checklist

After starting the application:

- Confirm the scheduler executes.
- Confirm active customers can be read.
- Validate the eligibility branch with representative test data.
- Verify duplicate active offers are not recreated.
- Verify a new offer is persisted.
- Verify notification processing.
- Verify notification history is persisted.
- Review Mule logs for correlation and error details.

## Production safety

Use secrets from secure deployment properties or a secrets manager. Never place passwords, SMTP credentials, Snowflake keys, tokens, or customer data in source control.
