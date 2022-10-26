# Sample Code

These are sample codes to help the Developer in coding for the JWT header.

## Node JS

```
'use strict';

// DEPENDENCIES
const {createHash} = require('crypto');
const crypto = require('crypto');
const fs = require('fs');
const jose = require('jose');
const jwt = require('jsonwebtoken');
const {v4: uuidv4} = require('uuid');

/*
    FUNCTION TO RETURN SHA-256 ENCODING
*/
function hash(string) {
  return createHash('sha256').update(string).digest('hex');
}
/*
    FUNCTION TO GENERATE JWT
*/
const getJWT = async (iss, sub, kid, aud, data, privateKey) => {
  // var caPrivateKey = fs.readFileSync('./private.key', 'utf8'); // Option to get PKCS8 private key from file
  var caPrivateKey = await importKey(privateKey);

  // SIGNING OPTIONS
  var signOptions = {
    algorithm: 'ES256',
    keyid: kid,
    expiresIn: '180s',
    jwtid: uuidv4(),
    issuer: iss,
    audience: aud,
    subject: sub,
  };
  var payload = {
    data: data,
  };

  // CREATE JWT
  var jwtAuth = jwt.sign(payload, caPrivateKey, signOptions);

  console.log(`JWT Payload-\n${JSON.stringify(payload)}\n`);
  console.log(`JWT SignOptions-\n${JSON.stringify(signOptions)}\n`);
  console.log(`JWT-\n${jwtAuth}\n`);

  return jwtAuth;
};

/*
    FUNCTION TO RETURN PRIVATE KEY IN PKCS8 FORMAT
*/
const importKey = async(key) => {

  const importedKey = await jose.importJWK(key, 'ES256')
  const privateKeyPKCS8 = await jose.exportPKCS8(importedKey);
  return privateKeyPKCS8;
}

// Start of Program

// This is private key generated.  In a real scenario this will be in a secure vault and not in program code.
const privateKey = {
  kty: 'EC',
  crv: 'P-256',
  x: 'usZhq9AL4aC-hkzGCBK3RuJjmxKE6zqEdFyp-tQ8kh4',
  y: 'wHI1r6rQCHQQSAdNxaJDA0Tw5Fq3B-icq-mbMVlLZA4',
  d: 'w55YEByLRumO-Rnsc8jg2_MaYXfEiT_ioFVoGgrCTlg',
  use: 'sig',
  kid: 'apex-example',
  alg: 'ES256',
};

var payload = {payload: 'data'};
var payloadString = JSON.stringify(payload);
var data = hash(payloadString);

console.log(`Payload-\n${payloadString}\n`);
console.log(`Hash-\n${data}\n`);

getJWT('xxxxx-xx-xxxxx,yyyyy-yy-yyyyy', 'POST', 'apex-example', 'https://public-stg.api.gov.sg/agency/api', data, privateKey);

```
<!-- TODO: Include Sample Code for JAVA -->

<!-- TODO: Include Sample Code for C# -->
