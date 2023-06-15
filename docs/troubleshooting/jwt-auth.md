# Troubleshooting JWT Authentication

Users are advised to test their algorithms for generating JWT Authentication headers by testing with [Hello World APIs](/docs/hello-world/jwt-auth.md). The Hello World APIs are able to validate the header and also generate the SHA-256 hash based on a given payload.

Error codes for JWT Authentication can be found [here](https://docs.developer.tech.gov.sg/docs/apex-cloud-troubleshooting-guide/docs/jwt/error-codes).

Also have you checked if your issue is in the [FAQ section](/docs/faq/jwt-auth.md)?

Do take note that if JWKS endpoint is specified, the user may need to validate that APEX has sufficient outwards connectivity to the JWKS endpoint and using [valid CA certificate authority](https://docs.developer.tech.gov.sg/docs/apex-cloud-troubleshooting-guide/docs/networking/networking-issues).
