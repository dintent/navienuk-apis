# Overview

This describes the resources that make up the Navien UK REST API v1. 
If you have any problems or requests, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

All API access is over HTTPS, and all data is sent and received as JSON.

## Authentication

We use API key for authenticate the call. For the details, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

Authentication header

```javascript
"x-api-key": "9c2kFTmLMKxxxxxxxxxx"
```

## APIs

### Update model and serial number mappings

Push all the model and serial number mappings

```javascript
PUT /models
```

Example

```javascript
PUT /models

{
  [
    {
      "serial": "6662", 
      "modelName": "NCB 20 System"
    },
    {
      "serial": "0129", 
      "modelName": "NCB 28 Combi"
    },
    {
      "serial": "22418", 
      "modelName": "SmartPlus kit - Thermostat & Recevier"
    },
  ]
}
```

Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok

## Company

### Create or update a company

Create a new company with the company details

```javascript
PUT /companies/:gas_safe_number
```

Example

```javascript
PUT /companies/207119

{
  "businessName": "All Gas services",
  "address": "The Panorama Park Street Ashford Kent",
  "postcode": "TN24 8DF",
  "phone": "+447956000000",
  "email": "info@email.com",
  "gasSafeNumber": "207119",
  "OftecNumber": "xxxx",
}
```

Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


### Get the company details that is created or updated on the given date

```javascript
GET /dates/:todays_date/companies
```

Example

```javascript
GET /dates/20200908/companies

{
  [
    {
      "businessName": "All Gas services",
      "address": "The Panorama Park Street Ashford Kent",
      "postcode": "TN24 8DF",
      "gasSafeNumber": "200001",
      "OftecNumber": "xxxx",
    },
    {
      "businessName": "Your Gas services",
      "address": "The Regents Park Street, London",
      "postcode": "N2 8DF",
      "gasSafeNumber": "200000",
      "OftecNumber": "xxxx",
    }
  ]
}
```

Response

* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


## Installer Users

### Get new installer user details created or updated on the given date

```javascript
GET /dates/:todays_date/users
```

Example

```javascript
GET /dates/20200908/users

{
  "firstname": "Michael",
  "lastname": "Niblett",
  "phone": "+447956598103",
  "email": "info@allgasserv.com",
  "companyNumber": "200000"
}
```

Response

* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


## Boiler registrations

### Get new registrations

```javascript
GET /dates/:todays_date/registrations
```

Example

```javascript
GET /dates/20200908/registrations

{
  [
    {
      "registrationId": "cfcb77e0-ca64-11ea-8e5b-b1d62677deda",
      "model": "LCB 700 Combi External 28KW",
      "serialNumber": "1710U19Y0769003",
      "installationDate": "09/07/2020",
      "registrationDate": "20/07/2020",
      "warrantyDate": "09/07/2030",
      "warrantyYear": 10,
      "firstName": "Tony",
      "lastName": "Mudge",
      "contactNo": "07554662557",
      "emailAddress": "tonyandtriciamudge@sky.com",
      "address1": "10 Millands Lane",
      "city": "Bridgwater",
      "county": "Somerset",
      "postCode": "ta5 1ed",
      "userId": "198d7a57-50d4-4adc-8b31-be5d41818704"
    },  
    {
      "registrationId": "04732c10-d3f0-11ea-b6d7-759f92541fc9",
      "model": "NCB 34 Combi",
      "serialNumber": "0130J1870535001",
      "installationDate": "01/08/2020",
      "registrationDate": "01/08/2020",
      "warrantyDate": "01/08/2028",
      "warrantyYear": 8,
      "firstName": "Kevin",
      "lastName": "Lawson",
      "contactNo": "07768310450",
      "emailAddress": "fklawson@hotnail.com",
      "address1": "32 Cove Hollow",
      "city": "Bangor",
      "county": "County Down",
      "postCode": "BT19 6HT",
      "userId": "1a1d9282-7f8f-4833-a9a0-2b3df06caf01"
    }
  ]
}
```

Response

* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


### Update Warranty

The Warranty API allows you to update the warranty year of an existing registration. 

```javascript
PUT /registrations/:registrationId/warranty
```

Example 

```javascript
PUT /registrations/04732c10-d3f0-11ea-b6d7-759f92541fc9/warranty

{
  "warrantyYear": 7
}
```

Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok
