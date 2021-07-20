# Auth Endpoint

## Overview

This repo contains all the source code for the user 2 factor authentification controller. 
This endpoint is utilized by: [user endpoint][user-repo], [register endpoint][register-repo] and [login endpoint][login-repo].

## Endpoint URIs

* ### **`/generate/secret`**

##### Description: generates new secret

> * http verb: *`GET`*
> * reponse code: `200`
> * response type: *JSON*
>
> Returns a *string*

##### Url Paramaters:

|param|description|type|default|required|
|---:|---|:---:|:---:|:---:|
| **`encoding`** | The encoding type to use when generating a new user secret. |*string* | "base32" | true |
| **`length`** | The desired length of the secret to be generated |*integer* | 20 | true |

#### Usage

Creating a new secret
* `encoding`: **base32**
* `length`: **20**

Will yeild:

```json
{
    "secret": "IZSEKN2SLZASGVCUJY3WOPROGBKUWPRVG53EYUSXH5PGKOBTEVDA"
}
```

<br/>

* ### **`/generate/token`**

##### Description: generates a token based on secret

> * http verb: *`POST`*
> * reponse code: `200`
> * response type: *JSON*
>
> Returns a *string*

##### Url Paramaters:

|param|description|type|default|required|
|---:|---|:---:|:---:|:---:|
| **`encoding`** | The encoding type to use when generating a new user secret. |*string* | "base32" | true |

#### Usage

Creating a new token from secret
* `encoding`: **base32**
* `secret`: **KQ4GI6Z6OM6FIXSPPFOVOPTYGNZFCWD5NQSTS3TSMETDUMD2MNKQ**

Will yeild:

```json
{
    "token": "717724",
    "remaining": 29
}
```

<br/>

* ### **`/verify/token`**

##### Description: verifies token against secret

> * http verb: *`POST`*
> * reponse code: `200`
> * response type: *JSON*
>
> Returns a *string*

##### Url Body Paramaters:

|param|description|type|default|required|
|---:|---|:---:|:---:|:---:|
| **`secret`** | The auth secret generated when user enabled two factor authentification |*string* || true |
| **`token`** | The token to verify the secret against, sent to the user by email |*integer* || true |

#### Usage

Creating a new secret
* `secret`: **KQ4GI6Z6OM6FIXSPPFOVOPTYGNZFCWD5NQSTS3TSMETDUMD2MNKQ**
* `token`: **317729**

Will yeild:

```json
{
    "valid": true,
    "remaining": 18
}
```


[login-repo]: https://github.com/noahgreff/login-controller-api/
[user-repo]: https://github.com/noahgreff/user-api-endpoint/
[register-repo]: https://github.com/noahgreff/register-controller-api/

