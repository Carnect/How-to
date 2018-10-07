### Availability of Car Offers

#### Request

[Documentation](http://doc.carnect.com/ota2007/quote.html)

| Parameter | Type | 2007 | 2012| Description |
|---|---|---|---|---|
| MaxResponses | Integer | ✅ | ✅ | Defines the maximum number of offers to be returned for each ACRISS-Code category|
| ReqRespVersion | String | ✅| ✅ | Requested version of the response message|
| EchoToken | String | ✅| ✅ | Additional message identification |
| PrimaryLangID | String | ❌ | ✅ | Defines the language of the response |
| ISOCountry | String |  ✅| ✅ | Defines the source market (of the affiliate) and language (format: ISO 3166-1 alpha-2) |
| AgentSine | String | ✅ | ❌ | Agent Code Optional field that can be used to link a reservation to a travel agent |
| PseudoCityCode | String | ✅ | ❌ | Shop reference Optional field that can be used to link a reservation to a affiliate organization unit|
| ISOCurrency | String |  ✅| ✅ | Selects currency to diplay prices in (format: ISO 4217 3-letter code) |
| RequestorID Type | String |  ✅| ✅ | Username (affiliate name) |
| RequestorID ID_Context | String |  ✅| ✅ | Password |
| RateQueryParameterType | Integer | ✅ | ❌ | Defines the rate query parameter type<br/> 1. LocationID (MNX location code)<br/>2. CityID or AirportID<br/>3. LocationCode (Supplier location code) + Supplier GDS code<br/>4. IATA code
| PickUpLocation / ReturnLocation CodeContext | Integer |  ✅| ✅ | Defines the location type of pickup or return location<br/>2007:<br/>1. City/Downtown request<br/>2. Airport request<br/><br/>2012:<br/>cityid: Carnect City ID<br/>aipid: Carnect Airport ID<br/>loccode: Supplier location<br/>code + Supplier GDS code<br/> cityiata: IATA code<br/>aipiata : IATA code |
| VehRentalCore PickUpDateTime | Integer | ✅| ✅ | Defines date and time the customer will pick up his car |
| VehRentalCore ReturnDateTime | Integer | ✅| ✅ | Defines date and time the customer will drop off his car |
| PickUpLocation LocationCode | Integer | ✅| ✅ | Defines the location the customer will pick up his car |
| ReturnLocation LocationCode| Integer | ✅| ✅ | Defines the location the customer will drop off his car |
| DriverType Age | Integer | ✅ | ❌ |Required for underage and senior drivers, to get information about additional charges|
| RateQualifier RateQualifier | String | ✅ | ❌ |Defines a promotion code used to get discounted offers. If the promotion code is invalid, no discount is applied.|



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

#### Differences

|Element|Attribute|2007|2012|Difference|
|-|-|-|-|-|
|Vehicle|CodeContext|❌|ACRISS|Is empty in 2007|
|Vehicle|VehicleCategory|Numbers|Letters|In 2007 the Vehicle Category is set to Numbers, in 2012 to Lettercodes|
|RateQualifier|VendorRateID|❌|Showing the unique ID of the Rate|Is moved to another node (&lt;Reference ID_Context=''&gt;)|
|RateComments RateComment|Name|Enum|❌|Package descriptor is now an attribute (Name)|
|RateRestrictions|MaximumAge/MinimumAge|❌|Number|Moved as child nodes of RateRestrictions (MinimumAge, MaximumAge)|
|TotalCharge|RateTotalAmount|❌|Number|Removed. Please use EstimatedTotalAmount|
|Fee||||Changed in different attributes. Please see documentation|
|Reference|ID|❌|String|Can be removed. Same information in ID_Context|
|Vendor|TravelSector|❌|String|Can be removed|
|VendorLocation|LocationCode|String|❌|ID of the location|
|DropOffLocation|LocationCode|String|❌|ID of the location|
|PricedCoverage Coverage Details|CoverageTextType|❌|String|Can be removed|
|PricedCoverage Coverage Details Charge||node|❌|Is a child node of &lt;Details&gt;|
|Calculation||node|❌|Is a child node from &lt;Charge&gt;|
|PaymentRule|RuleType|❌|String|Can be removed|

### Example

#### 2012
```xml
<VehAvail>
    <VehAvailCore Status="Available">
        <Vehicle AirConditionInd="true" TransmissionType="Manual" FuelType="Petrol" DriveType="Unspecified" PassengerQuantity="4" BaggageQuantity="2" VendorCarType="MBMR" Code="Fiat 500" CodeContext="ACRISS">
            <VehType VehicleCategory="B" DoorCount="2"/>
            <VehClass Size="1"/>
            <VehMakeModel Name="Fiat 500" Code="MBMR"/>
            <PictureURL>https://static.carhire-solutions.com/images/car/OKRENTACAR/small/MBMR.jpg</PictureURL>
        </Vehicle>
        <RentalRate>
            <RateDistance Unlimited="false" Quantity="300" DistUnitName="Km" VehiclePeriodUnitName="RentalPeriod"/>
            <VehicleCharges>
                <VehicleCharge CurrencyCode="EUR" TaxInclusive="true" Description="VAT(TAX)" IncludedInRate="true" Purpose="7"/>
                <VehicleCharge CurrencyCode="EUR" Amount="45.44" TaxInclusive="true" GuaranteedInd="true" RateConvertInd="false" Purpose="original">
                    <Calculation UnitCharge="11.36" UnitName="Day" Quantity="4"/>
                </VehicleCharge>
                <VehicleCharge CurrencyCode="EUR" Amount="45.44" TaxInclusive="true" GuaranteedInd="true" RateConvertInd="true" Purpose="preferred"/>
                <VehicleCharge CurrencyCode="EUR" Amount="0.60" TaxInclusive="true" Description="Limited mileage of 300 km/day, maximum 3000 Km per rental, Extra mileage is possible and charged locally at 0,60 €/ KM." IncludedInRate="false" IncludedInEstTotalInd="false" RateConvertInd="true" Purpose="8">
                    <Calculation UnitCharge="0.60" UnitName="Km"/>
                </VehicleCharge>
                <VehicleCharge CurrencyCode="EUR" Amount="1050" TaxInclusive="true" Description="Upon collection of the car a security deposit will be blocked on the driver’s credit card. This deposit is determined by supplier considering your selected car category. The value of one tank of fuel and possible traffic fines can be additionally blocked on a valid credit card (prepaid debit cards, prepaid credit cards and cash cannot be accepted).&#xD;&#xA;For luxury cars two credit cards in the same name are required for all rentals. The credit card must not be from the same issuer. Please note some suppliers will not accept American Express, Visa Premier or Diners Club credit cards, we strongly recommend to use a Visa or Mastercard. In the event that you fail to produce a valid credit card or have insufficient funds available the car rental agent may refuse to release the vehicle. In this instance no funds will be reimbursed.Estimated deposit amount:: EUR 1050" IncludedInRate="false" IncludedInEstTotalInd="false" RateConvertInd="true" Purpose="Estimated deposit amount"/>
            </VehicleCharges>
            <RateQualifier RateCategory="16" RateQualifier="Micronnexus" RatePeriod="Daily" VendorRateID="9HgEYgE1">
                <RateComments>
                    <RateComment Formatted="true" Language="EN" TextFormat="PlainText">BronzePackage</RateComment>
                    <RateComment Formatted="false" Name="Rate Code">BronzePackage</RateComment>
                </RateComments>
            </RateQualifier>
            <RateRestrictions MinimumAge="19" MaximumAge="75"/>
        </RentalRate>
        <TotalCharge RateTotalAmount="45.44" EstimatedTotalAmount="45.44" CurrencyCode="EUR" RateConvertInd="false"/>
        <Fees>
            <Fee CurrencyCode="EUR" TaxInclusive="true" Description="VAT(TAX)" IncludedInRate="true" Purpose="7"/>
        </Fees>
        <Reference URL="http://www.carhiremarket.com/upsell_parameter.aspx?reference_number=9HgEYgE1&amp;live=true" Type="16" ID="9HgEYgE1" ID_Context="9HgEYgE1"/>
        <Vendor CompanyShortName="OK RENT A C" TravelSector="Car Rental" Code="OK" CodeContext="257"/>
        <VendorLocation CodeContext="06" ExtendedLocationCode="322-OK06" CounterLocation="14" Name="Barcelona Airport">Barcelona Airport</VendorLocation>
        <DropOffLocation CodeContext="06" ExtendedLocationCode="322-OK06" CounterLocation="14" Name="Barcelona Airport">Barcelona Airport</DropOffLocation>
    </VehAvailCore>
    <VehAvailInfo>
        <PricedCoverages>
            <PricedCoverage>
                <Coverage CoverageType="Limited mileage of 300 km/day, maximum 3000 Km per rental, Extra mileage is possible and charged locally at 0,60 €/ KM." Code="416">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.60" TaxInclusive="true" Description="per km: 0.60 EUR" IncludedInRate="false" IncludedInEstTotalInd="false">
                    <MinMax MaxCharge="0.00"/>
                </Charge>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Inclusive Kilometers" Code="6">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="per day: On Request" IncludedInRate="false" IncludedInEstTotalInd="false">
                    <MinMax MaxCharge="0.00"/>
                </Charge>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Collision damage waiver" Code="CDW">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="with excess up to 900 EUR" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Supplementary Liability Insurance" Code="SLI">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Legally required, insurance for damages on the adversarial vehicle, persons and objects- In this offer it is included." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Theft protection" Code="TP">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="with excess up to 900 EUR" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Airport Service Charge" Code="ASC">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Some airports charge a service fee- In this offer it is included." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="One way rental" Code="Oneway">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="not possible" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="PetrolOption" Code="F2E">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Full-to-empty: Pick up with full tank + drop off with an empty tank. Please note the first tank needs to be purchased at pick up, additionally a local NON-REFUNDABLE Service charge of ca. 31€ incl. Vat applies. Unused fuel will be refunded after drop off." GuaranteedInd="true" IncludedInRate="false" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Excess" Code="Excessprice">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" Description="with excess"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="VAT" Code="TAX">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="The rate corresponds with the VAT-rate of the particular country." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Cancellation" Code="Cancellation">
                    <Details CoverageTextType="Supplement"/>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="Up to 48hours before pick-up, cancellation free of charge.  Within 48hours prior to pick-up and in the event of a no-show 100% of the sales price will be charged." GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Cancellation fee" Code="CF">
                    <Details CoverageTextType="Supplement">2018-06-19T14:43:42_2018-12-10T09:00:00</Details>
                    <Details CoverageTextType="Supplement">Up to 48hours before pick-up, cancellation free of charge.  Within 48hours prior to pick-up and in the event of a no-show 100% of the sales price will be charged.</Details>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="0.00" IncludedInRate="true"/>
            </PricedCoverage>
            <PricedCoverage>
                <Coverage CoverageType="Cancellation fee" Code="CF">
                    <Details CoverageTextType="Supplement">2018-12-10T09:00:00_2018-12-12T09:00:00</Details>
                    <Details CoverageTextType="Supplement">Up to 48hours before pick-up, cancellation free of charge.  Within 48hours prior to pick-up and in the event of a no-show 100% of the sales price will be charged.</Details>
                </Coverage>
                <Charge CurrencyCode="EUR" Amount="45.44" IncludedInRate="false"/>
            </PricedCoverage>
        </PricedCoverages>
        <PaymentRules>
            <PaymentRule RuleType="2" PaymentType="4">Prepayment: Full rental price due at time of reservation. For the local pick up the card holder (DRIVER) must provide a valid credit card. Prepaid or debit cards, such as Maestro, Visa electron, Visa Premier or Carte Bleue are not accepted.</PaymentRule>
        </PaymentRules>
        <TPA_Extensions>
            <TermsConditions url="http://static.carhire-solutions.com/pdf/mnx_t-c_en.PDF" xmlns=""/>
            <ProductInformation url="https://createpdf.carhire-solutions.com/termsandconditions.aspx?reference=9HgEYgE1&amp;languageId=2" xmlns=""/>
            <SupplierLogo url="https://static.carhire-solutions.com/images/supplier/logo/logo257.png" xmlns=""/>
        </TPA_Extensions>
    </VehAvailInfo>
    <AdvanceBooking RulesApplyInd="true"/>
</VehAvail>
```

#### 2007

```xml
<VehAvail>
  <VehAvailCore Status="Available">
    <Vehicle AirConditionInd="true" TransmissionType="Manual" FuelType="Petrol" DriveType="Unspecified" PassengerQuantity="4" BaggageQuantity="2" VendorCarType="MBMR" Code="Fiat 500" CodeContext="">
      <VehType VehicleCategory="1" DoorCount="2"/>
      <VehClass Size="1"/>
      <VehMakeModel Name="Fiat 500" Code="MBMR"/>
      <PictureURL>https://static.carhire-solutions.com/images/car/OKRENTACAR/small/MBMR.jpg</PictureURL>
    </Vehicle>
    <RentalRate>
      <RateDistance Unlimited="false" Quantity="300" DistUnitName="Km" VehiclePeriodUnitName="Day"/>
      <VehicleCharges>
        <VehicleCharge CurrencyCode="EUR" Amount="73.18" TaxInclusive="true" Purpose="original" RateConvertInd="true">
          <Calculation UnitName="Day" Quantity="4"/>
        </VehicleCharge>
        <VehicleCharge CurrencyCode="EUR" Amount="73.18" TaxInclusive="true" Purpose="preferred" RateConvertInd="true"/>
        <VehicleCharge CurrencyCode="EUR" Amount="0.60" Description="Limited mileage of 300 km/day, maximum 3000 Km per rental, Extra mileage is possible and charged locally at 0,60 €/ KM." Purpose="8"/>
        <VehicleCharge
          CurrencyCode="EUR"
          Amount="1050"
          TaxInclusive="true"
          Description="Upon collection of the car a security deposit will be blocked on the driver’s credit card. This deposit is determined by supplier considering your selected car category. The value of one tank of fuel and possible traffic fines can be additionally blocked on a valid credit card (prepaid debit cards, prepaid credit cards and cash cannot be accepted).&#xD;&#xA;For luxury cars two credit cards in the same name are required for all rentals. The credit card must not be from the same issuer. Please note some suppliers will not accept American Express, Visa Premier or Diners Club credit cards, we strongly recommend to use a Visa or Mastercard. In the event that you fail to produce a valid credit card or have insufficient funds available the car rental agent may refuse to release the vehicle. In this instance no funds will be reimbursed.Estimated deposit amount:: EUR 1050"
          IncludedInEstTotalInd="false"
          Purpose="Estimated deposit amount"
          RateConvertInd="true"/>
      </VehicleCharges>
      <RateQualifier VendorRateID="Micronnexus">
        <RateComments>
          <RateComment Name="BronzePackage"/>
        </RateComments>
      </RateQualifier>
      <RateRestrictions>
        <MinimumAge>19</MinimumAge>
        <MaximumAge>75</MaximumAge>
        <NoShowFeeInd>false</NoShowFeeInd>
      </RateRestrictions>
    </RentalRate>
    <TotalCharge CurrencyCode="EUR" EstimatedTotalAmount="73.18" RateConvertInd="false"/>
    <Fees>
      <Fee CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="VAT(TAX)" IncludedInRate="true" IncludedInEstTotalInd="true"/>
    </Fees>
    <Reference URL="http://www.carhiremarket.com/upsell_parameter.aspx?reference_number=Ah_RZQE1&amp;live=true" Type="16" ID_Context="Ah_RZQE1"/>
    <Vendor TravelSector="Car Rental" Code="OK" CodeContext="257">OK RENT A CAR</Vendor>
    <VendorLocation LocationCode="7542416" CodeContext="06" ExtendedLocationCode="322-OK06" CounterLocation="14" Name="Barcelona Airport">Barcelona Airport</VendorLocation>
    <DropOffLocation LocationCode="7542416" CodeContext="06" ExtendedLocationCode="322-OK06" CounterLocation="14" Name="Barcelona Airport"/>
  </VehAvailCore>
  <VehAvailInfo>
    <PricedCoverages>
      <PricedCoverage>
        <Coverage CoverageType="Limited mileage of 300 km/day, maximum 3000 Km per rental, Extra mileage is possible and charged locally at 0,60 €/ KM." Code="416">
          <Details>
            <Charge CurrencyCode="EUR" Amount="0.60" TaxInclusive="true" Description="per km: 0.60 EUR" IncludedInEstTotalInd="false">
              <Calculation UnitCharge="0.60" UnitName="PreferredCurrencyPrice" Quantity="1"/>
            </Charge>
          </Details>
        </Coverage>
        <Charge/>
      </PricedCoverage>
      <PricedCoverage>
        <Coverage CoverageType="Collision damage waiver" Code="CDW">
          <Details>
            <Charge Amount="0.00" IncludedInRate="true"/>
          </Details>
        </Coverage>
        <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="with excess up to 900 EUR" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
      </PricedCoverage>
      <PricedCoverage>
        <Coverage CoverageType="Supplementary Liability Insurance" Code="SLI">
          <Details>
            <Charge Amount="0.00" IncludedInRate="true"/>
          </Details>
        </Coverage>
        <Charge
          CurrencyCode="EUR"
          Amount="0.00"
          TaxInclusive="true"
          Description="Legally required, insurance for damages on the adversarial vehicle, persons and objects- In this offer it is included."
          GuaranteedInd="true"
          IncludedInRate="true"
          IncludedInEstTotalInd="true"/>
      </PricedCoverage>
      <PricedCoverage>
        <Coverage CoverageType="Theft protection" Code="TP">
          <Details>
            <Charge Amount="0.00" IncludedInRate="true"/>
          </Details>
        </Coverage>
        <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="with excess up to 900 EUR" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
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
        <Charge CurrencyCode="EUR" Amount="0.00" TaxInclusive="true" Description="not possible" GuaranteedInd="true" IncludedInRate="true" IncludedInEstTotalInd="true"/>
      </PricedCoverage>
      <PricedCoverage>
        <Coverage CoverageType="Fuel Information" Code="F2E">
          <Details>
            <Charge Amount="0.00" IncludedInRate="true"/>
          </Details>
        </Coverage>
        <Charge
          CurrencyCode="EUR"
          Amount="0.00"
          TaxInclusive="true"
          Description="Full-to-empty: Pick up with full tank + drop off with an empty tank. Please note the first tank needs to be purchased at pick up, additionally a local NON-REFUNDABLE Service charge of ca. 31€ incl. Vat applies. Unused fuel will be refunded after drop off."
          GuaranteedInd="true"
          IncludedInRate="true"
          IncludedInEstTotalInd="true"/>
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
            <Coverage CoverageType="2018-06-20T10:11:27_2018-08-10T09:00:00"/>
            <Charge CurrencyCode="EUR" Amount="0.00" Description="Up to 48hours before pick-up, cancellation free of charge.  Within 48hours prior to pick-up and in the event of a no-show 100% of the sales price will be charged." IncludedInRate="true"/>
          </Details>
          <Details>
            <Coverage CoverageType="2018-08-10T09:00:00_2018-08-12T09:00:00"/>
            <Charge CurrencyCode="EUR" Amount="73.18" Description="Up to 48hours before pick-up, cancellation free of charge.  Within 48hours prior to pick-up and in the event of a no-show 100% of the sales price will be charged."/>
          </Details>
        </Coverage>
        <Charge IncludedInRate="true"/>
      </PricedCoverage>
    </PricedCoverages>
    <PaymentRules>
      <PaymentRule PaymentType="4">Prepayment: Full rental price due at time of reservation. For the local pick up the card holder (DRIVER) must provide a valid credit card. Prepaid or debit cards, such as Maestro, Visa electron, Visa Premier or Carte Bleue are not accepted.</PaymentRule>
    </PaymentRules>
    <TPA_Extensions>
      <TermsConditions url="https://static.carhire-solutions.com/pdf/cnx_tac_en-gb.pdf" xmlns=""/>
      <ProductInformation url="https://createpdf.carhire-solutions.com/en/products/Ah_RZQE1" temp="https://createpdf.carhire-solutions.com/en/products/Ah_RZQE1?format=json" xmlns=""/>
      <SupplierLogo url="https://static.carhire-solutions.com/images/supplier/logo/logo257.png" xmlns=""/>
    </TPA_Extensions>
  </VehAvailInfo>
  <AdvanceBooking RulesApplyInd="true"/>
</VehAvail>
```
