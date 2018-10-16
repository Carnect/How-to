# Map Based Search #

If you want to display a map and list of offers to the end user, the following approach is recommended:

1. Show a list of available *rental locations* in the area around the geo coordinate first using the [location API with the geo coordinate](http://doc.carnect.com/ota2007/location.html#search-by-geo-coordinate-latitude-longitude).
2. Then query for available *offers* in this area using the [availability API with this geo coordinate](http://doc.carnect.com/ota2007/quote.html#by-geo-coordinates-see-geo-coordinates).


## Rental Locations ##

### Documentation ###
<http://doc.carnect.com/ota2007/location.html#search-by-geo-coordinate-latitude-longitude>

### Example Request ###

#### URL ####

`https://ota2007a.carhire-solutions.com/service.asmx`

#### HTTP parameters ####

`SOAPAction:"http://www.opentravel.org/OTA/2003/05/getVehLocationSearch"`

`Content-Type:text/xml;charset=UTF-8`

#### Body ####

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
xmlns:ns="http://www.opentravel.org/OTA/2003/05">
  <soapenv:Header />
  <soapenv:Body>
    <VehLocationSearchRQ xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://www.opentravel.org/OTA/2003/05">
      <POS>
        <Source ISOCountry="EN">
          <RequestorID Type="USER" ID_Context="PASSWORD" />
        </Source>
        <Source ISOCountry="EN" />
      </POS>
      <VehLocSearchCriterion Ranking="50">
        <RefPoint RefPointType="8" StateProv="1" CountryCode="DE" />
        <Position Latitude="53.542989" Longitude="9.986336" />
        <Radius DistanceMax="1" DistanceMeasure="km" />
      </VehLocSearchCriterion>
	 <Vendor>GR</Vendor>
    </VehLocationSearchRQ>
  </soapenv:Body>
</soapenv:Envelope>
```

### Example Response ###

```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Header>
    <informationHeader xmlns="http://www.opentravel.org/OTA/2003/05">
      <Successfully>true</Successfully>
      <ProcessingTime>1,2421909 sec</ProcessingTime>
    </informationHeader>
  </soap:Header>
  <soap:Body>
    <VehLocationSearchRS xmlns="http://www.opentravel.org/OTA/2003/05" TimeStamp="2018-10-16T09:25:50" Version="3">
      <VehMatchedLocs>
        <VehMatchedLoc>
          <LocationDetail AtAirport="false" Code="1221337" Name="HAMBURG  ROEDINGSMARKT" CodeContext="HAMC01" ExtendedLocationCode="47-EPHAMC01">
            <Address Type="7">
              <StreetNmbr>ROEDINGSMARKT 14</StreetNmbr>
              <CityName>47-HAMBURG</CityName>
              <PostalCode>20459</PostalCode>
              <CountryName Code="DE">Germany</CountryName>
            </Address>
            <Telephone PhoneTechType="1" PhoneNumber="+49 40 3786220"/>
            <Telephone PhoneTechType="2" PhoneNumber="+49 40 37862266"/>
            <AdditionalInfo>
              <ParkLocation Location=""/>
              <OperationSchedules>
                <OperationSchedule>
                  <OperationTimes>
                    <OperationTime Mon="true" Start="07:00" End="18:00"/>
                    <OperationTime Tue="true" Start="07:00" End="18:00"/>
                    <OperationTime Weds="true" Start="07:00" End="18:00"/>
                    <OperationTime Thur="true" Start="07:00" End="18:00"/>
                    <OperationTime Fri="true" Start="07:00" End="18:00"/>
                    <OperationTime Sat="true" Start="08:00" End="12:00"/>
                    <OperationTime Sun="true" Start="09:00" End="11:00"/>
                  </OperationTimes>
                </OperationSchedule>
              </OperationSchedules>
              <TPA_Extensions>
                <Position Latitude="53.5472" Longitude="9.9855"/>
              </TPA_Extensions>
            </AdditionalInfo>
          </LocationDetail>
          <VehLocSearchCriterion>
            <Position Latitude="53.5472" Longitude="9.9855"/>
          </VehLocSearchCriterion>
        </VehMatchedLoc>
        <VehMatchedLoc>
          <LocationDetail AtAirport="false" Code="7040462" Name="HAMBURG  ROEDINGSMARKT" CodeContext="HAMC01" ExtendedLocationCode="47-KYHAMC01">
            <Address Type="7">
              <StreetNmbr>ROEDINGSMARKT 14</StreetNmbr>
              <CityName>47-HAMBURG</CityName>
              <PostalCode>20459</PostalCode>
              <CountryName Code="DE">Germany</CountryName>
            </Address>
            <Telephone PhoneTechType="1" PhoneNumber="+49 40 3786220"/>
            <Telephone PhoneTechType="2" PhoneNumber="+49 40 37862266"/>
            <AdditionalInfo>
              <ParkLocation Location=" * Serviced by EUROPCAR *"/>
              <OperationSchedules>
                <OperationSchedule>
                  <OperationTimes>
                    <OperationTime Mon="true" Start="07:00" End="18:00"/>
                    <OperationTime Tue="true" Start="07:00" End="18:00"/>
                    <OperationTime Weds="true" Start="07:00" End="18:00"/>
                    <OperationTime Thur="true" Start="07:00" End="18:00"/>
                    <OperationTime Fri="true" Start="07:00" End="18:00"/>
                    <OperationTime Sat="true" Start="08:00" End="12:00"/>
                    <OperationTime Sun="true" Start="09:00" End="11:00"/>
                  </OperationTimes>
                </OperationSchedule>
              </OperationSchedules>
              <TPA_Extensions>
                <Position Latitude="53.5472" Longitude="9.9855"/>
              </TPA_Extensions>
            </AdditionalInfo>
          </LocationDetail>
          <VehLocSearchCriterion>
            <Position Latitude="53.5472" Longitude="9.9855"/>
          </VehLocSearchCriterion>
        </VehMatchedLoc>

        <!-- … more elements -->

      </VehMatchedLocs>
    </VehLocationSearchRS>
  </soap:Body>
</soap:Envelope>
```

## Offers ##

### Documentation ###
<http://doc.carnect.com/ota2007/quote.html#by-geo-coordinates-see-geo-coordinates>

### Example Request ###

#### URL ####

`https://ota2007a.carhire-solutions.com/service.asmx`

#### HTTP parameters ####

`SOAPAction:"http://www.opentravel.org/OTA/2003/05/getVehAvailRate"`
`Content-Type:text/xml;charset=UTF-8`

#### Body ####

```xml
<soapenv:Envelope xmlns:ns="http://www.opentravel.org/OTA/2003/05" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Header/>
  <soapenv:Body>
    <VehAvailRateRQ EchoToken="1.0" ReqRespVersion="large" Version="1.0" xmlns="http://www.opentravel.org/OTA/2003/05">
      <POS>
        <Source ISOCountry="EN">
          <RequestorID Type="USER" ID_Context="PASSWORD" />
        </Source>
        <Source ISOCountry="IT"/>
      </POS>
      <VehAvailRQCore RateQueryType="Live">
        <RateQueryParameterType>6</RateQueryParameterType>
        <VehRentalCore PickUpDateTime="2018-11-15T07:38:07+00:00" ReturnDateTime="2018-11-22T07:38:07+00:00">
		 <PickUpLocation LocationCode="53.5466451,10.0135512" CodeContext="3" />
         <ReturnLocation LocationCode="53.5466451,10.0135512" CodeContext="3" />
        </VehRentalCore>
        <DriverType Age="35" />
      </VehAvailRQCore>
    </VehAvailRateRQ>
  </soapenv:Body>
</soapenv:Envelope>
```

### Example Response ###

```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Header>
    <informationHeader xmlns="http://www.opentravel.org/OTA/2003/05">
      <Successfully>true</Successfully>
      <ProcessingTime>5.6273055</ProcessingTime>
    </informationHeader>
  </soap:Header>
  <soap:Body>
    <VehAvailRateRS xmlns="http://www.opentravel.org/OTA/2003/05" EchoToken="3.5496194;5.6273055" TimeStamp="2018-10-16T09:42:27" Version="3">
      <VehAvailRSCore>
        <VehRentalCore PickUpDateTime="2018-11-15T08:42:00" ReturnDateTime="2018-11-22T08:42:00" Quantity="144">
          <PickUpLocation LocationCode="47"/>
          <ReturnLocation LocationCode="47"/>
        </VehRentalCore>
        <VehVendorAvails>
          <VehVendorAvail>
            <VehAvails>
              <VehAvail>
                <VehAvailCore Status="Available">
                  <Vehicle AirConditionInd="true" TransmissionType="Manual" FuelType="Petrol" DriveType="Unspecified" PassengerQuantity="4" BaggageQuantity="1" VendorCarType="MBMR" Code="FORD KA" CodeContext="">
                    <VehType VehicleCategory="1" DoorCount="2"/>
                    <VehClass Size="1"/>
                    <VehMakeModel Name="FORD KA" Code="MBMR"/>
                    <PictureURL>https://static.carhire-solutions.com/images/car/Enterprise/small/t_MBMR_DE.jpg</PictureURL>
                  </Vehicle>
                  <RentalRate>
                    <RateDistance Unlimited="false" Quantity="2100" DistUnitName="Km" VehiclePeriodUnitName="RentalPeriod"/>
                    <VehicleCharges>
                      <VehicleCharge CurrencyCode="EUR" Amount="131.76" TaxInclusive="true" Purpose="original" RateConvertInd="true">
                        <Calculation UnitName="Day" Quantity="7"/>
                      </VehicleCharge>
                      <VehicleCharge CurrencyCode="EUR" Amount="131.76" TaxInclusive="true" Purpose="preferred" RateConvertInd="true"/>
                      <VehicleCharge CurrencyCode="EUR" Amount="0.25" Description="Kilometer inclusive: 2100 km (0,25 EUR/km)" Purpose="8"/>
                      <VehicleCharge CurrencyCode="EUR" Amount="1000" TaxInclusive="true" Description="Upon collection of the car a security deposit will be blocked on the driver&#x2019;s credit card. This deposit is determined by supplier considering your selected car category. The value of one tank of fuel and possible traffic fines can be additionally blocked on a valid credit card (prepaid debit cards, prepaid credit cards and cash cannot be accepted).&#13;&#10;For luxury cars two credit cards in the same name are required for all rentals. The credit card must not be from the same issuer. Please note some suppliers will not accept American Express, Visa Premier or Diners Club credit cards, we strongly recommend to use a Visa or Mastercard. In the event that you fail to produce a valid credit card or have insufficient funds available the car rental agent may refuse to release the vehicle. In this instance no funds will be reimbursed.Estimated deposit amount:: EUR 1000" IncludedInEstTotalInd="false" Purpose="Estimated deposit amount" RateConvertInd="true"/>
                    </VehicleCharges>
                    <RateQualifier VendorRateID="MNGPRF1">
                      <RateComments>
                        <RateComment Name="SilverPackage"/>
                      </RateComments>
                    </RateQualifier>
                    <RateRestrictions>
                      <MinimumAge>25</MinimumAge>
                      <MaximumAge>80</MaximumAge>
                      <NoShowFeeInd>false</NoShowFeeInd>
                    </RateRestrictions>
                  </RentalRate>
                  <TotalCharge CurrencyCode="EUR" EstimatedTotalAmount="131.76" RateConvertInd="false"/>
                  <Fees>
                    <Fee CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Location service charge(LSC)" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    <Fee CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="VAT(TAX)" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                  </Fees>
                  <Reference URL="http://www.carhiremarket.com/upsell_parameter.aspx?reference_number=Y6_TagM1&amp;live=true" Type="16" ID_Context="Y6_TagM1"/>
                  <Vendor TravelSector="Car Rental" Code="ET" CodeContext="61">Enterprise</Vendor>
                  <VendorLocation LocationCode="1451170" CodeContext="HAMC63" ExtendedLocationCode="47-ETHAMC63" Name="HAMBURG CITY SUED">53.54555,10.02958</VendorLocation>
                  <DropOffLocation LocationCode="1451170" CodeContext="HAMC63" ExtendedLocationCode="47-ETHAMC63" Name="HAMBURG CITY SUED">53.54555,10.02958</DropOffLocation>
                </VehAvailCore>
                <VehAvailInfo>
                  <PricedCoverages>
                    <PricedCoverage>
                      <Coverage CoverageType="Kilometer inclusive: 2100 km (0,25 EUR/km)" Code="416">
                        <Details>
                          <Charge CurrencyCode="EUR" Amount="0.25" TaxInclusive="false" Description="per km: 0.25 EUR" IncludedInEstTotalInd="false">
                            <Calculation UnitCharge="0.25" UnitName="PreferredCurrencyPrice" Quantity="1"/>
                          </Charge>
                        </Details>
                      </Coverage>
                      <Charge/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Other taxes and service charges" Code="418">
                        <Details>
                          <Charge CurrencyCode="EUR" Amount="16.83" TaxInclusive="true" Description="per rental: 16.83 EUR" IncludedInRate="true" IncludedInEstTotalInd="true">
                            <Calculation UnitCharge="16.83" UnitName="PreferredCurrencyPrice" Quantity="1"/>
                          </Charge>
                        </Details>
                      </Coverage>
                      <Charge/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Location service charge" Code="LSC">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="An additional service charge applies at some airports, railway stations and ports- In this offer it is included." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Collision damage waiver" Code="CDW">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="with excess up to 850 EUR" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Supplementary Liability Insurance" Code="SLI">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Legally required, insurance for damages on the adversarial vehicle, persons and objects- In this offer it is included." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Theft protection" Code="TP">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="with excess up to 850 EUR" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Airport Service Charge" Code="ASC">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Some airports charge a service fee- In this offer it is included." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="One way rental" Code="OW">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Onewayrental fees are included" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Fuel Information" Code="F2F">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Full to Full: Pick up and drop off with a full tank. If the car is not returned with a full tank, suppliers will charge fuel plus refueling charges. " GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="VAT" Code="TAX">
                        <Details>
                          <Charge Amount="0.00" IncludedInRate="true"/>
                        </Details>
                      </Coverage>
                      <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="The rate corresponds with the VAT-rate of the particular country." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
                    </PricedCoverage>
                    <PricedCoverage>
                      <Coverage CoverageType="Cancellation fee" Code="CF">
                        <Details>
                          <Coverage CoverageType="2018-10-16T09:42:26_2018-11-13T08:42:00"/>
                          <Charge CurrencyCode="EUR" Amount="0.00" Description="Up to 48hours before pick-up, cancellation free of charge.  Within 48hours prior to pick-up and in the event of a no-show 100% of the sales price will be charged." IncludedInRate="true"/>
                        </Details>
                        <Details>
                          <Coverage CoverageType="2018-11-13T08:42:00_2018-11-15T08:42:00"/>
                          <Charge CurrencyCode="EUR" Amount="131.76" Description="Up to 48hours before pick-up, cancellation free of charge.  Within 48hours prior to pick-up and in the event of a no-show 100% of the sales price will be charged."/>
                        </Details>
                      </Coverage>
                      <Charge IncludedInRate="true"/>
                    </PricedCoverage>
                  </PricedCoverages>
                  <PaymentRules>
                    <PaymentRule PaymentType="4">Prepayment: Full rental price due at time of reservation. For the local pick up the card holder (DRIVER) must provide a valid credit card.  Prepaid or debit cards, such as Maestro, Visa electron, Visa Premier or Carte Bleue are not accepted.</PaymentRule>
                    <PaymentRule PaymentType="5">Credit Card is required</PaymentRule>
                  </PaymentRules>
                  <TPA_Extensions>
                    <TermsConditions xmlns="" url="https://static.carhire-solutions.com/pdf/cnx_tac_en-gb.pdf"/>
                    <ProductInformation xmlns="" url="https://createpdf.carhire-solutions.com/en/products/Y6_TagM1" temp="https://createpdf.carhire-solutions.com/en/products/Y6_TagM1?format=json"/>
                    <SupplierLogo xmlns="" url="https://static.carhire-solutions.com/images/supplier/logo/logo61.png"/>
                  </TPA_Extensions>
                </VehAvailInfo>
                <AdvanceBooking RulesApplyInd="true"/>
              </VehAvail>

        <!-- … more elements -->

            </VehAvails>
          </VehVendorAvail>
        </VehVendorAvails>
      </VehAvailRSCore>
    </VehAvailRateRS>
  </soap:Body>
</soap:Envelope>
```
