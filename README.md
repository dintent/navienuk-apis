# Overview

This describes the resources that make up the Navien UK REST API v1. 
If you have any problems or requests, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

All API access is over HTTPS, and all data is sent and received as JSON.

## Authentication

We use API key for authenticate the call. For the details, please contact [DEEPEYES App Support](app@deepeyes.co.uk).

## Update Warranty

The Warranty API allows you to update the warranty year of an existing registration. 

```bash
PUT /registrations/:registrationId/installers/:installerId/warranty
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
