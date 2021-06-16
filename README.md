# NOAA-grb2
GRIB2 Tutorial with NOAA dataset

## Overview
This tutorial will show you how to deal with `GRIB data(.grb)` and `GRIB2 data(.grb2)` by using dataset from [NOAA](https://www.noaa.gov/) as an example.

There are 3 sections in this tutorial: **Data Scraping**, **Data Inspecting** and **Data Preprocessing**.

In the first place, I've learned how to get started with GRIB2 weather data from this [article](https://spire.com/tutorial/spire-weather-tutorial-intro-to-processing-grib2-data-with-python/). Although it gives me many useful code and understanding, it is not enough to deal with my task. 

## Getting Started

### Objective

To get these data with specific unit from NOAA dataset(`.grb` or `.grb2`)
  - `latitude (degree(-90 to +90))`
  - `longitude (degree(-180 to +180))`
  - `surface temperature(°c)`
  - `wind speed at 85000.0 Pa (km/hr)` 
  - `wind direction at 85000.0 Pa (degree(0-360))`
  - `datetime` as an index of the dataset
  - **We want only the data that located in Thailand**

### Dependency
- This tutorial was tested with Miniconda 3.8, python 3.8.5 and Ubuntu 20.04 LTS.
- Requirements: `xarray`, `PyNIO`, `BeautifulSoup`, `pandas`, `requests`and `urllib`
  ```
  conda install -c anaconda xarray
  conda install -c conda-forge pynio
  conda install -c anaconda beautifulsoup4 requests
  ```
  If it gives you this error `ImportError: libtbb.so.2: cannot open shared object file: No such file or directory` try 
  ```
  sudo apt-get install libtbb2
  ```
- In my case, as a Windows user, I run jupyter lab in miniconda environment on WSL(`Ubuntu 20.04 LTS`)
  - Installation
    - Open `Ubuntu 20.04 LTS`
    - Download [Miniconda Linux installers](https://docs.conda.io/en/latest/miniconda.html) `wget [installer-download-link]`
    - Set 777 permissions to the installer `chmod 777 [Miniconda-installer-file]`
    - Run the installer `./[Miniconda-installer-file]`
    - Close and Reopen the WSL to activate the conda
    - Create conda environment `conda create --name [conda-env]`
    - Activate miniconda environment `conda activate [conda-env]`
    - Install the libraries with the command above
  - Normal Use
    - Open `Ubuntu 20.04 LTS`
    - cd to the directory that the project belongs to e.g. `cd /mnt/c/Users/natthanon/Desktop/NOAA-grb2/`
    - Activate miniconda environment `conda activate [conda-env]`
    - Open jupyter lab using this command `jupyter lab` (It may not toggle the browser, you can simply copy the URL and paste it in the desirable browser)

### Dataset

Fotunately, NOAA has provided many climate dataset. In this tutorial, we will use the dataset from [Global Forecast System (GFS)](https://www.ncdc.noaa.gov/data-access/model-data/model-datasets/global-forcast-system-gfs)  

And scrape the `GRIB data(.grb)` and `GRIB2 data(.grb2)` from `Product Types` > `GFS Analysis` > `GFS-ANL, Historical Model` which is this [link](https://www.ncei.noaa.gov/data/global-forecast-system/access/historical/analysis/)

The `period of record` of this dataset is `01Jan2007–15May2020` and the data was collected `4 times per day` `(00, 06, 12 and 18 UTC)`


## Data Scraping

This section will show you how to scrape the data from NOAA, then you can modify the code to suit your task.

## Data Inspecting

This section will show you how to inspect the data by printing the `lookup key`, `human-readable name`, `units of measurement` and even `full metadata` of each variables, then you can understand all variables which are in the dataset and properly choose the one that suit your task.

## Data Preprocessing

This section will show you how to preprocess the data in the dataset, then you can get the data in the desirable format!
- `longitude`: convert `(degree(0 to 360))` to `(degree(-180 to +180))` which is the standard range
- `temperature`: convert `K` to `°c`
- `wind speed (km/hr)` and `wind direction (degree(0-360))`: get from `U-component at isobaric surface (Pa) (m/s)` and `V-component at isobaric surface (Pa) (m/s)` and choose only the data at `85000.0 Pa`
- `datetime`: get from `filename`
- Choose only the data that located in Thailand by using `geospatial bounding box`
- Set `datetime` as an index of the dataset

If it gives you this error `free(): invalid pointer Aborted` instead of preprocess all dataset at once, try to spit all dataset into parts, then preprocess each part and concat the output csv together in the end (In my case, each part consists of `385` .grb2 file)

## Output
The `output_data.csv` is look like this

|       | datetime | latitude | longitude | temperature | wind_speed | wind_direction |
|:-----:|:-------------------:|:----:|:----:|:---------:|:---------:|:---------:|
| **0** | 2017-11-07 07:00:00 | 20.0 | 97.5 | 13.128076 | 13.726042 | 43.228494 |
| **1** | 2017-11-07 07:00:00 | 20.0 | 98.0 | 15.928094 | 11.048007 | 57.959462 |
| **2** | 2017-11-07 07:00:00 | 20.0 | 98.5 | 16.128076 | 10.675245 | 69.713981 |
| **3** | 2017-11-07 07:00:00 | 20.0 | 99.0 | 15.828088	| 10.130219 | 64.575124 |
| .. | .. | .. | .. | .. | .. | .. |




