# Introduction to Hello World!

Hello World! APIs are used to test authorization header (***x-apex-jwt***), to help developers in testing their signing codes. 

## Hello World!

This API tests that the JWT in **x-apex-jwt** header is valid and will return with a Hello World! if successfully authenticated.

## SHA-256 Generator

This API evaluates the sha-256 of the API payload based on the binary content and returns it in the response body.  If **x-apex-returncontent** is included as a header with any value, the API payload is returned below the hash (in UTF-8).
