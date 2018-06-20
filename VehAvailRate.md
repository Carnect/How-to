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

|Element|Attribute|2007|2012|Difference|
|-|-|-|-|-|
|Vehicle|CodeContext|:x:|ACRISS|Is empty in 2007|
|Vehicle|VehicleCategory|Numbers|Letters|In 2007 the Vehicle Category is set to Numbers, in 2012 to Lettercodes|
|RateQualifier|VendorRateID|:x:|Showing the unique ID of the Rate|Is moved to another node (&lt;Reference ID_Context=''&gt;)|
|RateComments RateComment|Name|Enum|:x:|Package descriptor is now an attribute (Name)|
|RateRestrictions|MaximumAge/MinimumAge|:x:|Number|Moved as child nodes of RateRestrictions (MinimumAge, MaximumAge)|
|TotalCharge|RateTotalAmount|:x:|Number|Removed. Please use EstimatedTotalAmount|
|Fee||||Changed in different attributes. Please see documentation|
|Reference|ID|:x:|String|Can be removed. Same information in ID_Context|
|Vendor|TravelSector|:x:|String|Can be removed|
|VendorLocation|LocationCode|String|:x:|ID of the location|
|DropOffLocation|LocationCode|String|:x:|ID of the location|
|PricedCoverage Coverage Details|CoverageTextType|:x:|String|Can be removed|
|PricedCoverage Coverage Details Charge||node|:x:|Is a child node of &lt;Details&gt;|
|Calculation||node|:x:|Is a child node from &lt;Charge&gt;|
|PaymentRule|RuleType|:x:|String|Can be removed|
