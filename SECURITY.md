# Security notes

This portfolio MVP has not undergone an independent security audit. Do not place real secrets or personal/financial records in public issues. Repository owners should configure a private vulnerability reporting channel before inviting external reports.

Production identity currently depends on the Sites gateway. On other hosting, replace or verify the identity boundary; do not trust user-supplied identity headers. Configure secrets in server runtime storage. The local simulated login is for loopback development only.

Financial and provider integrations require sandbox and production-readiness verification before live use. Automated tests mock external services; passing tests do not establish real financial settlement or message delivery.
