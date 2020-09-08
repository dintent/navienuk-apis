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

### Update Product Information

Push all product information including S/N and Model mappings

```bash
PUT /products
```

Payload 

```javascript
{
  [
    {
      "serial": "6662", 
      "modelName": "NCB 20 System"
    },
    {
      "serial": "0129", 
      "modelName": "NCB 20 System"
    },
    {
      "serial": "22418", 
      "modelName": "SmartPlus kit - Thermostat & Recevier"
    },
  ]
}


```

## Company

### Create or update a company

Create a new company with the company details

```bash
PUT /companies/:gas_safe_number
```

Payload 

```javascript
{

}
```

### Get the details of companies updated on the given date

```bash
GET /companies/dates/:todays_date
```

Example

```bash
GET /companies/20200908
```

Response

```javascript
{
  "companyName": "test company",
  ....
}
```


### Update Warranty

The Warranty API allows you to update the warranty year of an existing registration. 

```bash
PUT /installers/:installerId/registrations/:registrationId/warranty
```

#### Input
| Name | Type | Description |
| ---- | ---- | ----------- |
| `wrrantyYear` | `integer` | **Required** the warranty year value you want to set |

#### Example

```javascript
{
  "warrantyYear": 7
}
```

## Installer Users

### Get new installers registered on the given date

```bash
GET /users/dates/:todays_date
```

Example

```bash
GET /users/dates/20200908
```

Response

```javascript
{
  "familyName": "Test family name",
  ....
}
```

## Boiler registrations

### Get new registrations

```bash
GET /registrations/dates/:todays_date
```

Example

```bash
GET /registrations/dates/20200908
```

Response

```javascript
{
  ....
}
```


