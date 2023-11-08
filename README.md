# Inspired by NASA SpaceApps challenge 2023
Inspired by the challenge `Be a Space Geologist` this project aims to explore Harmonized Landsat Sentinel 2 (HLS) data as cloud optimized geotiffs (COG) and the USGS National Map of Surficial Mineralogy as source of data to train a model for mineral classification, then create a web map that displays minerals on the fly. 

## Environment setup
Python 10 or 11 virtual environment is needed on windows PC. Use `requirements/requirements.txt` file to install the required libraries (download GDAL and rasterio wheels [here](https://www.lfd.uci.edu/~gohlke/pythonlibs/) and modify the requirements file accordingly). If having issues with libraries, use requirements files with specific versions that have been successful (`requirements/requirements_version_specific_py10.txt` and `requirements/requirements_version_specific_py11.txt` for py10 and py11 respectively).

## Data
HLS data can downloaded by cloning the [hls-bulk-download](https://git.earthdata.nasa.gov/scm/lpdur/hls-bulk-download.git)repository and running the script  
To authenticate, the `.netrc` file in this repository should be modified accordingly and placed in the users HOME directory on MAC or USERPROFILE on windows. For windows, rename the file to `_netrc`.  

Alternatively (recommended), HLS data can be manipulated in the cloud as COG as used in this project.

## Setup jupyter notebook from virtual machine
# From the VM terminal run:
$gcloud compute ssh --project PROJECT_ID --zone ZONE INSTANCE_NAME -- -L 8080:localhost:8080
# permission is required. Authentication scopes can be set as:

