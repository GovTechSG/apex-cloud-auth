# Frequently Asked Questions

## Useful information

<br>**Q.** Does the "aud" claim require query parameters?
<br>**A.** "aud" claim is defined to exclude query parameters.

<br>**Q.** Does Hello World Api exist in intranet?
<br>**A.** Yes, Hello World exists both in internet and intranet zone, with domains public-stg.api.gov.sg and gw-stg.int.api.gov.sg.

<br>**Q.** How do we carry out rotation of keys (JWK)?
<br>**A.** As the consumer, your application would be involved in signing of the JWT using the private key.
<br>Generate a new key with a new Key ID and add it to the JWKS endpoint ahead of time.  When the key is rotated, sign with the key with the new Key ID.
<br>Do note however that JWKS caching in APEX servers is 1 hour hence it is still recommended to automate this for an off-peak rotation.

<br>**Q.** How do we carry out automatic rotation of keys (JWK)?
<br>**A.** As the consumer, your application would be involved in signing of the JWT using the private key.
<br>Hence if your organization is able to host the public key in the form of a JWKS endpoint, you would be able to update the JWKS endpoint whenever you create a new private key for signing. Hence key rotation can be effected programatically with no human intervention.
<br>Do note however that JWKS caching in APEX servers is 1 hour hence you would have to update the JWKS endpoint at least an hour in advance.

## Troubleshooting

<br>**Q.** How do we troubleshoot **error 446 (incorrect data hash)**?
<br>**A.** Error 446 may mean that your data hash of your body is incorrect. Ensure that your data is [formatted correctly](docs/dev/jwt-auth?id=apex-standardized-json-payload) (generally without spaces and carriage returns/new lines) and do test your hash values with [Hello World APIs](docs/hello-world/jwt-auth?id=sha-256-generator) /helloworld/sha256 with x-apex-returncontent and seeing the return value of x-apex-hash and the content returned.

If you are using SOAP and are still having this error, do contact open a case with APEX.

<br>**Q.** How do we troubleshoot **error 441 (invalid iat claim)**?
<br>**A.** This could be due to the "iat" issued at time claim, which is in the future compared to date/time of APEX.

There could be time skew at the Consumer's server/application causing it to be earlier than universal NTP servers, hence the Consumer server needs to be checked that it is synced correctly to global NTP clocks.

<br>**Q.** How do we troubleshoot **error 443 (JWT Header Missing)**?
<br>**A.** The JWT header is not reaching APEX. Do register a new backend by going to this URL https://webhook.site and with the registered backend (eg. https://webhook.site/123456-1234-1234-1234-1234567890), use your application to call this. From your registered URL, you will be able to see if the header x-apex-jwt is indeed reaching the backend.

<br>**Q.** How do we troubleshoot **error 433 (Invalid JWKS)**?
<br>**A.** Do check that the JWKS is formatted correct in JSON (use only double quotes, key values need to be double-quoted, curly brackets and square brackets are correct).
<br> Also, do ensure that the JWKs have all the required keys - "x", "y", "use", "crv", "kid", "alg", "kty". Any of these omitted will cause an error.

<br>**Q.** How do we troubleshoot **error 490-499**?
<br>**A.** Ensure that you are not reusing JWT tokens or using any forbidden headers. If you are still encountering issues, do open a troubleshooting case with APEX.
