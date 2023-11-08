# Inspired by NASA SpaceApps challenge 2023
Inspired by the challenge `Be a Space Geologist` this project aims to explore LP DPAAC ASTER data as cloud optimized geotiffs (COG) from [AWS s3 bucket](https://registry.opendata.aws/aster-l1t/) and the USGS National Map of Surficial Mineralogy as source of data to train a model for mineral classification, then create a web map that displays minerals on the fly. 

## Environment setup
Python 10 or 11 virtual environment is needed on windows PC. Use `requirements/requirements.txt` file to install the required libraries (download GDAL and rasterio wheels [here](https://www.lfd.uci.edu/~gohlke/pythonlibs/) and modify the requirements file accordingly). If having issues with libraries, use requirements files with specific versions that have been successful (`requirements/requirements_version_specific_py10.txt` and `requirements/requirements_version_specific_py11.txt` for py10 and py11 respectively).

## Data
ASTER COGs are freely available for all users (no AWS account required) from `AWS s3 bucket` and can be accessed as follow:

install [AWS CLI](https://aws.amazon.com/cli/)

run: ```aws s3 ls --no-sign-request s3://aster-l1t/``` to list the content of the bucket.

complete the s3 url as:
`s3://aster-l1t/{sensor}/{epsg}/{path:03d}/{row:03d}/{yyyymmdd}/{granule}_{sensor}.tif`

`s3://aster-l1t/{sensor}/{epsg}/{path:03d}/{row:03d}/{yyyymmdd}/{granule}_{sensor}_stac.json`` is the metadata

EXAMPLE: 
`s3://aster-l1t/SWIR/32611/137/568/20080101/AST_L1T_00301012008054749_20170730074450_36729_SWIR.tif``

COMMAND: 
```aws s3 ls --no-sign-request s3://aster-l1t/SWIR/32611/137/568/20080101/AST_L1T_00301012008054749_20170730074450_36729_SWIR.tif```

To list COG from s3 bucket we can run the ls command recursively  
- `s3 ls --no-sign-request s3://aster-l1t/SWIR --recursive`
- `s3 ls --no-sign-request s3://aster-l1t/SWIR/32611/ --recursive`
- `s3 ls --no-sign-request s3://aster-l1t/SWIR/32611/137 --recursive`
- `s3 ls --no-sign-request s3://aster-l1t/SWIR/32611/137/568 --recursive`
- `s3 ls --no-sign-request s3://aster-l1t/SWIR/32611/137/568/20080101 --recursive`

To access the aws s3 bucket with no credentials we have to set the config file from this repo as: `~/.aws/config` on Linux or macOS, or as `C:\Users\USERNAME\.aws\config` on Windows.

We can now load COGs from aws s3 bucket to memory using rasterio. An example is given in the `Read_Aster_COG_from_AWS_s3_bucket.ipynb` file.  


## Setup jupyter notebook from virtual machine
# From the VM terminal run:
```gcloud compute ssh --project PROJECT_ID --zone ZONE INSTANCE_NAME -- -L 8080:localhost:8080```
# permission is required. Authentication scopes can be set as:

# To-Do
### create checker
- Create web app using django;
- Add imput fields (path, row, date, cloud cover) view button whose action displays the image (python as backenb);
- Add shapefile input field and clip button to clip the image to the extent of the shapefile before processing;  
### geo index algorithm
- Add a function that generates mineral indices (customised). Add input function and index generator button;
- create maptiles;
- Add a function that uploads maptiles to Google Cloud Storage bucket;
### Tensorflow.js classifier
- Generate a model that classifies mineral using tensorflow.js;
### Map page
- Add a page that displays a 3D map (mineral indices);
- use tensorflow.js to classify minerals on-the-fly.



