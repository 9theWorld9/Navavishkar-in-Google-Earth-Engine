# Navavishkar-in-Google-Earth-Engine
**Quantification Of Above Ground Biomass In Auroville Green Belt Using Google Earth Engine**

1 Loading and combining all raster variables
In this step, we loaded various raster variables including Sentinel-2 (S2) data, SRTM elevation data, and slope data. 
For the Sentinel-2 data, we loaded the surface reflectance image collection (S2_SR). To mask out clouds in the S2 images, a cloud masking function called "maskS2clouds" was created. This function utilized the QA band of Sentinel-2, which contains cloud mask information. The S2 image collection was filtered based on date, cloud cover percentage, and cloud mask, and only specific bands (B3, B4, B5, B6, B7, B8, B11) were selected for further analysis.
Next, we imported the SRTM DEM and clipped it to the study area boundary. The elevation data was reprojected to the WGS 84 UTM zone 44N coordinate reference system. Similarly, the slope was derived from the SRTM DEM and reprojected accordingly.
In the final step, all the raster variables were combined into a single image by merging the bands of the Sentinel-2 composite, elevation, and slope. The resulting image was clipped to the study area boundary.
Finally, an object called "bands" was created to specify the bands to be included in the classification model. This object contained the names of all the relevant raster variables.
Throughout this step, the loading, filtering, processing, and merging of raster variables were performed to prepare the data for the subsequent modeling steps.

2 Preparing training data
In this step, we prepared the training data using various datasets including GEDI L4B, Sentinel-2, SRTM elevation, and slope data. We started by loading the GEDI L4B dataset, which provides estimates of mean aboveground biomass (AGB) density at a resolution of 1 km x 1 km. The dataset was clipped to the study area boundary.
The next step involved reprojecting the GEDI L4B dataset to the WGS 84 UTM zone 44N coordinates reference system. The projection information of the dataset was checked to ensure consistency.
To visualize the mean AGB density map, a color palette was created, and the dataset was added as a layer to the map.
Subsequently, we sampled 2,000 AGB density points from the GEDI L4B dataset within the study area boundary. The sampling process considered the specified region, scale, and number of pixels. The resulting points were printed and displayed, and a layer representing the points was added to the map.
Next, the training data was split into a training set and a validation (or test) set. The points were assigned a random column using the randomColumn() method, with a seed value provided for repeatability. The training data set was then filtered based on the specified split percentage (70%) to obtain the training set, while the validation data set contained the remaining points.
Finally, the training and validation data sets were printed to the console for verification.
Throughout this step, the GEDI L4B dataset was utilized to extract AGB density points, which were subsequently divided into training and validation sets. These sets would serve as the basis for training and evaluating the biomass prediction model in the following steps.

