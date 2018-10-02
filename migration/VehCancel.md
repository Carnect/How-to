### Cancellation

#### Request

[Documentation](http://doc.carnect.com/ota2007/cancellation.html)

A cancellation only can be performed by using the reference number and the customer last name.
The cancellation request in OTA 2012 doesn't differ much from the request in OTA 2007.
There is no need of a big change. Except of one element.

OTA 2007
```xml
<UniqueID ID="xxxxxxxxxxxx" Type="14" />
```

OTA 2012
```xml
<UniqueID ID_Context="MNxxxxxx" />
```

#### Response

Response is the same in OTA 2007 and OTA 2012.
