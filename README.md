# Overview

This describes the resources that make up the Navien UK REST API v1. 
If you have any problems or requests, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

All API access is over HTTPS, and all data is sent and received as JSON.

## Updates

| API Name | Development Status | Operation Period |
| -------- | ------ | ------ |
| [Update model and serial-prefix mappings](#update-model-and-serial-number-mappings) | Completed, ready to use | on request |
| [Create or update a company](#create-or-update-a-company) | Completed, ready to use | Realtime |
| [Get a company details](#get-a-company-details) | Completed, ready to use | on request |
| [Get a registration details](#get-a-registration-details) | Completed, ready to use | on request |
| [Get a daliy list of new registrations](#get-a-daliy-list-of-new-registrations) | Completed, ready to use | daily(or on request) |
| [Update Warranty](#update-warranty) | Completed, ready to use | Realtime |
 * sequence diagramme for the realtime APIs
   - ['Create an account' flow](#create-an-account-flow)
   - ['Update the warranty' flow](#update-the-warranty-flow)

## Authentication

We use API key for authenticate the call. For the details, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

Authentication header

```javascript
"x-api-key": "xxxxxxxxxxxxxxxxx"
```


## APIs

### Update model and serial number mappings

Update all the mappings for SerialNumber Prefix and Model Name

```javascript
PUT /products
```

#### Example

```json
{
  "products":[ 
    {
      "serialNumberPrefix": "6662",
      "modelName": "NCB 20 System"
    },
    {
      "serialNumberPrefix": "0000",
      "modelName": "NCB 00 System"
    },
    {
      "serialNumberPrefix": "1234",
      "modelName": "NCB 1234 Boiler"
    }
  ]
}
```

#### Parameters

| Name | Type | location | Description |
| ---- | ---- | -------- | ----------- |
| projects | string | -- | name of the object array |
| serialNumberPrfix | string | json body | serial number prefix for the model |
| modelName | string | json body | model name description |


#### Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


## Company

### Create or update a company

Create a new company with the company details

```javascript
PUT /companies/:gas_safe_number
```

#### Example

```javascript
PUT /companies/207119
{
  "businessName": "All Gas services",
  "address": "The Panorama Park Street Ashford Kent",
  "postcode": "TN24 8DF",
  "oftecNumber": "xxxx",
}
```

#### Parameters

| Name | Type | location | Description |
| ---- | ---- | -------- | ----------- |
| gas_safe_number | string | path | **key** Gas Safe Number identifier |
| businessName | string | json body | business name of the company |
| address | string | json body | the full address of the company |
| postcode | string | json body | the postcode of the company |
| oftecNumber | string | json body | (optional) the oil and heating tech number of the company |


#### Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


## Company

### Get a company details

Get a company details by the given Gas Safe Number

```javascript
GET /companies/:gas_safe_number
```

#### Example

```javascript
GET /companies/207119
```

#### Parameters

| Name | Type | location | Description |
| ---- | ---- | -------- | ----------- |
| gas_safe_number | string | path | **key** Gas Safe Number identifier |


#### Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok

```javascript
{
    "GasSafeNumber": "123456",
    "BusinessName": "Tamgas",
    "Address": "12 Nelson St",
    "Postcode": "KA26 9AP",
    "OftecNumber": "",
    "Date": "2020-09-18T00:00:00"
}
```


### Get the company details that is created or updated on the given date

```javascript
GET /dates/:todays_date/companies
```

#### Example

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

#### Response

* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


## Installer Users

### Search users by email address

```javascript
GET /search/users?email=:email_address
```

#### Example

```javascript
GET /search/users?email=Alex.ponting@navienuk.com

{
 "Users": [
   {
      "GasSafeNumber": "Test2",
      "Username": "Alextest",
      "InstallerId": "baa8ef8a-35a5-4f82-95e3-4b11d123640a",
      "Email": "Alex.ponting@navienuk.com",
      "FamilyName": "Ponting",
      "GivenName": "Alex",
      "PhoneNumber": "+4407833096083",
      "EmailVerified": true,
      "UserStatus": "CONFIRMED"
  },
  {
      "GasSafeNumber": "",
      "Username": "Alex123",
      "InstallerId": "718400f2-9f76-46f2-986d-6e6a5601dc84",
      "Email": "Alex.ponting@navienuk.com",
      "FamilyName": "Ponting",
      "GivenName": "Alex ",
      "PhoneNumber": "+4407833096083",
      "EmailVerified": true,
      "UserStatus": "CONFIRMED"
  }
 ]
}
```

### Get new installer user details created or updated on the given date

```javascript
GET /dates/:todays_date/users
```

#### Example

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

#### Response

* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


## Boiler registrations

### Get a registration details

```javascript
GET /registrations/:serialNumber
```

#### Parameters

| Name | Type | location | Description |
| ---- | ---- | -------- | ----------- |
| serialNumber | string | path | **key** the serial number of the boiler |


#### Example

```javascript
GET /registrations/0128T18X2438040
```


#### Response

* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok

```javascript
{
 "City": "New Malden",
 "ContactNo": "07663599474",
 "County": "Surrey",
 "Door": "19 Charter Court",
 "EmailAddress": "janghyeonchoi@hotmail.com",
 "FirstName": "Test",
 "InstallationDate": "2020-07-21T00:00:00",
 "LastName": "test",
 "Model": "NCB 24 Combi",
 "PostCode": "KT3 3BL",
 "RegistrationDate": "2020-07-30T00:00:00",
 "RegistrationId": "af8d4241-d26d-11ea-bd5f-73c1a19ae622",
 "SearchIndex": "af8d4241-d26d-11ea-bd5f-73c1a19ae6220128T18X2438040NCB 24 Combi21/07/2020JamesJames07663599474janghyeonchoi@hotmail.com19 Charter CourtLinden GroveNew MaldenSurreyKT3 3BL30/07/202021/07/2020-12bf80404-6c2f-49c4-9eb1-6db07131672f",
 "SerialNumber": "0128T18X2438040",
 "UserId": "2bf80404-6c2f-49c4-9eb1-6db07131672f",
 "WarrantyDate": "2030-07-21T00:00:00",
 "WarrantyYear": 10
}
```



### Get a daliy list of new registrations

```javascript
GET /dates/:todays_date/registrations
```

#### Example

```javascript
GET /dates/20200908/registrations

[
 {
  "City": "Edinburgh",
  "ContactNo": "07540257195",
  "County": "",
  "Door": "49/1",
  "EmailAddress": "thistleservices@btinternet.com",
  "FirstName": "Alex",
  "InstallationDate": "2020-03-01T00:00:00",
  "LastName": "Mcrae",
  "Model": "NCB 28 Combi",
  "PostCode": "EH76RL",
  "RegistrationDate": "2020-03-10T00:00:00",
  "RegistrationId": "e473ada0-6319-11ea-8ea5-5994b062ab58",
  "SearchIndex": "e473ada0-6319-11ea-8ea5-5994b062ab580129X1992565020NCB 28 Combi01/03/2020AlexMcrae07540257195thistleservices@btinternet.com49/1Craigentinny RoadEdinburghEH76RL10/03/202001/03/2020-1b94108b7-ea77-4cb1-b6cb-42e9e55187fd",
  "SerialNumber": "0129X1992565020",
  "UserId": "b94108b7-ea77-4cb1-b6cb-42e9e55187fd",
  "WarrantyDate": "2028-03-01T00:00:00",
  "WarrantyYear": 8
 },
 {
  "City": "Bath",
  "ContactNo": "07931793138",
  "County": "Somerset",
  "Door": "Eden Cottage",
  "EmailAddress": "",
  "FirstName": "Sylvie ",
  "InstallationDate": "2020-03-10T00:00:00",
  "LastName": "Tuk",
  "Model": "ncb-28lhwe",
  "PostCode": "BA2 5DU",
  "RegistrationDate": "2020-03-10T00:00:00",
  "RegistrationId": "acd22fc1-62b5-11ea-ad48-35fc8383ca74",
  "SearchIndex": "acd22fc1-62b5-11ea-ad48-35fc8383ca746664D1662922016ncb-28lhwe10/03/2020Sylvie Tuk07931793138Eden CottageFarrs LaneBathSomersetBA2 5DU10/03/2020-1e9675f20-8e04-4ed2-83b1-4d0389fc097f",
  "SerialNumber": "6664D1662922016",
  "UserId": "e9675f20-8e04-4ed2-83b1-4d0389fc097f",
  "WarrantyDate": "2027-03-10T00:00:00",
  "WarrantyYear": 7
 }
]
```

#### Response

* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


### Update Warranty

The Warranty API allows you to update the warranty year of an existing registration. 

```javascript
PUT /registrations/:serialNumber/warranty
```

#### Example 

```javascript
PUT /registrations/1710U19Y0769003/warranty

{
  "warrantyYear": 7
}
```

#### Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 200 Ok


## Sequence Diagram of realtime operation API

### Create an account flow 
![image](https://user-images.githubusercontent.com/59367560/93712123-9c341780-fb4b-11ea-9292-e2fda7add0d0.png)

### Update the warranty flow 
![image](https://user-images.githubusercontent.com/59367560/93712154-df8e8600-fb4b-11ea-8faa-a1dac9c455e6.png)
