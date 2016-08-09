# Useful DHIS2 API requests

This is a list of common API requests. API requests can be executed in a web browser by accessing a URL. The format of the URL is always the same:

`<server_url>/api/<request>`

The field `server_url` depends on the requested server. For example, it could be `http://localhost:8989/dhis` to access a local instance, or `https://hmisocba.msf.es` to access the HMISOCBA production server.

The following sections deal only with the `request` field of the URL.

### Exporting data to MS Excel Table
Sometimes is useful to open the information in an excel table to sort, filter, reorder the colomns or just save the information. The steps to do that are the following:

1. Do the request. The information you want to save should be displayed in the web browser.
2. Right-click on the screen and click on "Save as...". Then save the ".xml" somewhere in your computer.
3. Open the ".xml" file with MS Excel. A dialog will be prompted, then choose "XML table". A new dialog will appear, just accept it.
4. Now, you should be able to see a MS Excel table with the information.

## Data Elements
### List of dataelements with some information (Tally Sheet)
List all dataelements

`/dataElements?paging=false&fields=id,code,displayName,displayFormName,displayDescription,categoryCombo[name],dataElementGroups[name],dataSets[name,code]`

## Indicators
### List indicators with all fields
List all the indicators in the system with description, numerator, denominator and factor (unit, per houndred, per thousand, etc).

`/indicators?paging=false&fields=id,code,displayName,displayDescription,numeratorDescription,denominatorDescription,indicatorType[name],indicatorGroups[name]`

## Datasets
### List all the datasets associated to a health site and to its services (eg. health site uid: EtI7MO3ou8C):
`/organisationUnits/EtI7MO3ou8C?fields=children[name,dataSets[name]],dataSets[name]`

## Filters
You can use any field to filter a request. To apply a filter you only have to append it to the URL.

For example, to look for an indicator with code HIV010 you have to append the following to the url:

`&filter=code:eq:HIV010`

the whole request could be for example:

`/indicators?paging=false&fields=id,code,name,description&filter=code:eq:HIV010`

If you want to filter by a field, but you don't know exactly the value of the field and you want to do a search, you can use the LIKE operator and include a key word. For example, to look for all the indicator that contains the word Malaria in their name, you can use the filter:

`filter=name:like:malaria`

## Languages
By default, the API gives the information in language of your user. To choose a different language you only have to append the following syntax to the url:

`&locale=en`

The field `locale` can have the values `en`, `fr`, `es` or `pt`.

NB: Does not seem to work with 'sub-requests' in 2.21 (it does work in 2.24 though).
