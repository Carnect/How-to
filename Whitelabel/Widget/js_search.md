# JS Search Widget

## Implementation

For widgets to display correctly the partner must have a widgets.scss file to be compiled. (See carhiremarket for example content).

```html
<!-- To initialise a widget container -->
<div data-cnx-container data-locale="en-gb">
    <!-- any data-component tags here will be initialised --> 
    <div data-component="search-form" data-display-mode="horizontal|fixed"></div>
</div>
 
<!-- All supported url params can be added as data params -->
<div data-cnx-container
data-currency="GBP"
data-ptype="2"
data-piata="3602"
...
>
</div>
```

## View

We support 2 different views. Horizontal and Fixed. Just changed data-display-mode attribute.

### Options

Attribute | Example | Description
--- | --- | ---
locale | `data-locale="en-us"` | Sets the default locale settings, lowercase
currency | `data-currency="CURRENCY=GBP"` | Sets the default currency, three letter currency code

If you want to redirect to our Iframe Widget, you need to use these parameters. More info

Attribute | Example | Description
--- | --- | ---
searchwidget-rooturl | `data-searchwidget-rooturl="https://website.com/search-results.html"` | Url, where the iframe widget is implemented
partner-id | `data-partner-id="website"` | The id of partner (provided by us)

There are other optional parameters. You can prefill location or date. For more info contact us.

## Live examples

Js Search Widget is live on [carhiremarket.com](https://www.carhiremarket.com/spain/airport/palma-de-majorca-airport_pmi.aspx), [viajeselcorteingles.es](https://www.viajeselcorteingles.es/)

## Caching

The widget loader "cnx-widget.js" has a long cache time (1 year), so you will not see the changes immediately.

## Issues

As JS Widgets are not sandboxed in a frame they are susceptible to being broken by the parent site, specifically with regards to styling, mostly this will just be because of global !important styling enforced by the parent site.
