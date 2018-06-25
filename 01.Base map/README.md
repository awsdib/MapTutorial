## Base map, traffic layer and public transport

1. Visit the examples page for javascript on DevPortal: [https://developer.here.com/api-explorer/maps-js/v3.0](https://developer.here.com/api-explorer/maps-js/v3.0)

2. Page structure:
    - Introduction to the example with all relevant infoprmation
    - The output of the example is shown
    - The Code section includes 2 tabs
        1. "Javascript" tab for adding the example to an existing project
        2. "JS+html" tab is the complete example with javascript and html

3. Understanding the code: HTML page with embedded javascript
    1. **HTML** part:
	    - in the <head> tag are all the required libraries and stylesheets
	    - in the <body> tag there is the html element which will hold the map 
            `<div id="map"></div>`, and the `<script>` section

    2. **Script** part:
	    1. *Boilerplate* is the code that is required in every HERE maps application to initialize the map.
	    It consists of 3 simple steps:

            1. Defining the platform object, and set the credentials 
                ```javascript
                var platform = new H.service.Platform({
                    app_id: 'Paste Your App Id Here',
                    app_code: 'And Your App Code Here',
                    useCIT: true,
                    useHTTPS: true
                });

                var pixelRatio = window.devicePixelRatio || 1;
                var defaultLayers = platform.createDefaultLayers({
                    tileSize: pixelRatio === 1 ? 256 : 512,
                    ppi: pixelRatio === 1 ? undefined : 320
                });
                ```

            2. Create the map js object and pass as a parameter the map html element defined before
                ```javascript
                var map = new H.Map(document.getElementById('map'),
                defaultLayers.normal.map, {pixelRatio: pixelRatio});
                ```

            3. adding control buttons to the map to make it interactive
                ```javascript
                var behavior = new H.mapevents.Behavior(new H.mapevents.MapEvents(map));
                // Create the default UI components
                var ui = H.ui.UI.createDefault(map, defaultLayers);

        2. The specific example code which is a function call to center the map on a specific location
            
            Function definition:
            ```javascript
            function moveMapToBerlin(map){
                map.setCenter({lat:52.5159, lng:13.3777});
                map.setZoom(14);
            }
            ```

            Function call
            ```javascript
            moveMapToBerlin(map);
            ```

        **Note:** the Function call must be written after initializing the map with the boilerplate code and after the function definition

4. How to build the example on your local machine
    * Create an empty html page
        - Open your favorite text editor (Notepad is fine)
        - Select file -> save as
        - Enter a file name with *(.html)* as extention
        - Open the html file with your text editor
        - From the examples page and the Code section copy the code snippet from *(JS+html)* tab to your newly created html page
        - Replace the two app keys with your own
        - Double click the html file to run it in the browser

5. Output
    - The example shows an interactive map which includes zooming buttons and scroll/pan features
    - In the bottom right corner, the rounded button with the layers icon is used to switch between different map views: Map, Satellite or Terrain
    - Additionally, the traffic layer and the public trasport layer are shown in the view list
    - The traffic information contain the traffic flow *(Traffic conditions)* as well as the single traffic events reffered to as *(Traffic incidents)* such as construction work or road closures.

