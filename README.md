# **Navavishkar-in-Google-Earth-Engine**
## **Quantification Of Above Ground Biomass In Auroville Green Belt Using Google Earth Engine**

### **1 Loading and combining all raster variables**
In this step, we loaded various raster variables including Sentinel-2 (S2) data, SRTM elevation data, and slope data.

### **2 Preparing training data**
In this step, we prepared the training data using various datasets including GEDI L4B, Sentinel-2, SRTM elevation, and slope data. We started by loading the GEDI L4B dataset. The dataset was clipped to the study area boundary.

### **3 Training the random forest model**
In this step, we trained and evaluated a random forest (RF) model for biomass prediction. The RF model was configured with a parameter specifying the number of trees, set to 50 in this case.

<p style="text-align:center;"><img src="https://github.com/failed-wizard/Navavishkar-in-Google-Earth-Engine/blob/main/google_img.png" alt="AGB density map for Auroville Greenbelt." width="50%" height="50%"/></p>

### **4 Estimating the trained model performance**
In this step, we evaluated the performance and accuracy of the random forest (RF) model. We first used the .explain() method on the trained RF model to compute variable importance and obtain model training statistics.

**To know more about this project, read this [Medium Article](https://medium.com/@ansr2510/quantification-of-above-ground-biomass-in-auroville-greenbelt-using-google-earth-engine-3a9a0b5bb8e1).**
