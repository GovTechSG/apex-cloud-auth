# JWKS Endpoint Sample Codes

These are sample codes to help the Developer in generating a JWKS endpoint. Do note that these are for reference only and not intended for production use.

## Node JS

```
'use strict';

// DEPENDENCIES
const jose = require('node-jose');
const crypto = require('crypto');

// CREATE JWKS
async function jwks() {

    /*
        CREATE JWK
    */

    let key = crypto.generateKeyPairSync('ec', {
      namedCurve: 'prime256v1',
      publicKeyEncoding: {
        type: 'spki',
        format: 'pem',
      },
      privateKeyEncoding: {
        type: 'pkcs8',
        format: 'pem',
      },
    });

    let cryptoKey = await jose.JWK.asKey(key.privateKey, 'pem');

    let publicKeyJSON = cryptoKey.toJSON();
    let privateKeyJSON = cryptoKey.toJSON(true);

    let jwksEndpoint = {
      keys: [{...publicKeyJSON,
              ...{use: "sig"},
              ...{crv: "P-256"},
              ...{alg: "ES256"},
    }]};

    console.log("Public keys:");
    console.log(publicKeyJSON);

    console.log("JWKS Endpoint:");
    console.log(jwksEndpoint);

    // console.log("Private keys:");
    // console.log(privateKeyJSON);

    // console.log("Private keys(PEM):");
    // console.log(cryptoKey.toPEM(true));
}
jwks();

```

```
% node create-keys.js
Public keys:
{
  kty: 'EC',
  kid: 'vyaeBP-ohJ5RF_cEEU1v0h3IEIoWCa24YKZK4ddb4-U',
  crv: 'P-256',
  x: 'RYvFyXBZLa7TWEDlk3sqqyhxXkTYGkEEl5AuANZ70Ps',
  y: 'JKobI-7Z4xBCGDKDubtBF-sHvC69F6sKGbRX3RIaGhY'
}
JWKS Endpoint:
{
  keys: [
    {
      kty: 'EC',
      kid: 'vyaeBP-ohJ5RF_cEEU1v0h3IEIoWCa24YKZK4ddb4-U',
      crv: 'P-256',
      x: 'RYvFyXBZLa7TWEDlk3sqqyhxXkTYGkEEl5AuANZ70Ps',
      y: 'JKobI-7Z4xBCGDKDubtBF-sHvC69F6sKGbRX3RIaGhY',
      use: 'sig',
      alg: 'ES256'
    }
  ]
}
```
