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
| RateQueryParameterType | Integer | :white_check_mark: | :x: | Defines the rate query parameter type<br/> 1. LocationID (MNX location code)<br/>2. CityID or AirportID<br/>3. LocationCode (Supplier location code) + Supplier GDS code<br/>4. IATA code
| PickUpLocation / ReturnLocation CodeContext | Integer |  :white_check_mark:| :white_check_mark: | Defines the location type of pickup or return location<br/>2007:<br/>1. City/Downtown request<br/>2. Airport request<br/><br/>2012:<br/>cityid: Carnect City ID<br/>aipid: Carnect Airport ID<br/>loccode: Supplier location<br/>code + Supplier GDS code<br/> cityiata: IATA code<br/>aipiata : IATA code |
| VehRentalCore PickUpDateTime | Integer | :white_check_mark:| :white_check_mark: | Defines date and time the customer will pick up his car |
| VehRentalCore ReturnDateTime | Integer | :white_check_mark:| :white_check_mark: | Defines date and time the customer will drop off his car |
| PickUpLocation LocationCode | Integer | :white_check_mark:| :white_check_mark: | Defines the location the customer will pick up his car |
| ReturnLocation LocationCode| Integer | :white_check_mark:| :white_check_mark: | Defines the location the customer will drop off his car |
| DriverType Age | Integer | :white_check_mark: | :x: |Required for underage and senior drivers, to get information about additional charges|
| RateQualifier RateQualifier | String | :white_check_mark: | :x: |Defines a promotion code used to get discounted offers. If the promotion code is invalid, no discount is applied.|



### Examples


In 2012:

```xml
<OTA_VehAvailRateRQ xsi:schemaLocation="http://www.opentravel.org/OTA/2003/05 OTA_VehAvailRateRQ.xsd" Target="Test" Version="1.000" SequenceNmbr="1" PrimaryLangID="EN" ReqRespVersion="small" xmlns="http://www.opentravel.org/OTA/2003/05">
  <POS>
    <Source ISOCountry="DE" ISOCurrency="EUR">
      <RequestorID Type="username" ID_Context="password" />
    </Source>
  </POS>
  <VehAvailRQCore>
    <VehRentalCore PickUpDateTime="2015-10-20T12:00:00" ReturnDateTime="2015-10-27T12:00:00">
      <PickUpLocation LocationCode="1931" CodeContext="aipid" />
      <ReturnLocation LocationCode="1931" CodeContext="aipid" />
    </VehRentalCore>
  </VehAvailRQCore>
</OTA_VehAvailRateRQ>
```

In 2007

```xml
<VehAvailRateRQ xmlns="http://www.opentravel.org/OTA/2003/05" EchoToken="1.0" Version="1.0" ReqRespVersion="large">
  <POS>
    <Source ISOCountry="US">
      <RequestorID Type="username" ID_Context="password" />
    </Source>
  </POS>
  <VehAvailRQCore RateQueryType="Live">
    <RateQueryParameterType>2</RateQueryParameterType>
    <VehRentalCore PickUpDateTime="2018-06-12T09:00:00.000" ReturnDateTime="2018-06-16T09:00:00.000">
      <PickUpLocation LocationCode="1931" CodeContext="1" />
      <ReturnLocation LocationCode="1931" CodeContext="1" />
    </VehRentalCore>
  </VehAvailRQCore>
</VehAvailRateRQ>
```

### Response


