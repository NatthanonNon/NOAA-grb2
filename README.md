# NOAA-grb2
GRB2 Tutorial with NOAA dataset

## Overview
This tutorial will show you how to deal with `GRIB data(.grb)` and `GRIB2 data(.grb2)` by using dataset from [NOAA](https://www.noaa.gov/) as an example.

There are 3 sections in this tutorial: **Data Scraping**, **Data Inspecting** and **Data Preprocessing**.

In the first place, I've learned how to get started with GRIB2 weather data from this [article](https://spire.com/tutorial/spire-weather-tutorial-intro-to-processing-grib2-data-with-python/). Although it gives me many useful code and understanding, it is not enogh to deal with my task. 

## Getting Started

### Objective

To get these data with specific unit from NOAA dataset
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

  - `conda install -c anaconda xarray`
  - `conda install -c conda-forge pynio`
  - `conda install -c anaconda pandas`
  - If it gives you this error `ImportError: libtbb.so.2: cannot open shared object file: No such file or directory` try `sudo apt-get install libtbb2`

### Dataset

Fotunately, NOAA had provided many climate dataset. In this totorial, we will use the dataset from [Global Forecast System (GFS)](https://www.ncdc.noaa.gov/data-access/model-data/model-datasets/global-forcast-system-gfs)  

And scrape the `GRIB data(.grb)` and `GRIB2 data(.grb2)` from `Product Types` > `GFS Analysis` > `GFS-ANL, Historical Model` which is this [link](https://www.ncei.noaa.gov/data/global-forecast-system/access/historical/analysis/)

The `period of record` of this dataset is `01Jan2007–15May2020` and the data was collected `4 times per day` `(00, 06, 12 and 18 UTC)`


## Data Scraping

As there are a lot of climate dataset 

## Data Inspecting

This section will show you how to inspect the data, then you can understand the data that is in the dataset and properly choose the one that suit your task.

## Data Preprocessing

If it gives you this error `free(): invalid pointer Aborted` instead of preprocess all dataset at once, try to spit all dataset into parts, then preprocess each part and concat the output csv together in the end  

