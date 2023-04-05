# BikepathsWuerzburg
Bikepaths in and around Wuerzburg.

Map of Bikepaths in and around Wuerzburg
The goal of this analysis is finding biking routes around Wuerzburg which are also accessible by train. To improve the experience during tours a layer of Beergardens and Nature Areas is included. 
The first step of creating a thematic map with bikepaths around an area is to get all the necessary data. 

Overview other the Steps of the Workflow:
![FlowchartBikepaths](https://user-images.githubusercontent.com/116875684/230120355-2816ad37-c80a-4d56-bb3c-866958b741b2.PNG)

The following data is used to create a map of the region around Wuerzburg:

- SRTM:	Raster	(https://dwtkns.com/srtm/)

- Administrative border of Wuerzburg:	Shape (Polygons)	(https://gdz.bkg.bund.de/index.php/default/open-data.html)

- Bikepaths:	Shape (Lines)	(https://opendata-esri-de.opendata.arcgis.com/datasets/esri-de-content::radrouten-osm/explore?location=51.046961%2C10.444122%2C7.69)

- DB Railways:	Shape (Lines)	(https://data.deutschebahn.com/dataset.groups.datasets.html)

- DB Train Stations:	Shape (Points)	(https://data.deutschebahn.com/dataset.groups.datasets.html)

- Beergardens:	Shape (Points)	(http://overpass-turbo.eu/)

- Corine Landcover:	Shape (Polygons)	(https://land.copernicus.eu/pan-european/corine-land-cover)

- Water Bodies:	Shape (Polygons)	(https://opendata-esri-de.opendata.arcgis.com/datasets/esri-de-content::dlm250-gew%C3%A4sserfl%C3%A4chen/explore?location=51.127186%2C10.469409%2C7.66)


To get the desired area, the City Boundaries of Wuerzburg are buffered using the Buffer tool. Then all the shape files are clipped to the buffer’s extent. To get the natural areas from the Corina Landcover dataset the natural grassland, vineyards and forests are extracted.
Combining all the layers results in a slightly chaotic map which is inconvenient to get an overview over where to bike. Therefore, I create an overview map designed as a Hexagon grid. To create this grid use Vector -> Research Tools -> Create grid. If you only want to summarize point layers to different designs of grid the Bestagon Plug-In (https://github.com/KonstiDE/Bestagon.git) might come in handy. For the Lines use the Sum Line Lengths. For Polygons use the Overlap Analysis. Both belong to the Vector Analysis Toolbox. Data used here are Bikepaths, Train Stations, Beergadens and Natural Areas.
Since the values are not in the same range, I reclassified them via the Attribute Tables with classes from 0 to 4. With 0 being the lowest, mostly 0 counts, and 4 the highest value. After summarizing all hexagon layer they were reclassified to fit the 5 classes. The highest score achieved for one hexagon is 14 out of 16.   
The resulting hexagon map makes it easy to see at first glance where the best areas for biking are also including personal priorities. Together with the overview map it is possible to decide on an area to go and take the first steps in planning. 
![Bikepaths](https://user-images.githubusercontent.com/116875684/230118646-212391de-640f-4204-b26b-6b131c1a287d.png)

![BikepathHex](https://user-images.githubusercontent.com/116875684/230118095-4956e1ab-97d7-4433-8741-1b56db859e34.png)
Further helpful tools when planning the ride are Road Slope and Terrain Profile. The first one includes a DEM to compute the slope of segments on a bike path. By classifying the slope you can find the steepest parts of your route and quantify them. The second tool, Terrain Profile, calculates an Hight Profile along a line, which will show you the ascends and descends of your selected route. One problem when using the Terrain Profile Tool is that the segments of the route are in the wrong order or they face the wrong way. The solve the first issue use the Plug-In MMQGIS -> Modify -> Sort to change the order of the lines. For the second problem activate the Advanced Digitizing Toolbar and use Reverse Line. 
![ExampleRouteCro](https://user-images.githubusercontent.com/116875684/230119534-d539a6ec-f9c8-410f-b355-a82755bbb621.png)


Plug-Ins used in this workflow: 
-	Bestagon (https://github.com/KonstiDE/Bestagon.git)
-	MMQGIS
-	Profile Tool
-	Road Slope Calculator

