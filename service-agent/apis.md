# Overview

Environment of API
- Architecture style: REST
- All API data transmission is encrypted over HTTPS,
- Payload type: JSON
- Host: https://egb17p3twf.execute-api.eu-west-1.amazonaws.com/dev
- Authentication
  : We use API key for authenticate the call. For the details, please contact [DEEPEYES App Support](app@deepeyes.co.uk).
  : Authentication header
  ```javascript
  "x-api-key": "xxxxxxxxxxxxxxxxx"
  ```
  
> If you have any problems or requests, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

## API index (link to each API)
| API Name | called by | called at |
| -------- | ------ | ------ |
| [Create a new service agent account](#create-user) | CIC | when a new account is created at CIC |
| [Create a new job](#create-job) | CIC | when a job is created at CIC |

### Create User (CIC -> Service Agent UK)
Create a new account of a service agent

#### Method / Endpoint
```javascript
POST /users
```

#### Payload
```javascript
{
  "companyId", "12020394",
  "companyName", "Guildford Gas Engineers",
  "firstname": "firstname",
  "lastname": "lastname",
  "email": "example@email.com"
}
```
> DB Keys: 
>  - email (string)

#### Parameters
NONE

#### Response
* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 500 Internal Server Error (please contact [DEEPEYES App Support](app@deepeyes.co.uk))
* 201 created

#### Example
<img width="723" alt="image" src="https://user-images.githubusercontent.com/59367560/185818969-dbdbf158-7d5a-4f19-962e-e31500380b23.png">

### Create Job (CIC -> Service Agent UK)
Create a new job to take an action

#### Method / Endpoint
```bash
POST /jobs
```

#### Payload
```json
{
  "jobNo": "2022008290002",
  "companyId": "20102918293",
  "customer": {
    "name": "Michael Adam",
    "phone": "07599 123456",
    "address": {
      "line1": "41 Victoria Road",
      "line2": "",
      "city": "Kingston Upon Thames",
      "county": "Surrey",
      "postcode": "KT1 2AB",
      "country": "United Kingdom"
    }
  },
  "product": {
    "id": "product-id",
    "name": "product name"
  },
  "serviceRequestDate": "2022-09-15",
  "jobNotes": "Lorem Ipsum ...",
  "symptom": "A0100004"
}
```
> DB Keys: 
>  - jobId (string),
>  - email (string)

#### Parameters
NONE

#### Response
* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 500 Internal Server Error (please contact [DEEPEYES App Support](app@deepeyes.co.uk))
* 201 created

#### Example
<img width="728" alt="image" src="https://user-images.githubusercontent.com/59367560/185975558-0956cb91-2d89-4f14-bf13-8f7580e9b039.png">
