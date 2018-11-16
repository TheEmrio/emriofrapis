## Getting started

> This page contains the basic concepts of the Emrio REST APIs and how to communicate with them.

Our APIs are RESTful so every request should be made using the HTTP(S) protocol

Latest version : `v1`

**Table of content:**
- Root endpoint
- Accepted methods
- Response structure
- Authentication
<!-- - Handling errors -->
- Versions
- Currently available APIs

### Root Endpoint

The root endpoint of the APIs is `https://apis.emrio.fr/`.
All URLs start with this base path.
Requests should be made over HTTPS.

### Accepted methods

All of the HTTP methods can be accepted for the APIs.
Supported methods can vary with the API you are using.
Moreover, the way data is transmitted can differ by method used and API version.

For v1 APIs
- `GET` method will take parameters in the URL
- All of the other methods (`POST`, `DELETE`, ...) use `x-www-form-urlencoded` data

Using a method not handled by the API for a URL will return a 405 or 404 HTTP Error

### Response structure

The response to a request will always be in the form of a JSON object.

This is an example of a request response

```json
{
  "code": 200,
  "message": "Request succeeded",
  "data": { ... }
}
```

- `code` (Number) is the HTTP response code. List available [here][link-list-http-codes] (all are not used).

- `message` (String) is a official message of the response. For errors, it is always the meaning of the HTTP code (a 404 code implies a message of "Resource Not Found")

- A `data` (JSON Object) will be present if the API returned anything. The content of this object depends on the API you are using.

- Some responses may have a `info` (String) entree. It may appear if the request didn't succeeded and to help you know why (no authentication, wrong method, not enough parameters).


### Authentication

Some API requests may need you to authenticate yourself (modifying values, creating entries, deleting, ...).

You can authenticate a request by using Bearer Authentication. Simply add the header `Authorization: Bearer YOUR_API_TOKEN`.

Not authenticating a request that needs authentication or having wrong credentials will return a 403 HTTP error.

You can get your API Key in your [personal account page][link-myaccount]. This API Key is unique and should not be shared. You therefore should not call the APIs that require authentication in the client-side of your application.

You can get a new API Key by clicking the &laquo; Regenerate &raquo; button in your [personal account page][link-myaccount]. This will revoke your old API Key which therefore cannot be used after.

<!-- ### Handling errors -->

### Versions

Some APIs may have different versions which can modify the response and/or how the request is treated.

If you want to use the latest version of an API, you should use the following endpoint:

```
https://apis.emrio.fr/service/etc
```

If you want to use a specific version of an API (eg: `v3`), use this endpoint:

```
https://apis.emrio.fr/v3/service/etc
```

### Currently available APIs

This is a list of the APIs currently available:

- [Shortener][link-shortener] (`v1`) : URL shortening service


[link-myaccount]: //emrio.fr/myaccount
[link-list-http-codes]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
[link-shortener]: //emrio.fr/apis/shortener