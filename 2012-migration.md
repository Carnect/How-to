# Migration 2012-2007 Guide

In general: Please use the [online documentation](http://doc.carnect.com/ota2007/). Our main OTA API (2007) is documented in detail. You will need it for the migration.

## Available SOAP methods
* [Availability of Car Offers]()
* [Raterules]()
* [Reservation]()
* [Cancellation]()
* [Retrieve Reservation]()


### Availability of Car Offers

#### Request

[Documentation](http://doc.carnect.com/ota2007/quote.html)

| Parameter | Type | 2007 | 2012| Description |
|---|---|---|---|---|
| MaxResponses | Integer | :white_check_mark:| :white_check_mark: | Defines the maximum number of offers to be returned for each ACRISS-Code category|
| ReqRespVersion | String | :white_check_mark:| :white_check_mark: | Requested version of the response message|
| EchoToken | String | :white_check_mark:| :white_check_mark: | Additional message identification |
| PrimaryLangID | String | :x: | :white_check_mark: | Defines the language of the response |
| ISOCountry | String |  :white_check_mark:| :white_check_mark: | Defines the source market (of the affiliate) and language (format: ISO 3166-1 alpha-2) |
| AgentSine | String | :white_check_mark: | :x: | Agent Code Optional field that can be used to link a reservation to a travel agent |
| PseudoCityCode | String | :white_check_mark: | :x: | Shop reference Optional field that can be used to link a reservation to a affiliate organization unit| 
| ISOCurrency | String |  :white_check_mark:| :white_check_mark: | Selects currency to diplay prices in (format: ISO 4217 3-letter code) |
| RequestorID Type | String |  :white_check_mark:| :white_check_mark: | Username (affiliate name) |
| RequestorID ID_Context | String |  :white_check_mark:| :white_check_mark: | Password |
| PickUpLocation / ReturnLocation CodeContext | Integer |  :white_check_mark:| :white_check_mark: | Defines the location type of pickup or return location |
| VehRentalCore PickUpDateTime | Integer | :white_check_mark:| :white_check_mark: | Defines date and time the customer will pick up his car |
| VehRentalCore ReturnDateTime | Integer | :white_check_mark:| :white_check_mark: | Defines date and time the customer will drop off his car |
| PickUpLocation LocationCode | Integer | :white_check_mark:| :white_check_mark: | Defines the location the customer will pick up his car |
| ReturnLocation LocationCode| Integer | :white_check_mark:| :white_check_mark: | Defines the location the customer will drop off his car |
| DriverType Age | Integer | :white_check_mark: | :x: |Required for underage and senior drivers, to get information about additional charges|
| RateQualifier RateQualifier | String | :white_check_mark: | :x: |Defines a promotion code used to get discounted offers. If the promotion code is invalid, no discount is applied.|

In 2012:

```

```
