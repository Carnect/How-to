### Retrieve Reservation

#### Request

[Documentation](http://doc.carnect.com/ota2007/retrieve_reservation.html)

A retrieve reservation only can be performed by using the reference number and the customer last name.
The retrieve reservation request in OTA 2012 doesn't differ much from the request in OTA 2007. There is no need of a big change.

OTA 2007
```xml
<UniqueID ID="xxxxxxxxxxxx" Type="14" />
```

OTA 2012
```xml
<UniqueID ID_Context="MNxxxxxx" />
```

#### Response
