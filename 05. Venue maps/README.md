## Working with indoor venue maps

* In this example, we Introduce HERE Venue Maps API and learn how to add the indoor layer to our applications. The example utilizes the venues service to show the indoor map of some places such as malls, restaurants, parkings etc..., and provides the user with control to show different floor levels.

* What's needed for the example to work locally:
    1. Adding the venues layer to the map
    2. Show the user interface that controls floor levels

1. Go to the venues API example page: [https://developer.here.com/api-explorer/maps-js/v3.0/maps/venues-layer](https://developer.here.com/api-explorer/maps-js/v3.0/maps/venues-layer)

2. Open the html page from the past example in your text editor

2. From the code section, JS+HTML tab, copy the definition of the following functions, and add them to your application
    * ```   function addVenueLayer(map, platform, renderControls)    ```
    * ```   function onSpaceCreated(space)    ```
    * ```   function renderControls(title, buttons)    ```
    * Finally, copy the call for adding the venue layer ``` addVenueLayer(map, platform, renderControls); ``` located in the end of the example

3. Understanding the code
    1. Adding the venues layer 
        * ``` (addVenueLayer)```: Using the **platform** object we can get the venues service that has the function **createTileLayer** which is responsible for getting the actual venue tiles.
        * ```javascript
            var customVenueLayer = platform.getVenueService().createTileLayer({
                // Provide a callback that will be called for each newly created space
                onSpaceCreated: onSpaceCreated
            });
          ```
        * ``` (onSpaceCreated)```: This function is called when the tiles are retrieved, and it recognizes single objects inside the venue layer such as single shops, and that makes it possible to style some objects differently. The function changes the style of the 'H&M' shop and shows it in light green.
        * ```javascript
            function onSpaceCreated(space) {
                // getData for spaces contains data from the Venue Interaction Tile API,
                // see https://developer.here.com/rest-apis/documentation/venue-maps/topics/resource-type-venue-interaction-tile.html
                if (space.getData().preview === 'H&M') {
                    space.setStyle({
                    fillColor: 'rgba(0,255,0,0.3)'
                    });
                }
            }
          ```

    2. Adding the User interface ```(renderControls)```: What the function does, is creating an html element **containerNode** which cosists of a title and 2 buttons for floor level control
    ```javascript
        function renderControls(title, buttons) {
            var containerNode = document.createElement('div');

            containerNode.innerHTML = '<h4 class="title">' + title + '</h4><div class="btn-group"></div>';
            containerNode.setAttribute('style',
                'position:absolute;top:0;left:0;background-color:#fff; padding:10px;text-align:center');

            Object.keys(buttons).forEach(function (label) {
                var input = document.createElement('input');
                input.value = label;
                input.type = 'button';
                input.onclick = buttons[label];
                input.className="btn btn-sm btn-default"
                containerNode.lastChild.appendChild(input);
            });

            map.getElement().appendChild(containerNode);
        }
    ```

4. Output:
    * At this point, the application implements both geocoding and venues services
    * To see that in action, type in the search field the text "Berlin Alexanderplatz"
    * Locate the *"Alexa Shopping Center"* on the map near Alexander street
    * Zoom in until the indoor map is shown
    * Try the control buttons and change the floor level
    * Check out how the 'H&M' is styled differently
