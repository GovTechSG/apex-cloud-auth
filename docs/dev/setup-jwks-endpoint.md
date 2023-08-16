# Setup for JWKS Endpoint

In the previous section we covered what basics of JWKS endpoint. To use the JWKS Endpoint for APEX, the following setup steps will be required.

## External Zone

If you are a consumer of APEX API in the external (internet zone), you would just need to configure the JWKS endpoint in your Application and toggle to "Use JWKS Endpoint".

Your TLS JWKS endpoint will need to be signed by a supported common trusted public root CA. Self-signed endpoints are not supported.

## Internal Zone

If you are a consumer of APEX API in the internal (intranet zone), you would just need to configure the JWKS endpoint in your Application and toggle to "Use JWKS Endpoint".

Your TLS JWKS endpoint will need to be signed by a supported common trusted public root CA or by SGCore's root CA. Self-signed endpoints are not supported. Recommended CAs can be found [here](https://docs.developer.tech.gov.sg/docs/apex-cloud-user-guide/docs/general/trusted-certificate-authorities). Do ignore the notice at the bottom meant for Publishers.

The next section will describe action(s) needed for APEX to access your JWKS endpoint in the internal zone.

</br>

a) For the following zones below, there is no need to clear any firewall between the cloud zones and you would just need to ensure that APEX's internal IP addresses is whitelisted/not blocked in any cloud security groups. Do raise a service desk request to get the IP addresses.

**- GCC 1.0 intranet, Azure Intranet, GCP Intranet.**

</br>

b) However, for the following zone, there is a need to set routes in your cloud environment. Do raise a service desk request to get instructions for setting routes in your zone.

**- GCC 2.0 intranet**

</br>

c) Lastly, for the third category of zones, there may be a need to clear firewall(s) from the CLZ to your server. Do raise a service desk request to get instructions for clearing the relevant firewall(s).

**- GEN and any linked networks**
