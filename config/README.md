# Runtime configuration

The Mule application expects environment-specific properties from the configuration file referenced by the main Mule XML.

Required property groups include:

- db.sf.* — Snowflake connection settings
- email.* — SMTP settings
- aws.* — Amazon SNS settings
- http.requester.* — external notification request settings
- ultramsg.token — external notification token

Do not commit a real runtime configuration file containing credentials or tokens.

For local development, create the expected configuration file from your team's secure configuration source and keep it outside version control.

The repository's source flow is unchanged; this document only explains configuration ownership.
