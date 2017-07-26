# Amyanpoh API Documentation

The Amyanpoh API lets partners integrate and interact with our delivery life programmatically. 
All URIs below are relative to https://api.amyanpoh.com/v1/

## General
All access requires an api token. You can specify this in as an 'x-api-key' field in your request header.
The best way to handle exceptions is to use the response code in the response header. Succesfully executed queries always return a HTTP code of 200.

## Paths
### Pricing
Returns pricing for a given item based on the rates from the contract or SLA.
**URI:** /packages/pricing
**method:** POST

**Body params:**
	Required
	| param | datatype | description |
	| ---- | ---- | ---- |
	| 'weight' | int or float | in kilograms |
	|'size'| [ints or floats]|	[l, w, h], each in inches|
	|'destination'|	string|	as a region suggested by the API response|
	|'price'|	int or float|	in kyats. Used to determine the cash handling fee.|	
	

### Get Packages
Read data about your existing packages from the Amyanpoh database.
**URI:** /packages
**method:** GET

**Query params:**
Performing this action without any filters will return your last 100 packages. The following filters are optional and can help you to search more specificly. The date filter currently only works if both start and end dates are present. The filters are applied in the order they are listed.
Optional:
| param | datatype | description |
| ---- | ---- | ---- |
| 'start_date' | int | Only show packages created after this [UNIX date](https://en.wikipedia.org/wiki/Unix_time) |
| 'end_date' | int | Only show packages created before this date |
| 'delivered' | string | If true, only shows delivered packages |
| 'last' | int | Return the last n results. Max 400. |

Example query: ` api.amyanpoh.com/v1/packages?start_date=1501029572&end_date=1501030747&last=6&delivered=true `

### Make Package
Creates a single package object in the Amyanpoh database under your account.
**URI:** /packages
**method:** POST

**Body params**:
There are several required parameters, and several optional parameters when creating a package. Optional parameters default to the most common choice.
Required:
| param | datatype | description |
| ---- | ---- | ---- |
|'name'	| string | The end customer's name |
| 'address'	| string | The end customer's address |
| 'phone' |string | Be careful not to pass ints starting with 0, as they can be read as octal digits |
| 'cod'	| int |	The amount in kyats to be collected from the end customer on your behalf |
Optional:
param | datatype | description
--- | --- | ---
'payment_method' | string | Defaults to 'Cash on Delivery'
'description' | string | Description visible to the end customer if customer tracking is activated
'latitude' | float | Coordinate of the destination
'longitude' | float | Coordinate of the destination
'region' | string | Defaults to 'ygn'. Options are ['ygn', 'mdy', 'npd', 'other']
	
Param | Datatype | Description
--- | --- | ---
'payment_method' | string | Defaults to 'Cash on Delivery'
'description' | string | Description visible to the end customer if customer tracking is activated
'latitude' | float | Coordinate of the destination
'longitude' | float | Coordinate of the destination
'region' | string | Defaults to 'ygn'. Options are ['ygn', 'mdy', 'npd', 'other']
