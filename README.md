# **Navavishkar-in-Google-Earth-Engine**
## **Quantification Of Above Ground Biomass In Auroville Green Belt Using Google Earth Engine**

### **1 Loading and combining all raster variables**
In this step, we loaded various raster variables including Sentinel-2 (S2) data, SRTM elevation data, and slope data.
For the Sentinel-2 data, we loaded the surface reflectance image collection (S2_SR). To mask out clouds in the S2 images, a cloud masking function called "maskS2clouds" was created. This function utilized the QA band of Sentinel-2, which contains cloud mask information. The S2 image collection was filtered based on date, cloud cover percentage, and cloud mask, and only specific bands (B3, B4, B5, B6, B7, B8, B11) were selected for further analysis.
Next, we imported the SRTM DEM and clipped it to the study area boundary. The elevation data was reprojected to the WGS 84 UTM zone 44N coordinate reference system. Similarly, the slope was derived from the SRTM DEM and reprojected accordingly.
In the final step, all the raster variables were combined into a single image by merging the bands of the Sentinel-2 composite, elevation, and slope. The resulting image was clipped to the study area boundary.
Finally, an object called "bands" was created to specify the bands to be included in the classification model. This object contained the names of all the relevant raster variables.

### **2 Preparing training data**
In this step, we prepared the training data using various datasets including GEDI L4B, Sentinel-2, SRTM elevation, and slope data. We started by loading the GEDI L4B dataset, which provides estimates of mean aboveground biomass (AGB) density at a resolution of 1 km x 1 km. The dataset was clipped to the study area boundary.
The next step involved reprojecting the GEDI L4B dataset to the WGS 84 UTM zone 44N coordinates reference system. The projection information of the dataset was checked to ensure consistency.
To visualize the mean AGB density map, a color palette was created, and the dataset was added as a layer to the map.
Subsequently, we sampled 2,000 AGB density points from the GEDI L4B dataset within the study area boundary. The sampling process considered the specified region, scale, and number of pixels. The resulting points were printed and displayed, and a layer representing the points was added to the map.
Next, the training data was split into a training set and a validation (or test) set. The points were assigned a random column using the randomColumn() method, with a seed value provided for repeatability. The training data set was then filtered based on the specified split percentage (70%) to obtain the training set, while the validation data set contained the remaining points.
Finally, the training and validation data sets were printed to the console for verification.

### **3 Training the random forest model**
In this step, we trained and evaluated a random forest (RF) model for biomass prediction. The RF model was configured with a parameter specifying the number of trees, set to 50 in this case.
To perform the training, we collected the training data by selecting the relevant bands from the merged collection and sampling the regions using the training data set. The scale of the training data was adjusted to avoid memory-related issues.
The RF model was trained using the smileRandomForest classifier with the output mode set to regression. The training data and properties such as the target class ("MU") and input bands were provided as inputs to the training process.
Following the training, the classification was performed using the trained RF model on the merged collection, and the resulting regression output was clipped to the study area boundary.
To display the regression output, a continuous palette was loaded from the "ee-palettes" package. A color palette from the chosen palette collection (in this case, colorbrewer.YlGn) was selected.
The regression classification was added as a layer to the map, using the defined palette. To determine the appropriate visualization parameters, the minimum and maximum predicted values within the study area were computed using the reduceRegion() method. These values were used to create a visualization dictionary.
A legend was created to provide information about the AGB density (in Mg/ha) represented by the color gradient. The legend panel included a title, a color gradient image, and text indicating the minimum and maximum values.

<img src="https://github.com/failed-wizard/Navavishkar-in-Google-Earth-Engine/blob/main/google_img.png" alt="AGB density map for Auroville Greenbelt." class="center" width="50%" height="50%"/>

### **4 Estimating the trained model performance**
In this step, we evaluated the performance and accuracy of the random forest (RF) model. We first used the .explain() method on the trained RF model to compute variable importance and obtain model training statistics.
The classifier details were retrieved using the classifier. explain(), and the importance values were extracted. A column chart was created to visualize the variable importance, showing the relative significance of different bands in the RF model.
Next, we assessed the model's performance by comparing the predicted regression points with the observed values in the training data. The predicted regression points were obtained at the same locations as the training data using the regression.sampleRegions() function. A scatter chart was generated to display the predicted versus observed values, and trendlines with R-squared values were included to indicate the goodness of fit.
To quantify the model's performance, the root mean squared error (RMSE) was computed by comparing the observation and prediction values. The residuals were calculated by subtracting the observation values from the predicted values, and then the RMSE was obtained by taking the square root of the mean of the squared residuals. The training RMSE value was printed to assess the accuracy of the RF model on the training data.
Moving on, we evaluated the accuracy of the RF model using the validation (test) data. The predicted regression points were obtained at the same locations as the validation data using regression.sampleRegions(). Similar to the training data assessment, a scatter chart was created to visualize the predicted versus observed values in the validation data. Trendlines with R-squared values were included to assess the goodness of fit.
To quantify the accuracy, the RMSE was computed by comparing the observation and prediction values in the validation data. Residuals were calculated, and the RMSE was obtained by taking the square root of the mean of the squared residuals. The validation RMSE value was printed to evaluate the accuracy of the RF model on the validation data.

**To know more about this project, read this [Medium Article](https://medium.com/@ansr2510/quantification-of-above-ground-biomass-in-auroville-greenbelt-using-google-earth-engine-3a9a0b5bb8e1).**
