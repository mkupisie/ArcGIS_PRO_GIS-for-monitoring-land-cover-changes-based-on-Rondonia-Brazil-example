## GIS for monitoring land cover changes based on Rondonia Brazil example [ArcGIS Pro]
In an era marked by rapid urbanization, environmental change and dynamic land use patterns, the ability to monitor and understand land cover changes is of paramount importance. Geographic information systems (GIS) are proving to be a powerful tool in this venture, providing a sophisticated framework for capturing, analyzing and visualizing spatial data. For the purpose of analyzing land cover change, Global Land Cover Layers can be used. These layers, created through advanced satellite imagery and classification techniques, provide a dynamic portrayal of land use, vegetation, and human impact on a global scale. As our world navigates challenges of sustainable development, global land cover layers play a pivotal role in fostering informed decision-making and promoting a balanced coexistence between human activities and the environment. 

As an example of detecting land cover change using GIS, let’s focus on one of the states in southern Brazil called Rondônia, that is a part of the Amazonian “Arc of Deforestation”, characterized by the rapid loss of tropical forest along the southern edge of the Amazon. Deforestation in Rondônia started in the 1970s and 1980s with road expansion, attracting loggers and miners. Government initiatives to combat poverty encouraged migration and colonization. In recent times, large-scale agriculture, especially cattle ranching and soy farming, has become a major driver of deforestation in the southern Amazon.

### Data
Global Land Cover Layers were retrieved from ArcGIS Living Atlas provided by Esri, which holds a collection of ready-to-use global geographic content, such as imagery, basemaps, boundaries, demographics, earth observations, urban systems and historical maps. The used layer called “Global Land Cover 1992-2020” is a time-series map of the surface of Earth created by ESA Climate Change Initiative ([See more]([https://pages.github.com/](https://www.arcgis.com/home/item.html?id=1453082255024699af55c960bc3dc1fe)https://www.arcgis.com/home/item.html?id=1453082255024699af55c960bc3dc1fe).

### Tools and methods
**1. Extracting land cover data for Rondonia region**. The Global Land Cover 1992-2020 layer was cut to the borders of the Rondonia state using the Extract by Mask tool. 

**2. Reclassifying raster data**. The Global Land Cover 1992-2020 layer is classified into 36 land cover types, however for the purpose of detecting changes mostly focused on forests, raster was classified into new 11 classes using Reclassify Raster tool. 

**3. Retrieving data for 1992 and 2020.**. The main layer was copied in order to create two Global Land Cover 1992-2020 layers and use the Definition Query for both to select layers with data only for the year 1992 and 2020 using StartDate and EndDate parameters. 

**1992:**
*“When StartDate is on or after 01.01.1992 and EndDate is on or before 31.12.1992”*

**2020:** 
*“When StartDate is on or after 01.01.2020 and EndDate is on or before 31.12.2020”*

**4. Adjusting coordinate system**. For the purpose of the area calculation in the given state the coordinate system was converted to South America Albers Equal Area Conic. 

**5. Calculating the area and difference**. In order to calculate the area of each land cover type, new column was added to attribute table and the Calculate Field tool was used with the following formula:

(!Count! * 96100)*0.000001

Each cell size is 310 x 310 meters, so the area of each cell is 96100 m2. In the given formula, the amount of cells for each land cover type was counted, multiplied by the size of each cell in m2 and then multiplied by 0.000001 to convert the results to km2. New column was added to calculate the difference between the years 2020 and 1992. 

**6. Calculating Categorical Difference**. ArcGIS Pro enables the calculation of categorical difference using the Compute Change tool. The results allow to see detailed information about area changes between each class. 


![Rondonia_deforestation_classify](https://github.com/mkupisie/ArcGIS_PRO_GIS-for-monitoring-land-cover-changes-based-on-Rondonia-Brazil-example/assets/130785524/d4a61341-3461-4894-8da0-98bf8dac1231)

<p align="center">
![table_area](https://github.com/mkupisie/ArcGIS_PRO_GIS-for-monitoring-land-cover-changes-based-on-Rondonia-Brazil-example/assets/130785524/6d2b7b29-3002-414a-a2d9-d0a86847f600)
</p>

**Categorical difference**
![categorical_diff](https://github.com/mkupisie/ArcGIS_PRO_GIS-for-monitoring-land-cover-changes-based-on-Rondonia-Brazil-example/assets/130785524/927a7e86-e5fc-4ab9-b787-bdfbe20484ff)


