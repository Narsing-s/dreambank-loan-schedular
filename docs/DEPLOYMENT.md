# Deployment Runbook

This guide documents deployment preparation without changing the existing Mule application flow.

## Pre-deployment

- Java 17 is available in the target environment.
- Mule runtime 4.9.0 is supported by the target runtime.
- Snowflake connectivity is available.
- SMTP configuration is available.
- AWS/SNS configuration is available when that notification path is enabled.
- External notification endpoint configuration is available where applicable.
- All credentials are supplied through secure deployment configuration.
- Synthetic validation data is ready.

## Package

From the repository root:

~~~
mvn clean package
~~~

The Mule Maven Plugin is configured in pom.xml.

## Deploy

Use the deployment method approved for the target environment, such as Anypoint Runtime Manager/CloudHub or Runtime Fabric.

Do not place deployment credentials in Git.

## Post-deployment verification

1. Confirm the application starts successfully.
2. Confirm the scheduler executes.
3. Confirm active customers can be read.
4. Validate an eligible synthetic customer.
5. Validate duplicate-offer behavior.
6. Verify LOAN_OFFERS.
7. Verify notification behavior in the configured test environment.
8. Verify EMAIL_HISTORY.
9. Review logs and correlation IDs.
10. Confirm no secrets or customer data appear in logs.

## Rollback

Use the previously verified application version in the target deployment platform. Record the deployment version and reason for rollback in the operational change record.
