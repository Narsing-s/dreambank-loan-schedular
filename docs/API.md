# Loan Offer API

## Purpose

The repository contains HTTP/API capability around the loan-offer solution. The current Mule application remains the source of truth for the actual endpoint configuration.

## Consumer documentation checklist

When the API is exposed in an environment, document:

- HTTP method
- Base URL
- Resource path
- Authentication/policy requirements
- Request headers
- Request parameters
- Response content type
- Success response
- Validation errors
- Dependency errors
- Example request and response using synthetic data

## Example response shape

Use synthetic values only when documenting or testing:

~~~
{
  "offerId": "OFF-202609250001",
  "accountNumber": "XXXXXX1234",
  "customerId": "CUST-001",
  "loanType": "HOME LOAN",
  "offerAmount": 5000000,
  "interestRate": 8.25,
  "tenure": 240,
  "status": "ACTIVE"
}
~~~

> The example above is documentation-only. It does not define or modify the application's current API contract.

## Recommended next contract step

If this API will be consumed by other applications, create an OpenAPI/RAML contract from the actual deployed endpoint rather than guessing the endpoint from screenshots.
