# City Downtown search #

If you want to offer a map for downtown search you can use different endpoints of Carnect's SOAP API.

1. You should make a search for all cities in a selected country.
2. Select from the response the city for which you want to do the downtown search
3. Make a location search for the selected city 
4. Select a car rental location for which you want to search for offers. 
   Or iterate over a selected list of car rental locations.

## City search ##

### Documentation ###
http://doc.carnect.com/ota2007/destination.html#getcities

### Example Request ###

#### URL ####

`https://ota2007a.carhire-solutions.com/destination.asmx`

#### HTTP parameters ####

`SOAPAction:"http://www.opentravel.org/OTA/2003/05/GetCities"`

`Content-Type:text/xml;charset=UTF-8`

#### Body ####

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
  <soap12:Body>
    <VehicleCityRequest xmlns="http://www.opentravel.org/OTA/2003/05">
      <Language>DE</Language>
      <CountryISO>DE</CountryISO>
    </VehicleCityRequest>
  </soap12:Body>
</soap12:Envelope>
```

### Example Response ###

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <soap:Body>
        <VehicleCityResponse xmlns="http://www.opentravel.org/OTA/2003/05">
            <Cities>
                <City id="59" iata="AAH" latitude="50.7781295776367" longitude="6.08849000930786">
                    <Name>Aachen</Name>
                    <RegionID>1</RegionID>
                </City>
                <!-- … more elements -->
                <City id="47" iata="HAM" latitude="53.565278" longitude="10.001389">
                    <Name>Hamburg</Name>
                    <RegionID>1</RegionID>
                </City>
                <!-- … more elements -->
                <City id="377" latitude="50.7147216796875" longitude="12.497730255127">
                    <Name>Zwickau</Name>
                    <RegionID>1</RegionID>
                </City>
            </Cities>
        </VehicleCityResponse>
    </soap:Body>
</soap:Envelope>
```

## Location search ##

### Documentation ###
http://doc.carnect.com/ota2007/location.html#list-of-rental-locations

### Example Request ###

#### URL ####

`https://ota2007a.carhire-solutions.com/service.asmx`

#### HTTP parameters ####

`SOAPAction:"http://www.opentravel.org/OTA/2003/05/getVehLocationSearch"`
`Content-Type:text/xml;charset=UTF-8`

#### Body ####

```xml
<?xml version="1.0" encoding="utf-8"?>
<soapenv:Envelope xmlns:ns="http://www.opentravel.org/OTA/2003/05" xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Header/>
  <soapenv:Body>
	<VehLocationSearchRQ ReqRespVersion="large"  xmlns="http://www.opentravel.org/OTA/2003/05">
	    <POS xmlns="http://www.opentravel.org/OTA/2003/05">
	        <Source ISOCountry="EN">
	            <RequestorID Type="USER" ID_Context="PASSWORD" />
	        </Source>
	    </POS>
      <!-- e.g. Hamburg, Germany -->
	    <VehLocSearchCriterion>
	        <RefPoint CountryCode="DE" RefPointType="1" CityName="47"/>
	    </VehLocSearchCriterion>
	</VehLocationSearchRQ>
  </soapenv:Body>
</soapenv:Envelope>
```

### Example Response ###

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <soap:Header>
        <informationHeader xmlns="http://www.opentravel.org/OTA/2003/05">
            <Successfully>true</Successfully>
            <ProcessingTime>3,1272518 sec</ProcessingTime>
        </informationHeader>
    </soap:Header>
    <soap:Body>
        <VehLocationSearchRS TimeStamp="2018-05-15T17:38:49" Target="Test" Version="3" xmlns="http://www.opentravel.org/OTA/2003/05">
            <VehMatchedLocs>
                <VehMatchedLoc>
                    <LocationDetail AtAirport="false" Code="1260425" Name="Hamburg Wandsbek" CodeContext="HAMI01" ExtendedLocationCode="47-IRHAMI01">
                        <Address>
                            <StreetNmbr>Brauhausstrasse 24-28</StreetNmbr>
                            <AddressLine />
                            <CityName>47-HAMBURG</CityName>
                            <PostalCode>22041</PostalCode>
                            <CountryName Code="DE">Deutschland</CountryName>
                        </Address>
                        <Telephone RPH="+49 (40) 520 187 222" />
                    </LocationDetail>
                    <VehLocSearchCriterion>
                        <Position Latitude="53.5724" Longitude="10.06" />
                    </VehLocSearchCriterion>
                </VehMatchedLoc>
                <!-- .. more nodes -->
                <VehMatchedLoc>
                    <LocationDetail AtAirport="false" Code="7595939" Name="Hamburg Wandsbek Sud" CodeContext="B6" ExtendedLocationCode="47-IGB6">
                        <Address>
                            <StreetNmbr>Ahrensburger Str. 138-148</StreetNmbr>
                            <AddressLine />
                            <CityName>47-HAMBURG</CityName>
                            <PostalCode>22045</PostalCode>
                            <CountryName Code="DE">Deutschland</CountryName>
                        </Address>
                        <Telephone RPH="+49 40 696481610" />
                    </LocationDetail>
                    <VehLocSearchCriterion>
                        <Position Latitude="53.581473" Longitude="10.106512" />
                    </VehLocSearchCriterion>
                </VehMatchedLoc>
            </VehMatchedLocs>
        </VehLocationSearchRS>
    </soap:Body>
</soap:Envelope>
```
