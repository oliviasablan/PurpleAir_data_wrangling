# Quality control procedures and data wrangling for PurpleAir PM<sub>2.5</sub> observations 
## Created and maintain by: Olivia Sablan <br> Last Updated: May 27, 2025 <br>
### Contact: olivia.sablan@gmail.com

## Overview
This repository contains Python code used in our NIH funded project to wrangle and clean data from our PurpleAir sensors deployed to the field. This combines data from the PurpleAir Data Download Tool, which provides access to the real-time data via WiFi from PurpleAir sensors, and the data from the physical PurpleAir SD card. We use quality control procedures to discard erroneous data using methods developed in previous work (Sablan et al. 2025; https://doi-org.ezproxy2.library.colostate.edu/10.1029/2023GH000982). This repository does not include any data analysis.

## General Method Outline
In the following code, we combine data from the PurpleAir Data Download Tool and SD cards. This allows us to have the most complete obervation records, as some PurpleAir sensors cycle off of WiFi and do not transmit data to the servers. Data is pulled monthly from the Data Download tool and removed from the SD card once a sensor has been returned from the field. Next, the data is quality controlled. The following data is discarded: (a) temperature >65°C, (b) relative humidity >100%, (c) channel disagreement >10% from the average of the two channels or 10 μg m<sup>−3</sup> in the absolute difference between the channels, and (d) measurements >500 μg m<sup>−3</sup>. Then, we take 10-minute averages of the data, and use the Barkjohn et al. (2021) correction factor to improve observation accuracy. Negative concentrations are removed following correction. Lastly, we take daily and hourly averages.

## Code File Description 
- **printfieldtoPull.ipynb** - allows for easy use of the PurpleAir Data Download Tool, by printing all the readkeys and sensor indexes needed
-  **OnlineandSD_step1.ipynb** - combines SD card data and WiFi transmitted data
-  **qualitycheck_step2.ipynb** - quality controls combined data and tracks discarded data
-  **dataAverages_step3.ipynb** - takes daily and hourly averages at each sensor
