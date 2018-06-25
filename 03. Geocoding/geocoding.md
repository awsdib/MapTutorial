## Geocoding and place search

1. Go to the geocoding example page: [https://developer.here.com/api-explorer/maps-js/v3.0/servicesRouting/geocode-a-location-from-address](https://developer.here.com/api-explorer/maps-js/v3.0/servicesRouting/geocode-a-location-from-address)

2. How to build the example on your local machine
    * Create an empty html page
        - Open your favorite text editor (Notepad is fine)
        - Select file -> save as
        - Enter a file name with *(.html)* as extention
        - Open the html file with your text editor
    * Copy the code example for geocoding
        - From the examples page and the Code section copy the complete code from *(JS+html)* tab to your new page
        - Replace the two app keys with your own
        - Double click the html file to run it in the browser

3. Understanding the code:
    1. **HTML** part:
	    - For calling the geoding function and for showing output results, a new html element ``` <div id="panel">...</div>``` is defined

    2. **Script** part:
        - In addition to the **Boilerplate (the basic map loading steps)**, few new functions are introduced
        - **geocode** function:
            This function performs the call to the geocoding service using the *platform* object.
            Inside, the service object is created, in addition to some parameters which contain the text that will be searched
            In the end, using the geocoding object, a request to the service is executed with passing the search parameters
            ```javascript
                function geocode(platform) {
                    var geocoder = platform.getGeocodingService(),
                        geocodingParameters = {
                        searchText: '200 S Mathilda Sunnyvale CA',
                        jsonattributes : 1
                        };

                    geocoder.geocode(
                        geocodingParameters,
                        onSuccess,
                        onError
                    );
                }
            ```

        - **onSuccess** function: Shows the result of geocoding on map as well as on the panel
        ```javascript 
            function onSuccess(result) {
                var locations = result.response.view[0].result;
                addLocationsToMap(locations);
                addLocationsToPanel(locations);
            }
        ```
        
        - **openBubble** function: is used when clicking on the markers to show the place information as a little tooltip box above the marker.

        - **addLocationsToPanel** function: is used to add the result of geocoding to the control panel
        
        - **addLocationsToMap** function: is used to add the result of geocoding as markers to the map

        - Finally, a call to the geodocing function that's defined in the beginning
        ```javascript
            geocode(platform);
        ```

5. Output
    - The example shows a static geocoding of the text '200 S Mathilda Sunnyvale CA'
    - A marker that represent the resulting geocoded place on the map, and on the panel more information about the place
    - When clicking on the marker, a bubble contains the label of the place is shown
    - Static geocoding: When running the html page, it always shows the same geocoded place. That's because the search text is coded staticly in the script. To change the logic and making the user search for any place, see next example.

