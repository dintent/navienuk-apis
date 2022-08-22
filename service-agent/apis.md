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

### Create User
Create a new account of a service agent
#### Method / Endpoint
```javascript
POST /users
```

#### Payload
```javascript
{
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

### Create Job
Create a new job to take an action
#### Method / Endpoint
```javascript
POST /jobs
```

#### Payload
```javascript
{
    "jobId": "202201290016",
    "symptomCode": "E016",
    "symptomDetail": "No hot water",
    "repairPart": "aaabbbccc",
    "repairDetail": "adjust",
    "status": "in-progress",
    "createdAt": "",
    "companyId": "{{$guid}}",
    "email": "email@email.com"
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
