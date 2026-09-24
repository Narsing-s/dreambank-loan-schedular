# Test Plan

The existing Mule business flow is intentionally unchanged. This document defines the safe test coverage that should be added or executed.

## Eligibility

| Test | Input balance | Expected loan type |
|---|---:|---|
| Home boundary | 500000 | HOME LOAN |
| Home above boundary | 500001 | HOME LOAN |
| Car boundary | 200000 | CAR LOAN |
| Car range | 499999 | CAR LOAN |
| Personal below boundary | 199999 | PERSONAL LOAN |
| Zero/default | 0 | PERSONAL LOAN |

## Duplicate prevention

Verify that an ACTIVE offer for the same account and loan type does not result in a second offer.

## Persistence

Verify that a newly generated offer contains:

- offer ID
- account number
- customer ID
- loan type
- offer amount
- interest rate
- tenure
- ACTIVE status
- creation timestamp
- expiry date

## Notifications

Use test recipients and test credentials. Verify email/SNS/HTTP notification behavior only in a non-production environment.

## Recommended automation

MUnit tests should cover the transformation and decision boundaries first. Integration tests should be used for Snowflake and external notification systems because those dependencies require environment-specific configuration.
