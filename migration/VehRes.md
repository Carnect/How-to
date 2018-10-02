### Reservation

#### Request

[Documentation](http://doc.carnect.com/ota2007/reservation.html)

The reservation request in OTA 2012 doesn't differ from the request in OTA 2007.
There is no need of a big change. Please test it properly.


#### Response


| Parameter | Type | 2007 | 2012| Description |
|---|---|---|---|---|
| success | node | :x: | :white_check_mark: ||
| VehSegmentCore > ConfID | | [ID_Context] is used | [ID] is used| Different attributes are used. In 2012 this Element can occur more than once.  <br/><ul><li>8 (supplier reference)</li><li>16 (Affiliate’s reference)</li><li>43 (Carnect reference number)|
| Vendor[CodeContext] | Attribute | :x: | :white_check_mark: | |
| Vendor | String | :white_check_mark: | :x: | |
| VehRentalCore > PickUpLocation[CodeContext] | String | :white_check_mark: | :white_check_mark: | different code context |
| Vehicle[VendorCarType] | String | :white_check_mark: | :white_check_mark: | different content |
| Vehicle[VendorCarType] | String | :x: | :white_check_mark: | |
| VehSegmentInfo > PaymentRules > PaymentRule[RuleType] | String | :x: | :white_check_mark: | |
| PricedCoverage > Coverage > Details | node |:white_check_mark: |:white_check_mark: |see snippets|
| VehResRSInfo > TPA_Extensions | node |:white_check_mark:|:white_check_mark:| see snippets |

## Snippets

### PricedCoverage

#### 2007

```xml
<PricedCoverage>
    <Coverage CoverageType="Kilometer inclusive: 250 km/Day (0,18 EUR/km)" Code="416">
        <Details>
            <Charge CurrencyCode="EUR" Amount="0.18" TaxInclusive="true" Description="per km: 0.18 EUR" IncludedInEstTotalInd="false">
                <Calculation UnitCharge="0.18" UnitName="PreferredCurrencyPrice" Quantity="1" />
            </Charge>
        </Details>
    </Coverage>
    <Charge />
</PricedCoverage>
```
#### 2012
```xml
<PricedCoverage>
    <Coverage CoverageType="Limited mileage of 300 km/day, maximum 3000 Km per rental, Extra mileage is possible and charged locally at 0,60 €/ KM." Code="416">
        <Details CoverageTextType="Supplement"/>
    </Coverage>
    <Charge CurrencyCode="EUR" Amount="0.60" TaxInclusive="true" Description="per km: 0.60 EUR" IncludedInRate="false" IncludedInEstTotalInd="false">
        <MinMax MaxCharge="0.00"/>
    </Charge>
</PricedCoverage>
```

### VehResRSInfo

#### 2007

```xml
<VehResRSInfo>
    <TPA_Extensions>
        <ProductInformation url="https://createpdf.carhire-solutions.com/en/bookings/EP358607246570/product" temp="https://createpdf.carhire-solutions.com/en/bookings/EP358607246570/product?format=json" xmlns="" />
        <SupplierLogo url="https://static.carhire-solutions.com/images/supplier/logo/logo34.png" xmlns="" />
    </TPA_Extensions>
</VehResRSInfo>

```

#### 2012

```xml
<VehResRSInfo>
    <TPA_Extensions>
        <TermsConditions url="https://createpdf.carhire-solutions.com/termsandconditions.aspx?reservationId=35860588&amp;languageId=2" xmlns=""/>
        <SupplierLogo url="https://static.carhire-solutions.com/images/supplier/logo/logo257.png" xmlns=""/>
    </TPA_Extensions>
</VehResRSInfo>
```
