# Combination of Search and Iframe Widget

This option is the most flexible way to implement our widgets. In this solution we don't make any changes on homepage, header or footer. The client implements on homepage only our Search Widget and on second page our Iframe Widget. 


## Example of implementation

[Search Widget - more info](js_search.md)

Implement this piece of code on your homepage. Styling on line 10 is up to you.

```html
<!-- START of CARNECT WIDGET -->
<div
  data-cnx-container
  data-locale="en-gb"
  data-searchwidget-rooturl="https://your_website.com/test-search.html"
  data-currency="EUR"
  data-partner-id="your_website">
 
  <!-- This is the main search box wrapper, styling is on you -->
  <div style="width: 420px; overflow: hidden; display: inline-block; padding:20px; background:#fff; border:1px solid #000;">
    <div data-component="search-form"></div>
  </div>
</div>
<script type="text/javascript" src="https://our_whitelabel.com/assets/js/cnx-widget.js"></script>
<!-- END of CARNECT WIDGET -->
```

[Iframe Widget - more info](iframe.md)

Implement this code on second page - where you would like to show results of the search. 

```html
<!-- Start CARNECT IFRAME WIDGET-->
<div id="cnx-widget-wrapper" data-cnx-widget="full" data-target-page="search" data-params=""></div>
<script type="text/javascript" src="https://our_whitelabel.com/assets/js/cnx-widget.js"></script>
<!-- End CARNECT IFRAME WIDGET-->
```


