# Overview

This describes the resources that make up the Navien UK REST API v1. 
If you have any problems or requests, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

All API access is over HTTPS, and all data is sent and received as JSON.

## All the APIs AppServer Provide
| API Name | Operation Period |
| -------- | ------ |
| [Update model and serial-prefix mappings](#update-model-and-serial-number-mappings) | on request |
| [Create or update a company](#create-or-update-a-company) | Realtime |
| [Update an installer](#update-an-installer) | Realtime |
| [Get a company details](#get-a-company-details) | on request |
| [Get a registration details](#get-a-registration-details) | on request |
| [Get a daily list of new companies](#get-a-daily-list-of-new-companies) | daily (or on request) |
| [Get a daliy list of new registrations](#get-a-daliy-list-of-new-registrations) | daily(or on request) |


### sequence diagramme for the realtime APIs
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

### Update an installer

Update an installer details

```javascript
PATCH /installers/:username
```

#### Example

```javascript
PATCH /installers/40598970-0d95-11eb-8e3a-c394de094129
{
  "email": "andrew.chaa@yahoo.co.uk",
  "familyName": "Chaa",
  "givenName": "Andrew",
  "phoneNumber": "+447590533111"
}
```

#### Parameters

| Name | Type | location | Description |
| ---- | ---- | -------- | ----------- |
| username | string (guid) | path | **key** unique user name |
| familyName | string | json body | family name or last name of the user |
| givenName | string | json body | given name or first name of the user |
| phoneNumber | string | json body | the phone number of the user. It should have **country code** at the beginning |
| oftecNumber | string | json body | (optional) the oil and heating tech number of the company |


#### Response

* 400 Bad Request: if the request is malformed
* 403 Forbidden: if the correct api key is not in the request header
* 204 NoContent: for successful request



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


### Get a daily list of new companies

```javascript
GET /dates/:todays_date/companies
```

#### Example

```javascript
GET /dates/20200908/companies
{
    "DailyList": [
        {
            "GasSafeNumber": "622458",
            "BusinessName": "Oscade Plumbing & heating Services Ltd ",
            "Address": "9 Derby Road ",
            "Postcode": "DE55 7AQ",
            "OftecNumber": "",
            "Date": "2020-09-22T00:00:00"
        },
        {
            "GasSafeNumber": "217049",
            "BusinessName": "Kjy Gas Services",
            "Address": "23 Burnbank",
            "Postcode": "EH20 9NE",
            "OftecNumber": "",
            "Date": "2020-09-22T00:00:00"
        },
        {
            "GasSafeNumber": "226854",
            "BusinessName": "RW Gas Services",
            "Address": "",
            "Postcode": "M27 4UR",
            "OftecNumber": "",
            "Date": "2020-09-22T00:00:00"
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
{
    "DailyList": [{
            "City": "Newbiggin-by-the-Sea",
            "ContactNo": "0777218ㅋㅋㅋㅋ",
            "County": "Northumberland",
            "Door": "Grasmere Terrace",
            "EmailAddress": "email@sky.com",
            "FirstName": "Joe ",
            "InstallationDate": "2020-12-05T00:00:00",
            "LastName": "Biden",
            "Model": "LCB 700 Combi Internal 28KW",
            "PostCode": "NE64 XXX",
            "RegistrationDate": "2020-12-05T00:00:00",
            "RegistrationId": "187b2171-370c-11eb-b652-e5dc519dcde7",
            "SerialNumber": "1706Z19Z1169038",
            "UserId": "7f9e2b9e-1280-4d17-a327-d741c2f284e9",
            "WarrantyDate": "2019-12-05T00:00:00",
            "WarrantyYear": -1,
            "InstallerUsername": "f1cc36c0-2fc4-11eb-bdef-01257a370e44",
            "InstallerEmail": "james@email.com",
            "InstallerFullname": "James Cameron",
            "InstallerGasSafeNumber": "303142"
        },      
        {
            "City": "Lancaster ",
            "ContactNo": "0152000000",
            "County": "lancs",
            "Door": "52",
            "EmailAddress": "a@a.com",
            "FirstName": "Paul",
            "InstallationDate": "2020-09-22T00:00:00",
            "LastName": "Lastname",
            "Model": "NCB 28 Combi",
            "PostCode": "LA1 1SS",
            "RegistrationDate": "2020-09-22T00:00:00",
            "RegistrationId": "1e7e53d1-fcbf-11ea-8ff8-05b04a7969b0",
            "SerialNumber": "0129R19Y1505012",
            "UserId": "dbed8649-d92a-4bc1-a539-a0140bbbb5ff",
            "WarrantyDate": "2027-09-22T00:00:00",
            "WarrantyYear": 7,
            "InstallerUsername": "ffcc36c0-2fc4-11eb-bdef-01257a370e44",
            "InstallerEmail": "matthew@email.com",
            "InstallerFullname": "Matthew Pointer",
            "InstallerGasSafeNumber": "303143"
        }
    ]
}
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
