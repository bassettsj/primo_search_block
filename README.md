primo_search_block
==================

Provides a search block following the recommened implementation by ExLibris in Drupal 7.


## Exlibris's instructions 

### Adding the Search Form to your website

This section will describe the supported parameters to use in the dlSearch request. Adding the JavaScript and HTML code to your website. The following HTML code should be wrapped in a valid HTML file on your website:

At the `<head>` section of your HTML please add the following JavaScript lines:
```html
<script type="text/javascript"> 
 function enterKey(evt) {
  var evt = (evt) ? evt : event
  var charCode = (evt.which) ? evt.which : evt.keyCode
  if (charCode == 13) {
    searchPrimo()
  }
 } 
 function searchPrimo() {
  document.getElementById("primoQuery").value = "any,contains," + 
    document.getElementById("primoQueryTemp").value;
  document.forms["searchForm"].submit();
 }
 function searchPrimoEvent(event) {
  if (event && event.which == 13) {
    document.getElementById("primoQuery").value = "any,contains," + 
      document.getElementById("primoQueryTemp").value;
    document.forms["searchForm"].submit();
  }
  else
    return true;
 }
 </script>
```
  
In the desired location on the webpage please add the following form:

```html
  <form name="searchForm" role="search" method="get" 
   action="http://<PRIMO_URL:PORT>/primo_library/libweb/action/dlSearch.do" enctype="application/x-www-form-urlencoded; charset=utf-8" id="simple" target="_self"  onsubmit="searchPrimo()">
   <input name="institution" value="<INSTITUTION_CODE>" type="hidden">
   <input name="vid" value="<VIEW_CODE>" type="hidden">
    <input name="search_scope" value="<SEARCH_SCOPE>" type="hidden">
   <input name="group" value="GUEST" type="hidden">
   <input name="onCampus" value="true" type="hidden">
   <input name="displayMode" value="full" type="hidden">
   <input type="hidden" id="primoQuery" name="query" />
   <input type="text" size="25" id="primoQueryTemp" value="" name="queryTemp" onkeypress="return searchPrimoEvent(event)" />
   <input id="go" type="button" value="Search" title="Search" style="background:#fff2c6; color: #8a8372; border:3px solid; margin-top: 5px; margin-left: 125px;" onclick="searchPrimo()" alt="Search">
  </form>
```
The following attributes should be modified to fit your Primo configuration:

* `<PRIMO_URL:PORT>`- This needs to be your Primo Front End, or Load Balancer address if you have an MFE environment. Example: primo-demo.exlibrisgroup.com:1701
* `<INSTITUTION_CODE>` - This needs to be your Primo Institution Code. Example: NORTH
* `<VIEW_CODE>` - This field specifies the View Code which the dlSearch will search at. Example: NORTH_VU01
* `<SEARCH_SCOPE>` - This field specifies the search scope within the View Wizard. Example: Primo_Central


### Customizing your added search box
\
