---
title: API Reference

search: true
---

# Introduction

Welcome to EmpowerID API! You can use our API to manage access tokens for user authentication, including functions such as:

+ creating new access tokens
+ retrieving information on tokens and users
+ refreshing tokens which have expired

# Authentication

EmpowerID API uses API keys to allow access to the API. You can request a new API key on our [QuickStart Page](https://docs.empowerid.com/2016/dev/webapi/quickstart).

EmpowerID API expects the API key to be included in the header when requesting a new access token.

<!-- <aside class="notice"></aside> -->

# HowTo

For more information on how to accomplish different access token tasks with EmpowerID, watch this [video] (https://drive.google.com/file/d/13-sY_eqccf4dqcbbsi_GQRn8uAsbfICN/view).

# Reference

## GET OpenID Connect Config

> Example request

```shell
curl --location --request GET "https://sso.empoweriam.com/oauth/.well-known/openid-configuration"
```
> Example response

```json
{
    "issuer": "https://sso.empoweriam.com",
    "jwks_uri": "https://sso.empoweriam.com/oauth/.well-known/jwks",
    "authorization_endpoint": "https://sso.empoweriam.com/oauth/v2/ui/authorize",
    "token_endpoint": "https://sso.empoweriam.com/oauth/v2/token",
    "userinfo_endpoint": "https://sso.empoweriam.com/oauth/v2/userinfo",
    "tokeninfo_endpoint": "https://sso.empoweriam.com/oauth/v2/tokeninfo",
    "tokenrevoke_endpoint": "https://sso.empoweriam.com/oauth/v2/tokenrevoke",
    "scopes_supported": [
        "openid",
        "profile",
        "email"
    ],
    "claims_supported": [
        "aud",
        "iss",
        "iat",
        "exp",
        "auth_time",
        "nonce"
    ],
    "response_types_supported": [
        "code",
        "token",
        "id_token",
        "id_token token",
        "code id_token",
        "code token",
        "code id_token token"
    ],
    "grant_types_supported": [
        "authorization_code",
        "client_credentials",
        "password",
        "refresh_token",
        "implicit",
        "urn:ietf:params:oauth:grant-type:saml2-bearer",
        "urn:ietf:params:oauth:grant-type:certificate-bearer",
        "urn:ietf:params:oauth:grant-type:impersonate-bearer",
        "urn:ietf:params:oauth:grant-type:jwt-bearer"
    ],
    "subject_types_supported": [
        "public"
    ],
    "id_token_signing_alg_values_supported": [
        "RS256"
    ],
    "token_endpoint_auth_methods_supported": [
        "client_secret_post",
        "client_secret_basic"
    ]
}
```

This endpoint retrieves configuration data for an EmpowerID platform tenant.

### HTTP Request

`GET https://sso.empoweriam.com/oauth/.well-known/openid-configuration`

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve
-->

## Get OpenID Connect Web Keys

> Example request

```shell
curl --location --request GET "https://sso.empoweriam.com/oauth/.well-known/jwks"
```

> Example response

```json
{
    "keys": [
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "_lq2NHEiFgQ7UhAVVNiQJ63cnYs",
            "x5t": "_lq2NHEiFgQ7UhAVVNiQJ63cnYs",
            "e": "AQAB",
            "n": "iAK5mwueGN3FD8Qect_LwQ5z554v2_3iP-ojLkoZwafszv5YLoyuTEHvOJeCspTf-YDwwKZ8tobAIl50pN0652QbBKIaimk0erQpFPyEQmN56B9JYAqU2sMFlczmYdbpqOH0uaQwi3ZYahGwAF2vF0hUz0r_X5yuDPZytVABBT4LkqKY3U_f1t0oQrmABCZmEZl_QETdQweVzKklR8x_ypnhl0OQgYExxZ8Dz8_j4bft3CfLZyKd_d8R4LVH_ssKUDX8WqrJFSMZU-iEVSN-xL8xHlOsq16dAB5TUUFC-fApDyoz3Ty5yhCyfbWoAVkXriXLZFa-2m7WS6_AVfADhw",
            "x5c": [
                "MIIC/zCCAeegAwIBAgIITkVwDg+Dp5IwDQYJKoZIhvcNAQELBQAwJjEkMCIGA1UEAwwbRW1wb3dlcklEIE9BdXRoIENlcnRpZmljYXRlMB4XDTE5MDYyMTAwMDAwMFoXDTIxMDYyMTAwMDAwMFowJjEkMCIGA1UEAwwbRW1wb3dlcklEIE9BdXRoIENlcnRpZmljYXRlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiAK5mwueGN3FD8Qect/LwQ5z554v2/3iP+ojLkoZwafszv5YLoyuTEHvOJeCspTf+YDwwKZ8tobAIl50pN0652QbBKIaimk0erQpFPyEQmN56B9JYAqU2sMFlczmYdbpqOH0uaQwi3ZYahGwAF2vF0hUz0r/X5yuDPZytVABBT4LkqKY3U/f1t0oQrmABCZmEZl/QETdQweVzKklR8x/ypnhl0OQgYExxZ8Dz8/j4bft3CfLZyKd/d8R4LVH/ssKUDX8WqrJFSMZU+iEVSN+xL8xHlOsq16dAB5TUUFC+fApDyoz3Ty5yhCyfbWoAVkXriXLZFa+2m7WS6/AVfADhwIDAQABozEwLzAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMA0GCSqGSIb3DQEBCwUAA4IBAQBotQvLAxfc15JSxF3794N7uhAT8cF2tbl6I5Z1noP1PBKO/2dibUzpGViBYLNE4G3PQF2ezDIsnoIfQnrdebZR3PxHHAvTjd+hSOCxUNRPi6PpeZCwPAw1DaJhbKSoYzamgOLbQHTFhXiIAmoKTI3PkV94o6NEIsv5xTfaffRqXmmCygQjlf4U7odeMNsAJKC650FnFc6KWzcUgfuE836yI1M2fS1OI/1o16QJzpYRPsfp4T1p2+59urzj17kFuU6Fm3/osxcMWlpBdg2K6pQzSnEm+83RfFdEf8yCkf0yroo4rqpMCDTKaNekrK5LuxtfRdP64H2jJI3nTwPgAGMD"
            ]
        },
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "mrTa7pmCADwefR_cP0jTo92V7vc",
            "x5t": "mrTa7pmCADwefR_cP0jTo92V7vc",
            "e": "AQAB",
            "n": "sr1qLVDXYpeaIwMN6g1aDMZdlLCPIVSaRrcWuHybD5JvJ21gWoAnk05kAp5asnlD4xUg2JiGVe8yWJif1hSQiprfpTqsWSTEQxYzT-kPssbJtbMNcte8LJ8nCxZcsH5RSMiUK8gpQB4Cpp-jAcHXBzF8M9wAI-66KNR0Ue8qc-j3B7W0irWsLOfh76ituppdZmL-H4WRrwqyy-jzXYsadZk1I9xGdaX6_y0CKkWGeQ8vJ-oEezoXhIkVOJYC5CuK8Ihs7PsjXr1oF3kUCui4yyTb2CBGiZ2Tj82twGC7X_f1Z4fXJxbxcicAZU2NeMzMFNU0iLaI50MSB0oSJ6cl1ujfr4eiFPZkfs3c9zXhTauTZ7j5jB9B6MOC6x--U_J74n1csJ38oFIAVniAEGVXbeC2SEQX2CFJ2t6YGV_BiWj7LLdCJMG80oh-WcROmi2bapeOSdtH9hPSf2OZwP_fqylYMZ1CVZjbVwcMFX5BNNJDjVM_-sQ9c1UsCpD5Lojf8OC7HUAxO4JuSz-TlHfyohjuvHLYWwuhWnoFfOlWRPxw39Y1k7v0xTYTjGc8BmsBiApnkZL7JbHE333Y2jGJoDmR8MCkqAT3QokIfj0gsjmPvfiJBQGZ2ysEAkmYZ27f-Zc5BsXMdfw05X-7zB79EDbnu6Hq8Vr8bBR4xBwF_9M",
            "x5c": [
                "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"
            ]
        },
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "3jaJpg7iYf8tDinNGobcK0_Ws44",
            "x5t": "3jaJpg7iYf8tDinNGobcK0_Ws44",
            "e": "AQAB",
            "n": "gx-FkcFVuVJBRPiaUrWz38k5mQdQp4FdwZ3aTJOf1Dj9WJ0JJVTcsbVUQ_OA39Pqg6rXmQLV6TaMyzIzmvEcc8UDf2U0EMlzPhWUV1lGZwDnvVb9913MQv6WJ9rPY9TeYoYYHX4VYWOPkvbM09Lt5WNwgwp4obyMeg1zuc0Wtj4gVeUmMoFgwGhgSznvBGNnC2oo4QEoGfrgUyonuDjeID7E6IkGWnd0wWCSwfUOw75ts0tptRQ8YPdMW8HoDlIaZo-ovuEnU-WrFom80Lm4FbFJc5Ts_HxUoXHj7bSQaSKP1WuYnu23Eb6_hrsdFEFtprQHBWG0MxDPx8B0Vsdviw",
            "x5c": [
                "MIIDEjCCAfqgAwIBAgIQGNJ+GYECN7xA/XvD1sHgIzANBgkqhkiG9w0BAQsFADAyMTAwLgYDVQQDEydNaWNoYWVsLVdpbjE2LnRoZWRvdG5ldGZhY3RvcnkuaW50ZXJuYWwwHhcNMTgwNjAxMTQyNzQ0WhcNMTkwNjAxMDAwMDAwWjAyMTAwLgYDVQQDEydNaWNoYWVsLVdpbjE2LnRoZWRvdG5ldGZhY3RvcnkuaW50ZXJuYWwwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCDH4WRwVW5UkFE+JpStbPfyTmZB1CngV3BndpMk5/UOP1YnQklVNyxtVRD84Df0+qDqteZAtXpNozLMjOa8RxzxQN/ZTQQyXM+FZRXWUZnAOe9Vv33XcxC/pYn2s9j1N5ihhgdfhVhY4+S9szT0u3lY3CDCnihvIx6DXO5zRa2PiBV5SYygWDAaGBLOe8EY2cLaijhASgZ+uBTKie4ON4gPsToiQZad3TBYJLB9Q7Dvm2zS2m1FDxg90xbwegOUhpmj6i+4SdT5asWibzQubgVsUlzlOz8fFShcePttJBpIo/Va5ie7bcRvr+Gux0UQW2mtAcFYbQzEM/HwHRWx2+LAgMBAAGjJDAiMAsGA1UdDwQEAwIEMDATBgNVHSUEDDAKBggrBgEFBQcDATANBgkqhkiG9w0BAQsFAAOCAQEAW7uC6Q2t8fhHBIW8/bfaBUkMpE5D0F0u0vWe9i6FUfidpTOlMh/HoTaggnbFpEXajvfPM6PwpIuel8xtfs4wESvZgjV9sBT7ItVaHI610VLG5swhCjMoJYyq7rTyBZ50BhJP8x1pEVeFCbHp+vNDsrOUuX4t156BMvUW84domffSqncG1BoyflwE+BrawO/lN3Uiy1U2Z5GhZaUVaHaTLiEeHBL4N4S9qq5Ei2ml/niviJgsAEhGIx9N3RZFreaUgAyABeo247j2I6WRrzXWZvWaIRjNR2cS8Q+xfTpWnICKg8cRRm7/fhMasbisl/IKgW5wpe/1IE0iX0REmyuubQ=="
            ]
        },
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "DXyhbYjljijVQ4g_DznZe-d18Ok",
            "x5t": "DXyhbYjljijVQ4g_DznZe-d18Ok",
            "e": "AQAB",
            "n": "kHNEGgR4a_TVqVx0NohjwBynpVstePwDzUNTubxN7POxZQm44BLrd5NnzmbCeBosbO6JRa3yWs3tNmB7rRbLo20E29MsrXj_CQ4UzvrdYrptns0L7alxn5mhHqYg9P6B1VJBNaYHo9PvX-nO6GnyYfpj3622wAkqsLL3AUCOGd5yDzL-LrR2S0mWPecvynTTZP4krPrLPdWlWmbq9hbDme-H9Ijl1TLv5lO9GM-gmvwagDRI0rcIy4P4fHIU9kpKkg2mw6wTaQD8Yqb6crfKAX5bJt_HXNLnKeK4TfSGmE7gvBmoU_0Q71i-t8xYor_RJtNb1wVmZAwvMgh6JAxJ1Q",
            "x5c": [
                "MIIDCzCCAfOgAwIBAgIIZ9nE/VxSO1AwDQYJKoZIhvcNAQELBQAwLDEqMCgGA1UEAwwhRW1wb3dlcklEIFNlbGYtc2lnbmVkIENlcnRpZmljYXRlMB4XDTE4MDcyNDAwMDAwMFoXDTIwMDcyNDAwMDAwMFowLDEqMCgGA1UEAwwhRW1wb3dlcklEIFNlbGYtc2lnbmVkIENlcnRpZmljYXRlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkHNEGgR4a/TVqVx0NohjwBynpVstePwDzUNTubxN7POxZQm44BLrd5NnzmbCeBosbO6JRa3yWs3tNmB7rRbLo20E29MsrXj/CQ4UzvrdYrptns0L7alxn5mhHqYg9P6B1VJBNaYHo9PvX+nO6GnyYfpj3622wAkqsLL3AUCOGd5yDzL+LrR2S0mWPecvynTTZP4krPrLPdWlWmbq9hbDme+H9Ijl1TLv5lO9GM+gmvwagDRI0rcIy4P4fHIU9kpKkg2mw6wTaQD8Yqb6crfKAX5bJt/HXNLnKeK4TfSGmE7gvBmoU/0Q71i+t8xYor/RJtNb1wVmZAwvMgh6JAxJ1QIDAQABozEwLzAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMA0GCSqGSIb3DQEBCwUAA4IBAQAJzHYWi+ZQPCgtVn6QNKgL8wjKwuK1xdeC40+apwNBy3I7XjSTJw0cXjsRZoR578U8j+T+WxusR3ZyfjV4A4xAC/G0SGC9JzO3JgYf7Y5MxcEHrcq9PH00sLRLFx/lhFqPMRjkI8GkwYnA9nvq3dNkX+ETUd7wWNvq501ZHNyeGRBMiF2YvRk1X8eS+X35Tb2o7cWDzQzbo3EylYDXc6FfXRLUc8mPFLA9et3dJVD7+pccSlsb5bBfSrL/IEs7qKe3D+Yuw7AgaVIfldBcorSXJNAjtUjjT0FcGoFbS9xrWfaWGo1HP/FslR3PwE8yWajOn1levE2mqYKSgDOTLw2+"
            ]
        },
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "szn7iHCjxiXVOM45QW2K100R1Qw",
            "x5t": "szn7iHCjxiXVOM45QW2K100R1Qw",
            "e": "AQAB",
            "n": "roIYhFGbgYf0tXvAH2ydYZT3pG2SbML9azXR0OKj3YBEMAGO2rrdHkF3IUCql5xaoN5j99bjuVneD8DBaE_A32u6lSloTx41fC2XZ1Wsf26lIOYJwuESxjaT6-84r20en6H3nqsx02uej9f9bbFM2tw-j74WTDoY3sCjeUzwCiy-oX0eLsygL_tI2bVZY4KiMgqPXzP6rvj8qg5CMpSYIb8q6qD1vsYsKR6VRNJDvMpm3juRgU668XEbbtA0szuw1Nrp3UhH4KVGxEvcWIUJ1aH5MjD8NVTfswnUHVRwfpg3NcpZO_pHwulqDwTNi94o6KFPjkZ8qtJoAzcuwaId0Q",
            "x5c": [
                "MIIDCzCCAfOgAwIBAgIIZiTwalbu2CMwDQYJKoZIhvcNAQELBQAwLDEqMCgGA1UEAwwhRW1wb3dlcklEIFNlbGYtc2lnbmVkIENlcnRpZmljYXRlMB4XDTE4MDgxMDAwMDAwMFoXDTIwMDgxMDAwMDAwMFowLDEqMCgGA1UEAwwhRW1wb3dlcklEIFNlbGYtc2lnbmVkIENlcnRpZmljYXRlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAroIYhFGbgYf0tXvAH2ydYZT3pG2SbML9azXR0OKj3YBEMAGO2rrdHkF3IUCql5xaoN5j99bjuVneD8DBaE/A32u6lSloTx41fC2XZ1Wsf26lIOYJwuESxjaT6+84r20en6H3nqsx02uej9f9bbFM2tw+j74WTDoY3sCjeUzwCiy+oX0eLsygL/tI2bVZY4KiMgqPXzP6rvj8qg5CMpSYIb8q6qD1vsYsKR6VRNJDvMpm3juRgU668XEbbtA0szuw1Nrp3UhH4KVGxEvcWIUJ1aH5MjD8NVTfswnUHVRwfpg3NcpZO/pHwulqDwTNi94o6KFPjkZ8qtJoAzcuwaId0QIDAQABozEwLzAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMA0GCSqGSIb3DQEBCwUAA4IBAQCfoSV28iwT56yp2qmG+YWM8N9qF8O0ok5ze3tnYhB7a35RYpzjcUKpyuMuU1+si9bB52SPHfiP5tCMQ+hQcFJCJ8UfQjiFnQTLLZPYOEklpHhWERd47jKbpFaLDKZJ+KnRk2AB2EwG5kju8RFJW9k29N9qkGLoNxwOJMNyB0Rj1ZDOhxgAKKJYAuk0l0JjQ7fRxbzD37G2VySUSj059EYMANTOY5SGWPxDkT7k1XHkPzwfcTjjXqDrCMMyLDLyRg8bvEyZxTc0vjPGqb7fUipXmqEpm/QHFpuy5kSG0lcLuD4cHbVSD/YCxyARbVSww0ReQEnLqgWOTIgx/bRPkpSB"
            ]
        },
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "FkW4n4nwll1WTM9fepcTsKXS6_I",
            "x5t": "FkW4n4nwll1WTM9fepcTsKXS6_I",
            "e": "AQAB",
            "n": "q4RmNq_hjrWurcT29C32PeNu8d-hGX7oBJqFJUgc_dqCCKUjnBNn3k8Xuq-TmdoTCiziguvmn3SxQpHmmBHb1UAdr3O3x8jNSwo0pcSmTlOgwkwveEoxzukoEL9PdZq1uei1xE4K1ggk_4YslujERCm_mLm_lyzkAC8VhLjphthvvkeWw1LIlwvqCwuFFrpwxaWFQ9FZiUXKRDxSQsndgddKnQDjI5LomkRymcQR1SBaMLLTrBcCBVyV7dstx0_3Veq7CrYv5KAFSkdpx0Iy8MZ5cX63HmclUuzmscdmHACro1lkWNynI7nIlit1hVjbljBSksdfEn26f8SpS_rJ4w",
            "x5c": [
                "MIIDCzCCAfOgAwIBAgIIFKbO+cngoW4wDQYJKoZIhvcNAQELBQAwLDEqMCgGA1UEAwwhRW1wb3dlcklEIFNlbGYtc2lnbmVkIENlcnRpZmljYXRlMB4XDTE4MDMyOTAwMDAwMFoXDTIwMDMyOTAwMDAwMFowLDEqMCgGA1UEAwwhRW1wb3dlcklEIFNlbGYtc2lnbmVkIENlcnRpZmljYXRlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAq4RmNq/hjrWurcT29C32PeNu8d+hGX7oBJqFJUgc/dqCCKUjnBNn3k8Xuq+TmdoTCiziguvmn3SxQpHmmBHb1UAdr3O3x8jNSwo0pcSmTlOgwkwveEoxzukoEL9PdZq1uei1xE4K1ggk/4YslujERCm/mLm/lyzkAC8VhLjphthvvkeWw1LIlwvqCwuFFrpwxaWFQ9FZiUXKRDxSQsndgddKnQDjI5LomkRymcQR1SBaMLLTrBcCBVyV7dstx0/3Veq7CrYv5KAFSkdpx0Iy8MZ5cX63HmclUuzmscdmHACro1lkWNynI7nIlit1hVjbljBSksdfEn26f8SpS/rJ4wIDAQABozEwLzAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMA0GCSqGSIb3DQEBCwUAA4IBAQBX+HDkCg1yyclbE869XgO/kHVWJ+W+75ORRVRxUDQE7R8BjYY8yLol7cymLVVghGxBs39/3mVVqmvqOztCZDFKQvMC9EgZwjdM6qZ2rGXpsw8/jXWX6YaxKSqKJh+yfFqc5OqVrIvTNsZbaTDhfYE/w6jtGoNakhsA2xxAGwh60oUd4Yt/tFvVUGb1kE7cDs8up4ELh9psSquSf0R7uhGNqIgWgFa34Qn7VPv0zbTH2umk/1xYJD5p1xta7Gi8WF/Q2uGtKuwukYUCPQO6u3f5/2e5IUtDhbP7BP6p/+HSxlNwtht/ny5I6P3mqWndQG3VbcAL4LtoUc6DZL/zDy7f"
            ]
        },
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "qc7AFv533tjzhqyRjb7BiBC3AYs",
            "x5t": "qc7AFv533tjzhqyRjb7BiBC3AYs",
            "e": "AQAB",
            "n": "vdNTMW0wyM6qrUgu7noy_6_KO08hudoebob8UKHSCVEYEuQgEQRwh8OP4BseqVxnE5RR8U_Y-O5guApCLqtnR8zaEnuJiFkhw6jbVntX_hBsmkSLaMkBatr23FWUl0SkN4zIu743rDMthH1SvuSokCu2HSjehzzA_s9pMOdqMGXhNmx2ZDci1OL8NGcAkqsob9I1szwpmOUZCxZ2qoIREOHaoJGGo8lbAOejCjkSGAPnH6qOO2QbfHNy9Gty0faHKKVpVN6YrI0Uli00_mpX9aKANnkCjLMML_TpsLIBDgC2sSBfLrZ4yB_CySwC2dtWfvvMcCoJf8NejdBpxIKAnCqTGP52xzVp5VdIpbOkzqfdI6IXzVNCaJGDjXhJZYwqSls6C0Cgup_Avlec-zfv1YAey3rzVE7qnpxBIuFQtxuGD5Pnlmjb-qOlSVjk1YIv6Q4Z20h8lfBL4alX-_sMIwDR6JtZ_a5-YYkifaaxWs5z5QEGritt4u6-OXCK_JD_xTDs-i78k2v-frwyNx-MaScrnvBbcw3BnX3klV_kc6VcnftRiDhEmbZZHNDfV_e-ZTCaal9A1aI1o0uk_FNL0rDAP5FveW8Ardeegd9RsFjf7RIqoB4zmsqkPWJbe1fkh12v04LF3kH-_X6OnxfBK-oHZu2TY5hhGSuK-8DOZVE",
            "x5c": [
                "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"
            ]
        }
    ]
}
```

This endpoint retrieves public keys.

### HTTP Request

`GET https://sso.empoweriam.com/oauth/.well-known/jwks`

## POST Access Token (Password)

> Example request

```shell
curl --location --request POST "https://sso.empoweriam.com/oauth/v2/token" \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Authorization: Basic cGF0cmljazpwQCQkdzByZA==" \
  --data "client_id=3542a382-60ef-4a49-85c4-30831fa1a474&client_secret=4d045e04-7f76-4fea-8041-4430e53a440c&grant_type=password&scope=openid"
```
> Example response

```json
{
    "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Im1yVGE3cG1DQUR3ZWZSX2NQMGpUbzkyVjd2YyIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJFbXBvd2VySUQiLCJzdWIiOiJwYXRyaWNrIiwiYXVkIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiZXhwIjoxNTY4MTgyMDk0LCJuYmYiOjE1NjQ1ODIwOTQsImlhdCI6MTU2NDU4MjA5NCwianRpIjoiYTQyZTg4N2YtZjdlMy00MmQ3LThlZjAtZjU4MDIwZjFiMmM2IiwiYXR0cmliIjp7InBlcnNvbkd1aWQiOiJkMzk5NzY1ZC1mY2Q3LTQ1YzktOTEzZi0yYjBjOWU2NWY4YjciLCJkaXNwbGF5TmFtZSI6IlBhdHJpY2sgUGFya2VyIiwiZW1haWwiOiJwYXRyaWNrQHBhdHJpY2twYXJrZXIuY29tIn19.lTEy42mU6zGwvGbDmwLXWbFuTtZ1jNesaPqwDL3gCp_Rh8gseJdJ_admy-gXaJ1V2oh2PP6WyIeBd93iPloR7k9-i10zdxL6zevA2LLUpoh_iisrnPS1wlw8LAehe7fAt3wvTPAxF5roNJAl3wI7_jOVoOh0FEtAFuXRahTPpecX98pyKINnz_dMSv0jQz0p8pEiNl_dQ5bvEs4R7DxUMzWXrgW0MPeKF4tvzbwBdIA5QIsknUeHb4nGBpaLV7S8upDX5X2BS1_AQwYkNzzQb8cs8Zb6XXqnnVnAW8tcCqJP8l0J2mUykQLqtFi57H-5FvRBpb0P49Fz_tm_-MTbdZkY8JWjUjbtbrJKHPNOQEgvkeKJXgeC8BpqouQpGBKgzvgdPVAEf0mIZeMtywn387PfGRLp4Ie_f0g8UsxZRTaEH4_f8j4kh9nhX82Sv2YQ8Kz_WJPpaTR1CR7yrzjz6k0w3GQnGZEeJE_IPIej7u4QKL-jCkOj_545fCvCh10mZ60-GrupkRnQucdnxuBOXRJxnOOgSRYi_zzchFLTigZQe7zOjm7zcEwWyrydn5O_hFk3JzjEy15DlmZWgvZqSs3T9IERAAIIBoHPq7UTXIpGMiFxJ8YfPOCUqXnLzhPz6xawFR-f5JDQzZvqWmK8vHrH1hqQmYCbk5Si6TaJGJ8",
    "token_type": "Bearer",
    "expires_in": 3600000,
    "refresh_token": "cm50Nlo2T1dEdlp2SFpDZm5TTTVMOHoyR1lrMER6V1hKY2xrcFNWRS9RL3BsOXhvNTlrUnVuclN4K1Y5TUlaRw",
    "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Im1yVGE3cG1DQUR3ZWZSX2NQMGpUbzkyVjd2YyIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJFbXBvd2VySUQiLCJzdWIiOiJwYXRyaWNrIiwiYXVkIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiZXhwIjoxNTY4MjU0MDQyLCJuYmYiOjE1NjEwNTQwNDIsImlhdCI6MTU2NDY1NDA0MiwiYXpwIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiYXRfaGFzaCI6IklkZkt1bHNvQk9RNXg2VWRVeWJmdUEiLCJqdGkiOiJkNjMxMjljMC05ZDQyLTRiMWQtYjQ4Ni0wNzY2NTQ5ODk2ZDQiLCJhdHRyaWIiOnt9fQ.AvtHJ3iEZhI8lUMqsWiivosjv4PTsjWuT25dRsk41jLICz4dGqh7e9byNOBtVzfiR9LVaej0oOJKgfS3ef8saLRkmSmrmvCRs4RhYunZPVBhwpT2DbHMlQBaw7Myp2X6AXVflF5APuxYL-OlavOziDq9b_8x50eWLOJumGJPQepTFC3vzHVXyal23m89XCJhRPuuBd7A5DMcXsJcIhBykqxzgDQBkSlA1CYiVKirxnZLI5ALBW1sPessxAaGmnI0Otvxm1mXXKWTMJxi7J8AirMY12Gc-bdmQpbOkVNrQq2gN8jatQL0MZNDuYk4__HGfOKHemeXgskfZQg2mrisUFKT5fRQcUrPKVkwU6kvGlWr2lvN6JlEJDnKC_aKWpvJVTWuCRI2H-a1yCbZIeJ4e3HY7VaKLeVoNZm-kTwLj2h8M3fDtmT_Gn9SwyAYrg6CMN-nPrEz8XQ0JcZlzbJYLeCzHUuHB5G368o-dNjmE90S0ZReQqALFmvKK2KY3KX4rt3HkJNqWpOyf8NyatXAjIvHPjFHRXWSgCO5g8nfrgJuvXKBFRA4C5VC3vB8YMvpOWvcvL-IEZT05sePUVqq5fAbV-c58KTMosctdjNevdGAbn0sfWKVagsfavN0UyVJ95tVGD6ByBWfFpAEqudqxOACTTfvktWm8wt1UL1kS-I",
    "id": "d399765d-fcd7-45c9-913f-2b0c9e65f8b7"
}
```
This endpoint retrieves the access token, ID token and refresh token for the password, which can be used in the POST Refresh Token, POST User Info and POST Token Info endpoints listed below.

### HTTP Request

`POST https://sso.empoweriam.com/oauth/v2/token`

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>
-->

### Headers

Parameter | Value  
--------- | -----------
**Content-Type** | application/x-www-form-urlencoded
**Authorization** | Basic cGF0cmljazpwQCQkdzByZA==

### Body *urlencoded*

Parameter | Value
--------- | -----------
**client_id** | 3542a382-60ef-4a49-85c4-30831fa1a474
**client_secret** | 4d045e04-7f76-4fea-8041-4430e53a440c
**grant_type** | password
**scope** | openid

## POST Access Token (Authorization code)

> Example request

```shell
curl --location --request POST "https://sso.empoweriam.com/oauth/v2/token" \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --data "client_id=3542a382-60ef-4a49-85c4-30831fa1a474&client_secret=4d045e04-7f76-4fea-8041-4430e53a440c&grant_type=authorization_code&code=bW5lWmNYT0VxMnAxRFQwUFIwNy84czBpUkdDTTY2RitjRkFhd0JXUXVOM3MzUXZ4TlptYTgrdUw2akdVMDRSdGc2V1h6WjdOV1NXVmFDMzEwbGsvYUE9PQ"
```
This endpoint retrieves the access token used for authorizing a user.

### HTTP Request

`POST https://sso.empoweriam.com/oauth/v2/token`

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>
-->

### Headers

Parameter | Value
--------- | -----------
**Content-Type** | application/x-www-form-urlencoded
**X-EmpowerID-API-Key** | fcdaa2eb-991f-4ded-a9fe-4e6b2410e09d

### Body *urlencoded*

Parameter | Value
--------- | -----------
**client_id** | 3542a382-60ef-4a49-85c4-30831fa1a474
**client_secret** | 4d045e04-7f76-4fea-8041-4430e53a440c
**grant_type** | authorization_code
**code** | bW5lWmNYT0VxMnAxRFQwUFIwNy84czBpUkdDTTY2RitjRkFhd0JXUXVOM3MzUXZ4TlptYTgrdUw2akdVMDRSdGc2V1h6WjdOV1NXVmFDMzEwbGsvYUE9PQ

## POST Refresh Token

> Example request

```shell
curl --location --request POST "https://sso.empoweriam.com/oauth/v2/token" \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --data "client_id=3542a382-60ef-4a49-85c4-30831fa1a474&client_secret=4d045e04-7f76-4fea-8041-4430e53a440c&refresh_token=cm50Nlo2T1dEdlp2SFpDZm5TTTVMOHoyR1lrMER6V1hKY2xrcFNWRS9RL3BsOXhvNTlrUnVuclN4K1Y5TUlaRw&grant_type=refresh_token"
```
> Example response

```json
{
    "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Im1yVGE3cG1DQUR3ZWZSX2NQMGpUbzkyVjd2YyIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJFbXBvd2VySUQiLCJzdWIiOiJwYXRyaWNrIiwiYXVkIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiZXhwIjoxNTY4MTgyMDk0LCJuYmYiOjE1NjQ1ODIwOTQsImlhdCI6MTU2NDU4MjA5NCwianRpIjoiYTQyZTg4N2YtZjdlMy00MmQ3LThlZjAtZjU4MDIwZjFiMmM2IiwiYXR0cmliIjp7InBlcnNvbkd1aWQiOiJkMzk5NzY1ZC1mY2Q3LTQ1YzktOTEzZi0yYjBjOWU2NWY4YjciLCJkaXNwbGF5TmFtZSI6IlBhdHJpY2sgUGFya2VyIiwiZW1haWwiOiJwYXRyaWNrQHBhdHJpY2twYXJrZXIuY29tIn19.lTEy42mU6zGwvGbDmwLXWbFuTtZ1jNesaPqwDL3gCp_Rh8gseJdJ_admy-gXaJ1V2oh2PP6WyIeBd93iPloR7k9-i10zdxL6zevA2LLUpoh_iisrnPS1wlw8LAehe7fAt3wvTPAxF5roNJAl3wI7_jOVoOh0FEtAFuXRahTPpecX98pyKINnz_dMSv0jQz0p8pEiNl_dQ5bvEs4R7DxUMzWXrgW0MPeKF4tvzbwBdIA5QIsknUeHb4nGBpaLV7S8upDX5X2BS1_AQwYkNzzQb8cs8Zb6XXqnnVnAW8tcCqJP8l0J2mUykQLqtFi57H-5FvRBpb0P49Fz_tm_-MTbdZkY8JWjUjbtbrJKHPNOQEgvkeKJXgeC8BpqouQpGBKgzvgdPVAEf0mIZeMtywn387PfGRLp4Ie_f0g8UsxZRTaEH4_f8j4kh9nhX82Sv2YQ8Kz_WJPpaTR1CR7yrzjz6k0w3GQnGZEeJE_IPIej7u4QKL-jCkOj_545fCvCh10mZ60-GrupkRnQucdnxuBOXRJxnOOgSRYi_zzchFLTigZQe7zOjm7zcEwWyrydn5O_hFk3JzjEy15DlmZWgvZqSs3T9IERAAIIBoHPq7UTXIpGMiFxJ8YfPOCUqXnLzhPz6xawFR-f5JDQzZvqWmK8vHrH1hqQmYCbk5Si6TaJGJ8",
    "token_type": "Bearer",
    "expires_in": 3600000,
    "refresh_token": "cm50Nlo2T1dEdlp2SFpDZm5TTTVMOHoyR1lrMER6V1hKY2xrcFNWRS9RL3BsOXhvNTlrUnVuclN4K1Y5TUlaRw",
    "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Im1yVGE3cG1DQUR3ZWZSX2NQMGpUbzkyVjd2YyIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJFbXBvd2VySUQiLCJzdWIiOiJwYXRyaWNrIiwiYXVkIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiZXhwIjoxNTY4MjU0MDQyLCJuYmYiOjE1NjEwNTQwNDIsImlhdCI6MTU2NDY1NDA0MiwiYXpwIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiYXRfaGFzaCI6IklkZkt1bHNvQk9RNXg2VWRVeWJmdUEiLCJqdGkiOiJkNjMxMjljMC05ZDQyLTRiMWQtYjQ4Ni0wNzY2NTQ5ODk2ZDQiLCJhdHRyaWIiOnt9fQ.AvtHJ3iEZhI8lUMqsWiivosjv4PTsjWuT25dRsk41jLICz4dGqh7e9byNOBtVzfiR9LVaej0oOJKgfS3ef8saLRkmSmrmvCRs4RhYunZPVBhwpT2DbHMlQBaw7Myp2X6AXVflF5APuxYL-OlavOziDq9b_8x50eWLOJumGJPQepTFC3vzHVXyal23m89XCJhRPuuBd7A5DMcXsJcIhBykqxzgDQBkSlA1CYiVKirxnZLI5ALBW1sPessxAaGmnI0Otvxm1mXXKWTMJxi7J8AirMY12Gc-bdmQpbOkVNrQq2gN8jatQL0MZNDuYk4__HGfOKHemeXgskfZQg2mrisUFKT5fRQcUrPKVkwU6kvGlWr2lvN6JlEJDnKC_aKWpvJVTWuCRI2H-a1yCbZIeJ4e3HY7VaKLeVoNZm-kTwLj2h8M3fDtmT_Gn9SwyAYrg6CMN-nPrEz8XQ0JcZlzbJYLeCzHUuHB5G368o-dNjmE90S0ZReQqALFmvKK2KY3KX4rt3HkJNqWpOyf8NyatXAjIvHPjFHRXWSgCO5g8nfrgJuvXKBFRA4C5VC3vB8YMvpOWvcvL-IEZT05sePUVqq5fAbV-c58KTMosctdjNevdGAbn0sfWKVagsfavN0UyVJ95tVGD6ByBWfFpAEqudqxOACTTfvktWm8wt1UL1kS-I",
    "id": "d399765d-fcd7-45c9-913f-2b0c9e65f8b7"
}
```

This endpoint refreshes an expired access token.

### HTTP Request

`POST https://sso.empoweriam.com/oauth/v2/token`

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>
-->

### Headers

Parameter | Value
--------- | -----------
**Content-Type** | application/x-www-form-urlencoded

### Body *urlencoded*

Parameter | Value
--------- | -----------
**client_id** | 3542a382-60ef-4a49-85c4-30831fa1a474
**client_secret** | 4d045e04-7f76-4fea-8041-4430e53a440c
**refresh_token** | QWZndmtFL0k0YldPMWpyYzVUeXdwdEVObXhDbWEraHVhb3A1bkZkVTBndVk0K2hzTmkza2wvVFA0MDYzMS80ZA
                  | Returned by POST Access Token (Password)
**grant_type** | refresh_token

## POST User Info

> Example request

```shell
curl --location --request POST "https://sso.empoweriam.com/oauth/v2/userinfo" \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --data "access_token=eyJhbGciOiJSUzI1NiIsImtpZCI6Im1yVGE3cG1DQUR3ZWZSX2NQMGpUbzkyVjd2YyIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJFbXBvd2VySUQiLCJzdWIiOiJwYXRyaWNrIiwiYXVkIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiZXhwIjoxNTY4MTgyMDk0LCJuYmYiOjE1NjQ1ODIwOTQsImlhdCI6MTU2NDU4MjA5NCwianRpIjoiYTQyZTg4N2YtZjdlMy00MmQ3LThlZjAtZjU4MDIwZjFiMmM2IiwiYXR0cmliIjp7InBlcnNvbkd1aWQiOiJkMzk5NzY1ZC1mY2Q3LTQ1YzktOTEzZi0yYjBjOWU2NWY4YjciLCJkaXNwbGF5TmFtZSI6IlBhdHJpY2sgUGFya2VyIiwiZW1haWwiOiJwYXRyaWNrQHBhdHJpY2twYXJrZXIuY29tIn19.lTEy42mU6zGwvGbDmwLXWbFuTtZ1jNesaPqwDL3gCp_Rh8gseJdJ_admy-gXaJ1V2oh2PP6WyIeBd93iPloR7k9-i10zdxL6zevA2LLUpoh_iisrnPS1wlw8LAehe7fAt3wvTPAxF5roNJAl3wI7_jOVoOh0FEtAFuXRahTPpecX98pyKINnz_dMSv0jQz0p8pEiNl_dQ5bvEs4R7DxUMzWXrgW0MPeKF4tvzbwBdIA5QIsknUeHb4nGBpaLV7S8upDX5X2BS1_AQwYkNzzQb8cs8Zb6XXqnnVnAW8tcCqJP8l0J2mUykQLqtFi57H-5FvRBpb0P49Fz_tm_-MTbdZkY8JWjUjbtbrJKHPNOQEgvkeKJXgeC8BpqouQpGBKgzvgdPVAEf0mIZeMtywn387PfGRLp4Ie_f0g8UsxZRTaEH4_f8j4kh9nhX82Sv2YQ8Kz_WJPpaTR1CR7yrzjz6k0w3GQnGZEeJE_IPIej7u4QKL-jCkOj_545fCvCh10mZ60-GrupkRnQucdnxuBOXRJxnOOgSRYi_zzchFLTigZQe7zOjm7zcEwWyrydn5O_hFk3JzjEy15DlmZWgvZqSs3T9IERAAIIBoHPq7UTXIpGMiFxJ8YfPOCUqXnLzhPz6xawFR-f5JDQzZvqWmK8vHrH1hqQmYCbk5Si6TaJGJ8"
```
> Example response

```json
{
    "id": "d399765d-fcd7-45c9-913f-2b0c9e65f8b7",
    "username": "patrick",
    "first_name": "Patrick",
    "last_name": "Parker",
    "email": "patrick@patrickparker.com",
    "organization": "Hosting Organization",
    "business_role_locations": [
        "Any Role in Anywhere",
        "Standard Employee in Anywhere",
        "All Employee Roles in Anywhere",
        "All Employee Roles in All Business Locations",
        "Any Role in All Business Locations",
        "Default Organization All Roles in All Business Locations",
        "Standard Employee in All Business Locations",
        "All Business Roles in Anywhere",
        "All Business Roles in Default Organization",
        "All Employee Roles in Default Organization",
        "Any Role in Default Organization",
        "Standard Employee in Default Organization"
    ]
}
```

This endpoint retrieves user information for a given access token.

### HTTP Request

`POST https://sso.empoweriam.com/oauth/v2/userinfo`

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>
-->

### Headers

Parameter | Value
--------- | -----------
Content-Type | application/x-www-form-urlencoded

### Body *urlencoded*

Parameter | Value
--------- | -----------
access_token | aGRpZytUY3ZCNmhYMWhKQXN3bWJlQUt2eG1vZG5tMzdFYUJ1Nndmd2lkbGdxYVFiME1CTkVsVklFUFBNVWxheWNoTDZHL0xjZzhpNTFUVmc4Y2JqbVhvVmk0ZWExLytTS1FSUU1vbVZ6ZnFNZ21SZy9CUmNCODBWTERPL0g3ZHJyM1B6NElMZ2k5a080VlAxdjlNQmRFaW5VYXA5bTllZ3d5NFB6ZUMrRlZ5aTI3ZHRwMVpqc3ltRUM4M3d6Rn
            | Access token returned by POST Access Token (Password)

## POST Token Info

> Example request

```shell
curl --location --request POST "https://sso.empoweriam.com/oauth/v2/tokeninfo" \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Authorization: Basic MzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0OjRkMDQ1ZTA0LTdmNzYtNGZlYS04MDQxLTQ0MzBlNTNhNDQwYw==" \
  --data "token=eyJhbGciOiJSUzI1NiIsImtpZCI6Im1yVGE3cG1DQUR3ZWZSX2NQMGpUbzkyVjd2YyIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJFbXBvd2VySUQiLCJzdWIiOiJwYXRyaWNrIiwiYXVkIjoiMzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0IiwiZXhwIjoxNTY4MTgyMDk0LCJuYmYiOjE1NjQ1ODIwOTQsImlhdCI6MTU2NDU4MjA5NCwianRpIjoiYTQyZTg4N2YtZjdlMy00MmQ3LThlZjAtZjU4MDIwZjFiMmM2IiwiYXR0cmliIjp7InBlcnNvbkd1aWQiOiJkMzk5NzY1ZC1mY2Q3LTQ1YzktOTEzZi0yYjBjOWU2NWY4YjciLCJkaXNwbGF5TmFtZSI6IlBhdHJpY2sgUGFya2VyIiwiZW1haWwiOiJwYXRyaWNrQHBhdHJpY2twYXJrZXIuY29tIn19.lTEy42mU6zGwvGbDmwLXWbFuTtZ1jNesaPqwDL3gCp_Rh8gseJdJ_admy-gXaJ1V2oh2PP6WyIeBd93iPloR7k9-i10zdxL6zevA2LLUpoh_iisrnPS1wlw8LAehe7fAt3wvTPAxF5roNJAl3wI7_jOVoOh0FEtAFuXRahTPpecX98pyKINnz_dMSv0jQz0p8pEiNl_dQ5bvEs4R7DxUMzWXrgW0MPeKF4tvzbwBdIA5QIsknUeHb4nGBpaLV7S8upDX5X2BS1_AQwYkNzzQb8cs8Zb6XXqnnVnAW8tcCqJP8l0J2mUykQLqtFi57H-5FvRBpb0P49Fz_tm_-MTbdZkY8JWjUjbtbrJKHPNOQEgvkeKJXgeC8BpqouQpGBKgzvgdPVAEf0mIZeMtywn387PfGRLp4Ie_f0g8UsxZRTaEH4_f8j4kh9nhX82Sv2YQ8Kz_WJPpaTR1CR7yrzjz6k0w3GQnGZEeJE_IPIej7u4QKL-jCkOj_545fCvCh10mZ60-GrupkRnQucdnxuBOXRJxnOOgSRYi_zzchFLTigZQe7zOjm7zcEwWyrydn5O_hFk3JzjEy15DlmZWgvZqSs3T9IERAAIIBoHPq7UTXIpGMiFxJ8YfPOCUqXnLzhPz6xawFR-f5JDQzZvqWmK8vHrH1hqQmYCbk5Si6TaJGJ8"
```
> Example response

```json
{
    "active": true,
    "client_id": "3542a382-60ef-4a49-85c4-30831fa1a474",
    "token_type": "Bearer",
    "username": "patrick",
    "exp": 1568182094,
    "iat": 1564582094,
    "nbf": 1564582094,
    "sub": "patrick",
    "iss": "EmpowerID",
    "jti": "a42e887f-f7e3-42d7-8ef0-f58020f1b2c6"
}
  ```

This endpoint retrieves token information for a given access token.

### HTTP Request

`POST https://sso.empoweriam.com/oauth/v2/tokeninfo`

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>
-->

### Headers

Parameter | Value
--------- | -----------
**Content-Type** | application/x-www-form-urlencoded
**Authorization** | Basic MzU0MmEzODItNjBlZi00YTQ5LTg1YzQtMzA4MzFmYTFhNDc0OjRkMDQ1ZTA0LTdmNzYtNGZlYS04MDQxLTQ0MzBlNTNhNDQwYw==
                  | Base64 Encode \<ClientID:ClientSecret>

### Body *urlencoded*

Parameter | Value
--------- | -----------
**token** | aGRpZytUY3ZCNmhYMWhKQXN3bWJlQUt2eG1vZG5tMzdFYUJ1Nndmd2lkbGdxYVFiME1CTkVsVklFUFBNVWxheWNoTDZHL0xjZzhpNTFUVmc4Y2JqbVhvVmk0ZWExLytTS1FSUU1vbVZ6ZnFNZ21SZy9CUmNCODBWTERPL0g3ZHJyM1B6NElMZ2k5a080VlAxdjlNQmRFaW5VYXA5bTllZ3d5NFB6ZUMrRlZ4RkloRko0b013YVpUZitRbXdxT2
          | Access token returned by POST Access Token (Password)
**token_type_hint** | refresh_token
                    | Defaults to access_token
**client_id** | 3542a382-60ef-4a49-85c4-30831fa1a474
              | Pass if Authorization Header is not sent
**client_secret** | 4d045e04-7f76-4fea-8041-4430e53a440c
                  | Pass if Authorization Header is not sent
**token_type_hint** | refresh_token
                  | Defaults to access_token

## POST Token Revoke

> Example request

```shell
curl --location --request POST "https://sso.empoweriam.com/oauth/v2/tokenrevoke" \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Authorization: Basic cGF0cmljazpwQCQkdzByZA==" \
  --data "token=bHdxdkFzY1gyenEwV3Z1aVQ4WUJhNzFJd1NJeU8zWDdlS3pEK3pwTFBKOWhRUHlDTDZ4MWg3WmMzQVpDNEdzR0xLbzZ3Tk9UUkJYZlRZS0R1OW8wZzVnV1J6TXovNXRtMnRwMEFxemVBeDY3K0UvbytoVnhRVHlVM1IybEVxTHVsdytUTXpyUTdzbkowOGRqUDdEY2lFc2V4YXZId3E3Q3c5VFJIUHQvNnFNdXdFRWFtU3RMM1B6bTBybnBNTW&client_id=3542a382-60ef-4a49-85c4-30831fa1a474&client_secret=4d045e04-7f76-4fea-8041-4430e53a440c"
  ```

This endpoint revokes an access token.

### HTTP Request

`POST https://sso.empoweriam.com/oauth/v2/tokenrevoke`

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>
-->

### Headers

Parameter | Value
--------- | -----------
**Content-Type** | application/x-www-form-urlencoded
**Authorization** | Basic cGF0cmljazpwQCQkdzByZA==
                  | Base64 Encode \<Username:Password>

### Body *urlencoded*

Parameter | Value
--------- | -----------
**token** | bHdxdkFzY1gyenEwV3Z1aVQ4WUJhNzFJd1NJeU8zWDdlS3pEK3pwTFBKOWhRUHlDTDZ4MWg3WmMzQVpDNEdzR0xLbzZ3Tk9UUkJYZlRZS0R1OW8wZzVnV1J6TXovNXRtMnRwMEFxemVBeDY3K0UvbytoVnhRVHlVM1IybEVxTHVsdytUTXpyUTdzbkowOGRqUDdEY2lFc2V4YXZId3E3Q3c5VFJIUHQvNnFNdXdFRWFtU3RMM1B6bTBybnBNTW
          | Access token returned by POST Access Token (Password)
**token_type_hint** | access_token
**client_id** | 3542a382-60ef-4a49-85c4-30831fa1a474
**client_secret** | 4d045e04-7f76-4fea-8041-4430e53a440c

# Errors

EmpowerID API uses the following error codes:

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is invalid
404        | Not Found -- The specified resource could not be found
