# Iframe Widget usage

The whole site without header and footer can be embedded in an iframe.

## Usage
Include the widget loader file in the page where the widget should be loaded.

```html
<div data-cnx-widget="full"></div>
 
<!-- Either include at the end of the body tag or with the defer attribute to prevent blocking -->
<script defer src="https://YOUR_URL.com/assets/js/cnx-widget.js"></script>
```

The widget loader when loaded will traverse the DOM and insert widgets where widget or container tags are found

## Options

Attribute | Example | Description
--- | --- | ---
locale | data-locale="en-us" | Sets the default locale settings, lowercase
market | data-params="smarket=ES" | Source market, two letter country code
currency | data-params="CURRENCY=GBP" | Sets the default currency, three letter currency code
agentCode | data-params="agentCode=TestUser" | Sets the Agent Code, optional, an arbitrary data

### Examples

```html
<!-- data-locale can be used to select the language of the loaded page, if ommitted then the default locale will be loaded -->
<div data-cnx-widget="full" data-locale="fr-fr"></div>
 
<!-- data-params can be used to pass params supported in the target page -->
<div data-cnx-widget="full" data-params="smarket=ES&age=21"></div>
 
<!-- data-target-page can be used to load a page directly, when ommitted the index will be loaded -->
<div data-cnx-widget="full" data-target-page="search" data-params="..."></div>
 
<!-- all configuration used together -->
<div data-cnx-widget="full"
    data-target-page="search"
    data-locale="de-de"
    data-params="PLABEL=Hamburg+Airport+%28HAM%29&PTYPE=2&PIATA=3602&DLABEL=Hamburg+Airport+%28HAM%29&DTYPE=2&DIATA=3602&PDAY=22&PMONTHYEAR=5.2017&PTIME=12%3A00&DDAY=29&DMONTHYEAR=5.2017&DTIME=12%3A00&smarket=DE&CURRENCY=GBP">
</div>
```

Target page can also be specified with the query parameter cnxpage in the parent window location.search 

All data params are optional without a target page, however when coupled with a target page they act in the same way as standard deep linking.

## Types

Currently the only iframe widget type supported is 'full' which represents the whole site without header or footer.
