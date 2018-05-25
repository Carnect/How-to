# Authentication API - Integration Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Requirements](#requirements)
3. [URLs](#urls)
4. [Obtaining Authentication Token](#obtaining-authentication-token)
5. [Using Authentication Token](#using-authentication-token)
6. [API Documentation](#api-documentation)
7. [Further Help](#further-help)

## Introduction
The Carnect Authentication API serves as a single service where the user only needs to authenticate once to gain access to all of our APIs and services. The API follows the REST conventions and the JSON Web Token (JWT) approach.

## Requirements
To communicate with our API, one requires *either*:
1. A Programming Language supporting HTTP calls
2. REST Client eg. [Postman](https://www.getpostman.com/apps)
	
## URLs
Carnect offers a sandboxed environment for testing and integration related purposes and a production-ready live environment. The URLs for the resepective environments are:

Environment | URL
--- | --- 
**Sandbox/Testing** | https://auth.cnx-uat.com
**Live** | https://auth.carhire-solutions.com

## Obtaining Authentication Token
**Important:** To authenticate a user it is required that the user be *already* created in our systems. Please contact your administrator to have your user created.

Once a user is created they will have an **email** and **password**. The authentication API requires this information.

*Note*: Make sure that the `Content-Type` header is set to **`application/vnd.api+json`**

#### Obtaining Token Programmatically
**curl**
```shell
curl -X POST "https://auth.cnx-uat.com/auth/token" \
  -H "Content-Type: application/vnd.api+json" 
  -d '{"email":"YOUR_EMAIL","password":"YOUR_PASSWORD"}'
```

**C#**
```csharp
using (var client = new HttpClient())
{
	client.BaseAddress = new Uri("https://auth.cnx-uat.com");
	var request = new StringContent(
                    "{\"email\":\"YOUR_EMAIL\", \"password\":\"YOUR_PASSWORD\"}",
                    Encoding.UTF8,
                    "application/vnd.api+json");
	var result = await client.PostAsync("/auth/token", request);
	var json = await result.Content.ReadAsStringAsync();
	System.Console.WriteLine(json);
}
```

**NodeJS**
```javascript
const request = require('request');

const options = {
  url: 'https://auth.cnx-uat.com/auth/token',
  json: true,
  headers: {
    'Content-Type': 'application/vnd.api+json',
  },
  body: {
  	email: 'YOUR_EMAIL',
  	password: 'YOUR_PASSWORD',
  }
};

request.post(options, (err, request, body) => {
	console.log(body)
});
```

#### Obtaining Token Using Postman
1. Set the type of request to `POST`
2. Type the URL wih the endpoint `/auth/token`
3. Set `Content-Type` to `application/vnd.api+json`
4. Click on `Body` tab and enter the JSON body as shown in 7.
5. Click Send
6. View your response

![postman-example](postman-00.png?raw=true) 

#### Authentication Success
If the request is succesful you with receive a `HTTP 200` with the following body structure:

```json
{
  "data": {
    "type": "tokens",
    "id": "00000000-0000-0000-0000-000000000000",
    "attributes": {
      "value": "eyhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ImNlNmQzYTJhLTMzNTctNDRjOS1hOGZkLTRiZDVhYTNiMzk0NCIsImVtYWlsIjoiY254LWFkbWluQGNhcm5lY3QuY29tIiwiYWZmaWxpYXRlSWQiOjcyOSwiYWZmaWxpYXRlSWRzIjpbNzMxLDcyOV0sInNjb3BlIjpbInVzZXI6KiIsInNob3A6KiIsImdyb3VwOioiLCJvcmdhbml6YXRpb246KiIsInN1cGVydXNlcjoqIiwicm9sZToqIiwiYm9va2luZzoqIl0sImFzc29jaWF0aW9uIjp7InNob3BJZCI6bnVsbCwiZ3JvdXBJZCI6bnVsbCwib3JnYW5pemF0aW9uSWQiOiIxNDVmZDVmOC1lMzk2LTRjOTAtYTRjNi1kZjBmNGQ1NDRjOWIifSwia2lkIjoiNzg5ZGNiOGQtOWEyMi00NjI0LWE4YjItZjFlZTdmMTViZWY0IiwiaWF0IjoxNTI3MjQyMTUwLCJleHAiOjE1MjcyNDMzNTAsImF1ZCI6ImNhcm5lY3QuYXV0aC5hcGkiLCJpc3MiOiJjYXJuZWN0LmF1dGguYXBpIiwianRpIjoiMDcxMWQxOTYtZDI4Ni00NGYwLWIyOTAtMmRhODg3ZGZiMDgzIn0.bDGPpth8MXIc0-54X-W224ZNtTRaNjq-CF_pj8nDJbyCoB-0tMmqorO_mry2gNg9rpSaOBicazCoj18OO61EbgzZaQszqHGzSgXL5VxzwCtwbGxNUHitqDQeX0yZhY2P8I9uDRwOYA7b0XEJP7lQgwjqHzYD-w2axjoH-rV8vdu_LPy48xu8kZnrYVrxM-p6xdAPh77MhBMkELIT0_PXrqEcXmXgC92MwgmBN1Biw62VPcY5q0yg_OYkTAKRXmQQ_i3AO_nFKbYFlkoiLUbsOr-yQY795QQ5o4dL2xYKQaV5ArXZll7mzhPgViz1Dxj0D53Hx8ptw4enx9EMZog"
    }
  }
}
```

The JWT token is present in the `data.attributes.value` key. One should **save** this token and use it to communicate with our systems for any future requests.

#### Authentication Error
If the request is unsuccessful, one will get a `HTTP 401` with the following body structure:

```json
{
  "errors": [
    "Unauthorized request"
  ]
}
``` 

## Using Authentication Token
The JWT token obtaned from the [above step](#obtaining-authentication-token) can be used for the following services:

* Authentication API
* Booking API
* User Management
* Bridge


**Important**: Authentication API and most other APIs require that the `Content-Type` be of the type **`application/vnd.api+json`**

The process remains the same - it needs to be passed in the **Authorization** HTTP header with the **Bearer** scheme:
```
Authorization: Bearer YOUR_TOKEN
```

*For example*, to obtain the token information, one can use `GET /auth/identity` endpoint of the Authentication API. The response includes a *basic* information about the user for whom the token has been issued:

```json
{
  "data": {
    "type": "users",
    "id": "1d6d382a-1357-4ac9-08fd-4bd4aa3b39a8",
    "attributes": {
      "email": "test@test.com",
      "firstName": "Test",
      "lastName": "User",
      "role": {
        "id": "29018f65-bb80-42fa-9c75-754dca470ba5",
        "name": "default role",
        "scope": [ ]
      },
      "status": "active",
      "language": "en-GB",
      "affiliateId": 729,
      "createdAt": "2017-10-06T13:43:20.579Z",
      "association": {
        "organizationId": "145fd5f8-e396-4c90-a4c6-df0f4d544c9b",
        "groupId": null,
        "shopId": null
      }
    }
  }
}
```

#### Using Token Programmatically
**cURL**
```shell
curl -X GET "https://auth.cnx-uat.com/auth/identity" \
  -H "Authorization: Bearer YOUR_TOKEN" 
```

**C#**
```csharp
var token = "YOUR_TOKEN";
using(var client = new HttpClient())
{
	client.BaseAddress = new Uri("https://auth.cnx-uat.com");
	client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
	var result = await client.GetAsync("/auth/identity");
	var json = await result.Content.ReadAsStringAsync();
	System.Console.WriteLine(json);
}
```

**NodeJS**
```javascript
const request = require('request');
const token = 'YOUR_TOKEN';

const options = {
  url: 'https://auth.cnx-uat.com/auth/identity',
  json: true,
  headers: {
    'Authorization': `Bearer ${token}`
  }
};

request.get(options, (err, request, body) => {
	console.log(body)
});
```

#### Using Token in REST Client

**Postman:**
1. Set the type of request `GET`, `POST`, `PATCH` or `DELETE`
2. Type the URL wih the endpoint
3. Set `Content-Type` for `POST` or `PATCH` requests
4. Set the `Authorization` header
5. Click Send
6. View your response

![postman-example](postman-01.png?raw=true) 

## API Documentation

The complete intensive API documentation is available at `/docs` endpoint of the APIs:


* **Staging**: https://auth.cnx-uat.com/docs
* **Live**: https://auth.carhire-solutions.com/docs

## Further Help
Please contact us for additional questions and queries


























