# mosquitto-jwt-auth

[![Build Status](https://travis-ci.org/wiomoc/mosquitto-jwt-auth.svg?branch=master)](https://travis-ci.org/wiomoc/mosquitto-jwt-auth)
[![Coverage Status](https://coveralls.io/repos/github/wiomoc/mosquitto-jwt-auth/badge.svg)](https://coveralls.io/github/wiomoc/mosquitto-jwt-auth)

Simple Plugin for Mosquitto which enables authentication and authorisation via JWT as MQTT password.

Requires at least Mosquitto v1.6.3
## Configuration

| Property           | Valid values | Usage |
|--------------------|------|-------|
| `auth_opt_jwt_alg` | `HS256`, `HS384`, `HS512`, `ES256`, `ES384`, `RS256`, `RS384`, `RS512`| Sets the algorithm of the JWT signature |
| `auth_opt_jwt_sec_file` | `<enviroment variable name>` | Path to the file which contains the secret used for verification of the signature. Should be DER-encoded for RSA |
| `auth_opt_jwt_sec_env` | `<enviroment variable name>` | Name of the environment variable which contains the base64 encoded secret used for verification of the signature. |
| `auth_opt_jwt_sec_base64` | `<base64-encoded-secret>` | Base64 encoded secret used for verification of the signature. |
| `auth_opt_jwt_validate_exp` | _(default)_ `true`, `false` | `true` if the `exp` claim / the expiry date of the JWT should be validated |
| `auth_opt_jwt_validate_sub_match_username` | _(default)_ `true`, `false` | `true` if the MQTT username has to be the same as specified in the `sub` claim |

## Custom Claims

* `publ` _(Optional)_ Contains the Topics(filters) the client is allowed to publish in
* `subl` _(Optional)_ Contains the Topics(filters) the client is allowed to subscribe to


      {
        "sub": "mqttUser",
        "iat": 1516239022,
        "exp": 1616239022,
        "subs": ["/+/topic", "/abc/#"],
        "publ": ["/abc"]
      }
