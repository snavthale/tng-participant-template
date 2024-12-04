# Introduction

This repository contains the template for building [onboarding](https://github.com/WorldHealthOrganization/smart-trust/blob/main/input/pagecontent/concepts_onboarding.md) informations for the Smart Trust Network Attendees. This includes CSCAs, Auth information, signing information and other relevant files for onboarding a participant.

# Technical Procedure

Regarding the prerequisities and technical procedure, the necessary information and commands are documented on [Smart-trust](https://worldhealthorganization.github.io/smart-trust/concepts_onboarding_checklist).


# Trust Domains

Supported Domains:

- DCC
- IPS-PILGRIMAGE
- DICVP
- PH4H

## Adding a new trust domain

New trust domains can be established only in agreement between the requesting party and WHO.
Collaborate with the WHO's secretariat to gather comprehensive insights and feedback for the development of the new trust domain.

Once the new trust domain is established create new subdirectory in 'onboarding' subdir that reflect the agreed domain name.
If you are already onboarded for a domain (e.g. DCC, IPS-PILGRIMAGE,DICVP,PH4H etc.) you only need to provide SCA for the the newly added domain.  This can either be an existing SCA or a new SCA.
If the newly added domain is the first one for this participant, UPLOAD, TLS and SCA must be generated.

# Trusted Issuer

To onboard Trusted Issuer, provide input via the subfolder ISSUER.

Other credential types like Verifiable Credentials are using DIDs or other Issuer IDs which are not necessarily linked to any SCA, but with crypto material behind it. 
To support these issuers and their credentials, trusted issuers must be onboarded like SCAs and all other certificates.
For the onboarding a JSON structure is used.

## JSON structure specification

The JSON structure is defined as follows named `Trusted_Issuer.json`:

```json
{
  "name": "Ministry of Health",
  "url": "did:web:example.com",
  "urlType": "DID",
  "hash": "463bcd43a6ae45a5d9606adfb0c2d968cfacb73e0df827f05a7c7f781a1869c5",
  "sslPublicKeys": [
    "MIIGwjCCBaqgAwIBAvd3QuY29tMEkGCCsG....Lz3lGqBrHBklHq7x5WK4dAipTLrG39u",
    "MIIGwjCCBaqgAwIBAvd3QuY29tMEkGCCsG....Lz3lGqBrHBklHq7x5WK4dAipTLrG40u"
  ],
  "country" : "DE"
}
```

Multiple files can be provided by adding a numbered suffix like `Trusted-Issuer_1.json`, `Trusted-Issuer_2.json`.


| Field         | Optional | Type   | constraints          | Description                                                                                                                                                 |
|---------------|----------|--------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| name          | No       | String | 512 chars            | Name of the Service                                                                                                                                         |
| url           | No       | String | 64 chars             | A resolvable DID URL using did:web as DID method                                                                                                            |
| urlType       | No       | String | 25 chars             | DID                                                                                                                                                         |
| hash          | No       | String | 64 chars             | SHA256 Hash of the content behind it (if applicable)                                                                                                        |
| sslPublicKeys | No       | String | 2048 chars per entry | SSL Certificates of the endpoint hosting the DID document. Additional entry may be used to support key rotation. (Format: Base64 of the DER representation) |
| country       | No       | String | ISO 3166-1 alpha-2   | The alpha 2 country code of the participant                                                                                                                 |

The JSON structure will be signed by the trust anchor and onboarded to the gateway.

