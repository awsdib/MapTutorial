## Traffic: Always show traffic layers (roads and incidents)

### How to build the example on your local machine

1. Visit the traffic examples page for javascript: [https://developer.here.com/api-explorer/maps-js/v3.0/maps/showing-traffic-information](https://developer.here.com/api-explorer/maps-js/v3.0/maps/showing-traffic-information)

2. Go to the code section 

3. From the Javascript tab, copy the function definition for showing traffic layer:
    ```javascript 
        function enableTrafficInfo (map) {...}
    ```

4. Open the html page from the past example in your text editor
    
5. Paste the copied function definition in the end of the script in the bottom of the page

6. Finally, for the function to take effect, call the function after it's definition by writing:
    ```javascript 
        enableTrafficInfo(map);
    ``` 

7. You need to replace the credentials with your own if you got the example from the tutorial files

8. The complete new code that is supposed to be added to the previous example:
    ```javascript 
        function enableTrafficInfo (map) {
            // Center map on New York
            map.setCenter({lat: 40.74007175329128, lng: -73.8701876028157});
            map.setZoom(11);

            // Show traffic tiles
            map.setBaseLayer(defaultLayers.normal.traffic);

            // Enable traffic incidents layer
            map.addLayer(defaultLayers.incidents);
        }

        enableTrafficInfo(map);
    ``` 

9. To keep the map centered on the same point from the previous example, you can delete or comment the centering code in the new function.

    To comment the centering code, add two forward slashes // on the setCenter function call:
    ```javascript 
    
        function enableTrafficInfo (map) {
            // Center map on New York
            //map.setCenter({lat: 40.74007175329128, lng: -73.8701876028157});
            //map.setZoom(11);
            ...
        }
    ```     

10. Output
    - The example shows the same previous interactive map
    - Now, the traffic layer is always shown by default
    - The traffic information contain the traffic flow *(Traffic conditions)* as well as the *(Traffic incidents)*

