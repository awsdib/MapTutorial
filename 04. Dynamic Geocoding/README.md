## Interactive Geocoding

* In the last geocoding example, we introduced the geocoding API and developed an example that always shows the same geocoded place. 

* In the following example, the input is taken dynamically from the user and then geocoded

* What's needed to be added to the previous example:
    1. Create the user interface
    2. Link the interface with the geocoding function
    3. Improve the usability

1. Creating the user interface: All what's needed to dynamic geocoding of user input is to have an input field and a search button
    1. Open the html page from the previous example in your text editor
    2. Make sure that you replaced your App key and App code
    3. In the **HTML** section, find the panel element
    4. The new interface should be added inside the panel element
        The old html structure:
        ```html
            <div id="panel" style="position:absolute; width:49%; left:51%; height:100%; background:inherit" >   </div>
        ```
    5. Add the input field and the search button:
        * First, add an input field with 2 attributes: **type="text"** and **id="query"**.
            The id attribute will be used later to get the content of the field.
        * Second, add a button with a "Search" text, and specify the click function by setting the function name for the **onClick** attribute.
        ```html
            <div id="panel" style="position:absolute; width:49%; left:51%; height:100%; background:inherit" >
                <input type="text" id="query">
                <button onclick="search()">Search</button>
            </div>
        ```

2. Link the button click with the geocoding function
    1. Anywhere in the code, create a function with the name chosen for the button's onClick attribute, in this case: **search()**. That function will be called every time the user clicks on the button
        ```javascript
            function search() {

            }
        ```
    2. Find the default call of the geocode function **geocode(platform);** at the end of the code and move it to the **search()** function
        ```javascript
            function search() {
                geocode(platform);
            }
        ```
    3. Making the geocode function search for the text entered in the input field:
        * When calling the geocode API function, the parameter **searchText** is used to pass the query. By default the fuction always search for the text string '200 S Mathilda Sunnyvale CA'
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
        * Now to get the value entered in the input field (with the specified id="query"), use this command ```document.getElementById('query').value;``` and with that, replace the static text.
        * To do that neatly, create a new variable named **query** in the beginning of the fuction, and give it the value of the input field. Afterwards, replace the static text with the new variable.
        ```javascript
            function geocode(platform) {
                var query = document.getElementById('query').value;

                var geocoder = platform.getGeocodingService(),
                    geocodingParameters = {
                    searchText: query,
                    jsonattributes : 1
                    };

                geocoder.search(
                    geocodingParameters,
                    onSuccess,
                    onError
                );
            }
        ```

3. Make better usability
    * In the current state, every time the user searches for a new place, the new results in the panel are shown in addition to the old ones. Also, the old markers from the previous search are still showing on the map.
    * To show only new results in the panel, on each call of the **search()** function, the result list should be cleared before showing the new ones.
        ```javascript
            function search() {
                var oldResult = document.getElementsByTagName('ul');
                if(oldResult.length>0) oldResult[0].remove();

                geocode(platform);
            }
        ```
    * To show only new markers on the map, the markers set from before need to be removed. There are 2 steps for doing that:
        1. In the function ```addLocationsToMap()```, move the definition of the marker group to the outside of the function (to the global scope), so the same object which contains the markers can be used later.
        ```javascript
            var group = new  H.map.Group(),
                position,
                i;

            function addLocationsToMap(locations){

                // Add a marker for each location found
                for (i = 0;  i < locations.length; i += 1) {...}
                ...
            }
        ```
        2. Now the **group** object can be used to clear all the marker from it using ```group.removeAll();```
        ```javascript
            var group = new  H.map.Group(),
                position,
                i;

            function addLocationsToMap(locations){

                group.removeAll();

                // Add a marker for each location found
                for (i = 0;  i < locations.length; i += 1) {...}
                ...
            }
        ```

* Output
    - The example now shows the result of geocoding input text from the user
    - Every time the user searches for a new place, the previous results and markers are gone and replaced by the new ones.