| Parameter | Type | 2007 | 2012 | Description |
|-|-|-|-|-|
| ID_Context | String |:white_check_mark:| :white_check_mark: | The unique identifier (reservation reference) |
| VehAvailCore Status | String |:white_check_mark:|:white_check_mark:| Specifies if the vehicle is available ("Available")                  |
| Vehicle AirConditionInd | Boolean |:white_check_mark:|:white_check_mark:| Flag indicating whether the vehicle has air condition or not |
| Vehicle TransmissionType | String |:white_check_mark:|:white_check_mark:| E.g. "manual" or "automatic" |
| Vehicle FuelType | String |:white_check_mark:|:white_check_mark:| E.g. "Petrol" or "Diesel" |
| Vehicle DriveType | String |:white_check_mark:|:white_check_mark:| "4WD", "AWD" or "Unspecified" |
| Vehicle PassengerQuantity | Integer |:white_check_mark:|:white_check_mark:| Max. number of passengers |
| Vehicle BaggageQuantity | Integer |:white_check_mark:|:white_check_mark:| Estimated max. number of pieces of luggage |
| Vehicle VendorCarType | String |:white_check_mark:|:white_check_mark:| Supplier specific code of car type |
| Vehicle Code | String |:white_check_mark:|:white_check_mark:| Supplier specific fleet name |
| Vehicle VehicleType VehicleCategory | Integer |:white_check_mark:|:white_check_mark:| Corresponds to the category of the vehicle, e.g. 'Mini', 'Economy' or 'Compact' or 'Premium'|
| Vehicle VehicleType DoorCount | Integer |:white_check_mark:|:white_check_mark:| Number of doors of the vehicle |
| Vehicle Size | Integer |:white_check_mark:|:white_check_mark:| Corresponds to the size of the vehicle |
| Vehicle VehMakeModel Name | String |:white_check_mark:|:white_check_mark:| Supplier specific name of the fleet |
| Vehicle VehMakeModel Code | String |:white_check_mark:|:white_check_mark:| ACRISS code of the vehicle |
| Vehicle PictureURL | String |:white_check_mark:|:white_check_mark:| URL to an image representation of the car. Images have a fixed width of at least 124px and a dynamic height |
| RentalRate RateDistance Unlimited | Boolean |:white_check_mark:|:white_check_mark:| Flag indicating whether there is a mileage limitation or not |
| RentalRate RateDistance DistUnitName | String |:white_check_mark:|:white_check_mark:| Indicator of the distance unit (only if Unlimited=false), can be either 'km' or 'm' |
| RentalRate VehicleCharge CurrencyCode| String |:white_check_mark:|:white_check_mark:| Two letter code of the currency the rental price is referring to |
| RentalRate VehicleCharge Amount | Decimal |:white_check_mark:|:white_check_mark:| Rental price of the vehicle standalone |
| RentalRate VehicleCharge TaxInclusive| Boolean |:white_check_mark:|:white_check_mark:| Flag indicating whether the local tax is included or not |
| RentalRate VehicleCharge Purpose | String |:white_check_mark:|:white_check_mark:| Indicating if the rental price refers to the original price or the discounted one. |
| RentalRate VehicleCharge RatecodeIndicator | Boolean |:white_check_mark:|:white_check_mark:| Flag to indicate if the rental price has been converted between different currencies|
| TotalCharge EstimatedTotalAmount | Decimal |:white_check_mark:|:white_check_mark:| Estimated total amount of the vehicle from the rental price and all fees that apply |
| Fees | | |:white_check_mark:|:white_check_mark:|Element containing all mandatory fees for this offer|
| Fee / IncludedInRate | Boolean |:white_check_mark:|:white_check_mark:| Flag indicating if the fee has been already included in rental price |
| Fee / IncludedInEstTotalInd | Boolean |:white_check_mark:|:white_check_mark:| Flag indicating if the fee has been already included in EstimatedTotalAmount |
| PricedCoverage | |:white_check_mark:|| Element containing all services (e.g. insurances) included in this offer. Attribute Amount will always be "0.00" and IncludedInRate="true" e.g.: <Charge Amount="0.00" IncludedInRate="true"/> |
| PaymentRule | String |:white_check_mark:|| Defines payment model of offer (refer to OTA2007a payment code table). It contains the PaymentType element which indicates the payment mode. |
| PaymentType | Integer |:white_check_mark:|| Index to indicate the modes of payment, e.g. if the offer is prepaid during reservation or postpaid at the rental station.                   |
| Vendorlocation/dropofflocation value | String |:white_check_mark:|| Denotes whether offer is valid for multiple locations within chosen destination or  not. |
| VehicleCharge/ Purpose | String |:white_check_mark:|| Original: Rental price to be paid in currency of the request. Preferred: Rental price in currency preferred in request. |
| VehicleCharge/RateConvertInd | String |:white_check_mark:|| Indicates whether the original price was converted or not. Pay attention: currency exchangerate is applied at time of reservation. It may differ at time of pick up. |
| TPA_Extensions TermsConditions url | String |:white_check_mark:|| URL to retrieve the supplier specific Terms & Conditions from |
| Warning Code | Integer |:white_check_mark:|| Unique ID of the warning message |
| Warning | String |:white_check_mark:|| Descriptive text of the warning message |
| AdvanceBooking RulesApplyInd | Boolean |:white_check_mark:|| Always true, just for backward compatibility|
