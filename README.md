HW6 - Darksky Shiny App
-----
Due Tuesday 11/05 by 11:59 pm

Dark Sky is an iOS app and website that provides "hyperlocal" weather forecasts. They make their data available to third parties via a web API which we will be using to create a simple shiny app. 

In order to access this API you need an account - if you go to https://darksky.net/dev/ you can sign up to gain access to their API. Once you have registered you will have access to a usage console that includes a unique secret key (the long alphanumeric string at the top of the page) you will use this to access the API. You can make up to 1000 API requests per day without incurring any cost, so there is no need to enter any billing information.

Documentation for the Dark Sky API can be found [here](https://darksky.net/dev/docs) and includes all information about how to create a properly formated API request and the details of the JSON format of the returned data.

<br/>

#### Task 1 - Getting data from Dark Sky

Your first task is to write a single function that accepts an API key, latitude, longitude, and optionally a date and returns a data frame containing the hourly forecast for the given location (and time). The Dark Sky forecast API provides a number of different weather related predictions - all of these quantities should be returned by your function along with a properly formated `datetime` column. You do not need to return any of the currently, minutely, daily or other data - only hourly data is required. Note that you can exclude some of these results via your API request.

Some additional requirements:

* If no date is provided the results should be the hourly forecast for the next two days, this is the default behavior of a [Forecast Request](https://darksky.net/dev/docs/forecast).

* If a date you should assume the user is requesting data centered at midnight for that particular date in that particular timezone. You should return the hourly forecast data for the two days *prior* as well as that date and the following day (96 hours total) - this can be achieved via multiple requests to the [Time Machine Request](https://darksky.net/dev/docs/time-machine) endpoint. 

* All date/time results should be reported in the local timezone for the request - this information is included in the API return results.

<br/>

#### Task 2 - Prediction Locations

Your second task is to scrap US city location information from the following Wikipedia page: https://en.wikipedia.org/wiki/List_of_United_States_cities_by_population. The entire table should be read into R via web scraping (think `rvest`).

Your final data frame should meet the following requirements

* Rows should be filtered to only contains cities with more than 500,000 residents during the 2010 Census

* City and state names should be cleaned up and appropriately formated (remove any footnote references, etc.)

* Location should be split up into new numeric latitude and longitude columns. Note that western longitudes and southern latitudes should be negative.

* Your table must contain the following columns: `City`, `State`, `estimate_2017`, `census_2010`, `change`, `land_area_2016`, `pop_density_2016`, `latitude`, and `longitude`.

* All columns but city and state should be numeric

* For the land area and population density columns choose to use either metric or imperial units (don't report both)

<br/>
 
#### Task 3 - Shiny Predictions

Your third task is to create a shiny app that provides a GUI interface for the `get_darksky` function you wrote earlier. This app should allow the user to select a city from a list and provide a visualization of the hourly weather forecast for that location. 

Your app should have the following features:

* Your visualization should always include the temperature, but also allow the user to select a second quantity (e.g. precipitation chance, barometric pressure, etc.) to optionally display on the *same* plot object (small multiples / faceting are acceptable) - this must also include appropriate axes and legend.

* The list of cities should come from the data frame your created in Task 2.

* When a city is selected its latitude and longitude should also be reported in the user interface. 

* UI should also allow the user to specify a historical date for the forecast or no date which should then use the current date and time

* Extra credit for adding bells and whistles and overall polish / design of your app.
