---
layout: single
title: "Xarray Guidebook Part 1: Working with Multidimensional Climate Data"
date: 2026-10-07
permalink: /posts/2026/10/xarray-guidebook-part1/
excerpt: "An introduction to working with multidimensional climate datasets using Python and Xarray, covering data loading, inspection, selection, and exploratory analysis."
read_time: true
tags:
  - Python
  - Xarray
  - Climate Data
  - Data Analysis
---

# Working with multidimensional climate data using Python (Part 1)

In this notebook, I will go through the basics of xarray and other necessary packages that are used to explore and analyze multidimensional climate datasets (**CMIP6, ERA5, CRU, CHRIPS etc.**)

This notebook is structured as follows:
1. Reading dataset
1. Inspecting the dataset
1. filtering by time and location


```python
import xarray as xr
import numpy as np
import pandas as pd
```

**The main xarray objects**<br>
>DataArray: one labeled variable, for example daily precipitation or tasmax.

>Dataset: a container holding one or more variables, coordinates, and metadata.

>Dimensions: axes of an array, often time, latitude, longitude, or level.

>Coordinates: labels that identify positions along dimensions, such as dates and grid-cell locations.

>Attributes (attrs): metadata such as units, long name, and source.

## 0. Introduction to necessary file formats: 
**About NetCDF File:**<br>
>***NetCDF (Network Common Data Form)*** is a file format designed to store scientific data, especially multidimensional data such as temperature, precipitation, humidity, and wind speed over time and geographical locations.<br>
- Structure: Stores data in dimensions (e.g., time, latitude, longitude), variables, and metadata.
- Common uses: Climate model outputs, satellite observations, and reanalysis datasets such as ERA5.
- Python tools: xarray, netCDF4, and h5netcdf.<br>

**About GRIB File:**<br>
>***GRIB (GRIdded Binary)*** is a compact binary file format developed by the World Meteorological Organization (WMO) for storing and transmitting meteorological and weather forecast data.<br>
- Structure: Stores gridded weather variables along with information about time, geographical coordinates, forecast steps, and data levels.
- Common uses: Numerical weather prediction, weather forecasts, and meteorological reanalysis datasets.
- Python tools: cfgrib with xarray, and eccodes.

## 1. Reading Datasets

### 1.1 Opening a single netcdf file


```python
temp_df = xr.open_dataset("D:\CMIP6 Project\Thesis work\Data Analysis\Data\ERA5_Data\ERA5_Daily_Tmin_Tmax_1989_2019.nc")
temp_df
```

    c:\Users\Anwoy\miniconda3\envs\cmip6\Lib\site-packages\xarray\backends\plugins.py:110: RuntimeWarning: Engine 'cfgrib' loading failed:
    Cannot find the ecCodes library
      external_backend_entrypoints = backends_dict_from_pkg(entrypoints_unique)
    




<div><svg style="position: absolute; width: 0; height: 0; overflow: hidden">
<defs>
<symbol id="icon-database" viewBox="0 0 32 32">
<path d="M16 0c-8.837 0-16 2.239-16 5v4c0 2.761 7.163 5 16 5s16-2.239 16-5v-4c0-2.761-7.163-5-16-5z"></path>
<path d="M16 17c-8.837 0-16-2.239-16-5v6c0 2.761 7.163 5 16 5s16-2.239 16-5v-6c0 2.761-7.163 5-16 5z"></path>
<path d="M16 26c-8.837 0-16-2.239-16-5v6c0 2.761 7.163 5 16 5s16-2.239 16-5v-6c0 2.761-7.163 5-16 5z"></path>
</symbol>
<symbol id="icon-file-text2" viewBox="0 0 32 32">
<path d="M28.681 7.159c-0.694-0.947-1.662-2.053-2.724-3.116s-2.169-2.030-3.116-2.724c-1.612-1.182-2.393-1.319-2.841-1.319h-15.5c-1.378 0-2.5 1.121-2.5 2.5v27c0 1.378 1.122 2.5 2.5 2.5h23c1.378 0 2.5-1.122 2.5-2.5v-19.5c0-0.448-0.137-1.23-1.319-2.841zM24.543 5.457c0.959 0.959 1.712 1.825 2.268 2.543h-4.811v-4.811c0.718 0.556 1.584 1.309 2.543 2.268zM28 29.5c0 0.271-0.229 0.5-0.5 0.5h-23c-0.271 0-0.5-0.229-0.5-0.5v-27c0-0.271 0.229-0.5 0.5-0.5 0 0 15.499-0 15.5 0v7c0 0.552 0.448 1 1 1h7v19.5z"></path>
<path d="M23 26h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
<path d="M23 22h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
<path d="M23 18h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
</symbol>
</defs>
</svg>
<style>/* CSS stylesheet for displaying xarray objects in jupyterlab.
 *
 */

:root {
  --xr-font-color0: var(
    --jp-content-font-color0,
    var(--pst-color-text-base rgba(0, 0, 0, 1))
  );
  --xr-font-color2: var(
    --jp-content-font-color2,
    var(--pst-color-text-base, rgba(0, 0, 0, 0.54))
  );
  --xr-font-color3: var(
    --jp-content-font-color3,
    var(--pst-color-text-base, rgba(0, 0, 0, 0.38))
  );
  --xr-border-color: var(
    --jp-border-color2,
    hsl(from var(--pst-color-on-background, white) h s calc(l - 10))
  );
  --xr-disabled-color: var(
    --jp-layout-color3,
    hsl(from var(--pst-color-on-background, white) h s calc(l - 40))
  );
  --xr-background-color: var(
    --jp-layout-color0,
    var(--pst-color-on-background, white)
  );
  --xr-background-color-row-even: var(
    --jp-layout-color1,
    hsl(from var(--pst-color-on-background, white) h s calc(l - 5))
  );
  --xr-background-color-row-odd: var(
    --jp-layout-color2,
    hsl(from var(--pst-color-on-background, white) h s calc(l - 15))
  );
}

html[theme="dark"],
html[data-theme="dark"],
body[data-theme="dark"],
body.vscode-dark {
  --xr-font-color0: var(
    --jp-content-font-color0,
    var(--pst-color-text-base, rgba(255, 255, 255, 1))
  );
  --xr-font-color2: var(
    --jp-content-font-color2,
    var(--pst-color-text-base, rgba(255, 255, 255, 0.54))
  );
  --xr-font-color3: var(
    --jp-content-font-color3,
    var(--pst-color-text-base, rgba(255, 255, 255, 0.38))
  );
  --xr-border-color: var(
    --jp-border-color2,
    hsl(from var(--pst-color-on-background, #111111) h s calc(l + 10))
  );
  --xr-disabled-color: var(
    --jp-layout-color3,
    hsl(from var(--pst-color-on-background, #111111) h s calc(l + 40))
  );
  --xr-background-color: var(
    --jp-layout-color0,
    var(--pst-color-on-background, #111111)
  );
  --xr-background-color-row-even: var(
    --jp-layout-color1,
    hsl(from var(--pst-color-on-background, #111111) h s calc(l + 5))
  );
  --xr-background-color-row-odd: var(
    --jp-layout-color2,
    hsl(from var(--pst-color-on-background, #111111) h s calc(l + 15))
  );
}

.xr-wrap {
  display: block !important;
  min-width: 300px;
  max-width: 700px;
}

.xr-text-repr-fallback {
  /* fallback to plain text repr when CSS is not injected (untrusted notebook) */
  display: none;
}

.xr-header {
  padding-top: 6px;
  padding-bottom: 6px;
  margin-bottom: 4px;
  border-bottom: solid 1px var(--xr-border-color);
}

.xr-header > div,
.xr-header > ul {
  display: inline;
  margin-top: 0;
  margin-bottom: 0;
}

.xr-obj-type,
.xr-array-name {
  margin-left: 2px;
  margin-right: 10px;
}

.xr-obj-type {
  color: var(--xr-font-color2);
}

.xr-sections {
  padding-left: 0 !important;
  display: grid;
  grid-template-columns: 150px auto auto 1fr 0 20px 0 20px;
}

.xr-section-item {
  display: contents;
}

.xr-section-item input {
  display: inline-block;
  opacity: 0;
  height: 0;
}

.xr-section-item input + label {
  color: var(--xr-disabled-color);
  border: 2px solid transparent !important;
}

.xr-section-item input:enabled + label {
  cursor: pointer;
  color: var(--xr-font-color2);
}

.xr-section-item input:focus + label {
  border: 2px solid var(--xr-font-color0) !important;
}

.xr-section-item input:enabled + label:hover {
  color: var(--xr-font-color0);
}

.xr-section-summary {
  grid-column: 1;
  color: var(--xr-font-color2);
  font-weight: 500;
}

.xr-section-summary > span {
  display: inline-block;
  padding-left: 0.5em;
}

.xr-section-summary-in:disabled + label {
  color: var(--xr-font-color2);
}

.xr-section-summary-in + label:before {
  display: inline-block;
  content: "►";
  font-size: 11px;
  width: 15px;
  text-align: center;
}

.xr-section-summary-in:disabled + label:before {
  color: var(--xr-disabled-color);
}

.xr-section-summary-in:checked + label:before {
  content: "▼";
}

.xr-section-summary-in:checked + label > span {
  display: none;
}

.xr-section-summary,
.xr-section-inline-details {
  padding-top: 4px;
  padding-bottom: 4px;
}

.xr-section-inline-details {
  grid-column: 2 / -1;
}

.xr-section-details {
  display: none;
  grid-column: 1 / -1;
  margin-bottom: 5px;
}

.xr-section-summary-in:checked ~ .xr-section-details {
  display: contents;
}

.xr-array-wrap {
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: 20px auto;
}

.xr-array-wrap > label {
  grid-column: 1;
  vertical-align: top;
}

.xr-preview {
  color: var(--xr-font-color3);
}

.xr-array-preview,
.xr-array-data {
  padding: 0 5px !important;
  grid-column: 2;
}

.xr-array-data,
.xr-array-in:checked ~ .xr-array-preview {
  display: none;
}

.xr-array-in:checked ~ .xr-array-data,
.xr-array-preview {
  display: inline-block;
}

.xr-dim-list {
  display: inline-block !important;
  list-style: none;
  padding: 0 !important;
  margin: 0;
}

.xr-dim-list li {
  display: inline-block;
  padding: 0;
  margin: 0;
}

.xr-dim-list:before {
  content: "(";
}

.xr-dim-list:after {
  content: ")";
}

.xr-dim-list li:not(:last-child):after {
  content: ",";
  padding-right: 5px;
}

.xr-has-index {
  font-weight: bold;
}

.xr-var-list,
.xr-var-item {
  display: contents;
}

.xr-var-item > div,
.xr-var-item label,
.xr-var-item > .xr-var-name span {
  background-color: var(--xr-background-color-row-even);
  border-color: var(--xr-background-color-row-odd);
  margin-bottom: 0;
  padding-top: 2px;
}

.xr-var-item > .xr-var-name:hover span {
  padding-right: 5px;
}

.xr-var-list > li:nth-child(odd) > div,
.xr-var-list > li:nth-child(odd) > label,
.xr-var-list > li:nth-child(odd) > .xr-var-name span {
  background-color: var(--xr-background-color-row-odd);
  border-color: var(--xr-background-color-row-even);
}

.xr-var-name {
  grid-column: 1;
}

.xr-var-dims {
  grid-column: 2;
}

.xr-var-dtype {
  grid-column: 3;
  text-align: right;
  color: var(--xr-font-color2);
}

.xr-var-preview {
  grid-column: 4;
}

.xr-index-preview {
  grid-column: 2 / 5;
  color: var(--xr-font-color2);
}

.xr-var-name,
.xr-var-dims,
.xr-var-dtype,
.xr-preview,
.xr-attrs dt {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  padding-right: 10px;
}

.xr-var-name:hover,
.xr-var-dims:hover,
.xr-var-dtype:hover,
.xr-attrs dt:hover {
  overflow: visible;
  width: auto;
  z-index: 1;
}

.xr-var-attrs,
.xr-var-data,
.xr-index-data {
  display: none;
  border-top: 2px dotted var(--xr-background-color);
  padding-bottom: 20px !important;
  padding-top: 10px !important;
}

.xr-var-attrs-in + label,
.xr-var-data-in + label,
.xr-index-data-in + label {
  padding: 0 1px;
}

.xr-var-attrs-in:checked ~ .xr-var-attrs,
.xr-var-data-in:checked ~ .xr-var-data,
.xr-index-data-in:checked ~ .xr-index-data {
  display: block;
}

.xr-var-data > table {
  float: right;
}

.xr-var-data > pre,
.xr-index-data > pre,
.xr-var-data > table > tbody > tr {
  background-color: transparent !important;
}

.xr-var-name span,
.xr-var-data,
.xr-index-name div,
.xr-index-data,
.xr-attrs {
  padding-left: 25px !important;
}

.xr-attrs,
.xr-var-attrs,
.xr-var-data,
.xr-index-data {
  grid-column: 1 / -1;
}

dl.xr-attrs {
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: 125px auto;
}

.xr-attrs dt,
.xr-attrs dd {
  padding: 0;
  margin: 0;
  float: left;
  padding-right: 10px;
  width: auto;
}

.xr-attrs dt {
  font-weight: normal;
  grid-column: 1;
}

.xr-attrs dt:hover span {
  display: inline-block;
  background: var(--xr-background-color);
  padding-right: 10px;
}

.xr-attrs dd {
  grid-column: 2;
  white-space: pre-wrap;
  word-break: break-all;
}

.xr-icon-database,
.xr-icon-file-text2,
.xr-no-icon {
  display: inline-block;
  vertical-align: middle;
  width: 1em;
  height: 1.5em !important;
  stroke-width: 0;
  stroke: currentColor;
  fill: currentColor;
}

.xr-var-attrs-in:checked + label > .xr-icon-file-text2,
.xr-var-data-in:checked + label > .xr-icon-database,
.xr-index-data-in:checked + label > .xr-icon-database {
  color: var(--xr-font-color0);
  filter: drop-shadow(1px 1px 5px var(--xr-font-color2));
  stroke-width: 0.8px;
}
</style><pre class='xr-text-repr-fallback'>&lt;xarray.Dataset&gt; Size: 75MB
Dimensions:     (valid_time: 11322, latitude: 33, longitude: 25)
Coordinates:
  * latitude    (latitude) float64 264B 28.0 27.75 27.5 ... 20.5 20.25 20.0
  * longitude   (longitude) float64 200B 87.0 87.25 87.5 ... 92.5 92.75 93.0
  * valid_time  (valid_time) datetime64[ns] 91kB 1989-01-01 ... 2019-12-31
Data variables:
    tasmax      (valid_time, latitude, longitude) float32 37MB ...
    tasmin      (valid_time, latitude, longitude) float32 37MB ...
Attributes:
    GRIB_centre:             ecmf
    GRIB_centreDescription:  European Centre for Medium-Range Weather Forecasts
    GRIB_subCentre:          0
    Conventions:             CF-1.7
    institution:             European Centre for Medium-Range Weather Forecasts
    history:                 2026-02-18T15:22 GRIB to CDM+CF via cfgrib-0.9.1...</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.Dataset</div></div><ul class='xr-sections'><li class='xr-section-item'><input id='section-71d5a694-235c-4ea1-805b-9d038ac82daf' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-71d5a694-235c-4ea1-805b-9d038ac82daf' class='xr-section-summary'  title='Expand/collapse section'>Dimensions:</label><div class='xr-section-inline-details'><ul class='xr-dim-list'><li><span class='xr-has-index'>valid_time</span>: 11322</li><li><span class='xr-has-index'>latitude</span>: 33</li><li><span class='xr-has-index'>longitude</span>: 25</li></ul></div><div class='xr-section-details'></div></li><li class='xr-section-item'><input id='section-8818b9de-0399-405e-9ae4-2a09e4900941' class='xr-section-summary-in' type='checkbox'  checked><label for='section-8818b9de-0399-405e-9ae4-2a09e4900941' class='xr-section-summary' >Coordinates: <span>(3)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>latitude</span></div><div class='xr-var-dims'>(latitude)</div><div class='xr-var-dtype'>float64</div><div class='xr-var-preview xr-preview'>28.0 27.75 27.5 ... 20.5 20.25 20.0</div><input id='attrs-15412e0c-b9e1-46d4-a4d5-f3c5a31a0cb0' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-15412e0c-b9e1-46d4-a4d5-f3c5a31a0cb0' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-2e58ff9b-4764-417f-915e-0b3d1d917829' class='xr-var-data-in' type='checkbox'><label for='data-2e58ff9b-4764-417f-915e-0b3d1d917829' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>units :</span></dt><dd>degrees_north</dd><dt><span>standard_name :</span></dt><dd>latitude</dd><dt><span>long_name :</span></dt><dd>latitude</dd><dt><span>stored_direction :</span></dt><dd>decreasing</dd></dl></div><div class='xr-var-data'><pre>array([28.  , 27.75, 27.5 , 27.25, 27.  , 26.75, 26.5 , 26.25, 26.  , 25.75,
       25.5 , 25.25, 25.  , 24.75, 24.5 , 24.25, 24.  , 23.75, 23.5 , 23.25,
       23.  , 22.75, 22.5 , 22.25, 22.  , 21.75, 21.5 , 21.25, 21.  , 20.75,
       20.5 , 20.25, 20.  ])</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>longitude</span></div><div class='xr-var-dims'>(longitude)</div><div class='xr-var-dtype'>float64</div><div class='xr-var-preview xr-preview'>87.0 87.25 87.5 ... 92.5 92.75 93.0</div><input id='attrs-6ca189b4-bcdc-4208-9214-09d31449725d' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-6ca189b4-bcdc-4208-9214-09d31449725d' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-1bf31a6c-12f5-429a-8117-f934d1c6fe93' class='xr-var-data-in' type='checkbox'><label for='data-1bf31a6c-12f5-429a-8117-f934d1c6fe93' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>units :</span></dt><dd>degrees_east</dd><dt><span>standard_name :</span></dt><dd>longitude</dd><dt><span>long_name :</span></dt><dd>longitude</dd></dl></div><div class='xr-var-data'><pre>array([87.  , 87.25, 87.5 , 87.75, 88.  , 88.25, 88.5 , 88.75, 89.  , 89.25,
       89.5 , 89.75, 90.  , 90.25, 90.5 , 90.75, 91.  , 91.25, 91.5 , 91.75,
       92.  , 92.25, 92.5 , 92.75, 93.  ])</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>valid_time</span></div><div class='xr-var-dims'>(valid_time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1989-01-01 ... 2019-12-31</div><input id='attrs-79866c8f-121b-4236-8078-6874d1a2be10' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-79866c8f-121b-4236-8078-6874d1a2be10' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-8367ed13-162f-4378-b16c-f6a3ffade938' class='xr-var-data-in' type='checkbox'><label for='data-8367ed13-162f-4378-b16c-f6a3ffade938' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>time</dd><dt><span>standard_name :</span></dt><dd>time</dd><dt><span>time_shift :</span></dt><dd>0 days 06:00:00</dd></dl></div><div class='xr-var-data'><pre>array([&#x27;1989-01-01T00:00:00.000000000&#x27;, &#x27;1989-01-02T00:00:00.000000000&#x27;,
       &#x27;1989-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-29T00:00:00.000000000&#x27;,
       &#x27;2019-12-30T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-bc4ffea4-1138-4496-8c1b-f482bda39af9' class='xr-section-summary-in' type='checkbox'  checked><label for='section-bc4ffea4-1138-4496-8c1b-f482bda39af9' class='xr-section-summary' >Data variables: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>tasmax</span></div><div class='xr-var-dims'>(valid_time, latitude, longitude)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>...</div><input id='attrs-bbf5037b-e1d5-44d0-a7c4-e10fc7913132' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-bbf5037b-e1d5-44d0-a7c4-e10fc7913132' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-a3dc76de-4c82-4627-a7fb-bbeeb8b51316' class='xr-var-data-in' type='checkbox'><label for='data-a3dc76de-4c82-4627-a7fb-bbeeb8b51316' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>an</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>825</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>25</dd><dt><span>GRIB_Ny :</span></dt><dd>33</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.25</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.25</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>28.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.0</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>87.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>93.0</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily maximum near-surface air temperature</dd><dt><span>units :</span></dt><dd>°C</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><pre>[9340650 values with dtype=float32]</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span>tasmin</span></div><div class='xr-var-dims'>(valid_time, latitude, longitude)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>...</div><input id='attrs-eb57c4ad-e654-4229-b743-5a3e9971731c' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-eb57c4ad-e654-4229-b743-5a3e9971731c' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-4ae4fe2c-88d6-4ae0-a966-bc57bcb1c133' class='xr-var-data-in' type='checkbox'><label for='data-4ae4fe2c-88d6-4ae0-a966-bc57bcb1c133' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>an</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>825</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>25</dd><dt><span>GRIB_Ny :</span></dt><dd>33</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.25</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.25</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>28.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.0</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>87.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>93.0</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily minimum near-surface air temperature</dd><dt><span>units :</span></dt><dd>°C</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><pre>[9340650 values with dtype=float32]</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-002d6a0c-bbe4-4860-b3d9-8a63f2336247' class='xr-section-summary-in' type='checkbox'  ><label for='section-002d6a0c-bbe4-4860-b3d9-8a63f2336247' class='xr-section-summary' >Indexes: <span>(3)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-index-name'><div>latitude</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-04a919c5-974b-4bec-bba5-ee7f1655f040' class='xr-index-data-in' type='checkbox'/><label for='index-04a919c5-974b-4bec-bba5-ee7f1655f040' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(Index([ 28.0, 27.75,  27.5, 27.25,  27.0, 26.75,  26.5, 26.25,  26.0, 25.75,
        25.5, 25.25,  25.0, 24.75,  24.5, 24.25,  24.0, 23.75,  23.5, 23.25,
        23.0, 22.75,  22.5, 22.25,  22.0, 21.75,  21.5, 21.25,  21.0, 20.75,
        20.5, 20.25,  20.0],
      dtype=&#x27;float64&#x27;, name=&#x27;latitude&#x27;))</pre></div></li><li class='xr-var-item'><div class='xr-index-name'><div>longitude</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-32ad3afe-0a96-4525-ab3b-627ddbc0e3b5' class='xr-index-data-in' type='checkbox'/><label for='index-32ad3afe-0a96-4525-ab3b-627ddbc0e3b5' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(Index([ 87.0, 87.25,  87.5, 87.75,  88.0, 88.25,  88.5, 88.75,  89.0, 89.25,
        89.5, 89.75,  90.0, 90.25,  90.5, 90.75,  91.0, 91.25,  91.5, 91.75,
        92.0, 92.25,  92.5, 92.75,  93.0],
      dtype=&#x27;float64&#x27;, name=&#x27;longitude&#x27;))</pre></div></li><li class='xr-var-item'><div class='xr-index-name'><div>valid_time</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-2a184090-5f17-4dd0-ab9d-ca87c3c77fe4' class='xr-index-data-in' type='checkbox'/><label for='index-2a184090-5f17-4dd0-ab9d-ca87c3c77fe4' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(DatetimeIndex([&#x27;1989-01-01&#x27;, &#x27;1989-01-02&#x27;, &#x27;1989-01-03&#x27;, &#x27;1989-01-04&#x27;,
               &#x27;1989-01-05&#x27;, &#x27;1989-01-06&#x27;, &#x27;1989-01-07&#x27;, &#x27;1989-01-08&#x27;,
               &#x27;1989-01-09&#x27;, &#x27;1989-01-10&#x27;,
               ...
               &#x27;2019-12-22&#x27;, &#x27;2019-12-23&#x27;, &#x27;2019-12-24&#x27;, &#x27;2019-12-25&#x27;,
               &#x27;2019-12-26&#x27;, &#x27;2019-12-27&#x27;, &#x27;2019-12-28&#x27;, &#x27;2019-12-29&#x27;,
               &#x27;2019-12-30&#x27;, &#x27;2019-12-31&#x27;],
              dtype=&#x27;datetime64[ns]&#x27;, name=&#x27;valid_time&#x27;, length=11322, freq=None))</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-43f75958-f53a-4125-b5f0-df216bdc6969' class='xr-section-summary-in' type='checkbox'  checked><label for='section-43f75958-f53a-4125-b5f0-df216bdc6969' class='xr-section-summary' >Attributes: <span>(6)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'><dt><span>GRIB_centre :</span></dt><dd>ecmf</dd><dt><span>GRIB_centreDescription :</span></dt><dd>European Centre for Medium-Range Weather Forecasts</dd><dt><span>GRIB_subCentre :</span></dt><dd>0</dd><dt><span>Conventions :</span></dt><dd>CF-1.7</dd><dt><span>institution :</span></dt><dd>European Centre for Medium-Range Weather Forecasts</dd><dt><span>history :</span></dt><dd>2026-02-18T15:22 GRIB to CDM+CF via cfgrib-0.9.15.1/ecCodes-2.42.0 with {&quot;source&quot;: &quot;2m_temperature.grib&quot;, &quot;filter_by_keys&quot;: {&quot;stream&quot;: [&quot;oper&quot;]}, &quot;encode_cf&quot;: [&quot;parameter&quot;, &quot;time&quot;, &quot;geography&quot;, &quot;vertical&quot;]}
earthkit.transforms.aggregate.temporal.daily_reduce(2m_temperature_stream-oper, how=max, **{&#x27;time_shift&#x27;: {&#x27;hours&#x27;: 6}})</dd></dl></div></li></ul></div></div>



### 1.2 Opening multiple datasets


```python
# Files should have compatible dimensions and coordinates
ds = xr.open_mfdataset(
    r"D:\CMIP6 Project\Thesis work\Data Analysis\Data\ERA5_Data\tasmax\era5_max*.nc",
    combine="by_coords"
)
```

### 1.3 Opening GRIB file

```python
import cfgrib
data = cfgrib.open_datasets(file_location)
```
**Note: If you face an error while importing cfgrib, use this code.**<br>
```python
import os
import sys
from pathlib import Path

env = Path(sys.prefix)
dll_dir = env / "Library" / "bin"

print("DLL directory exists:", dll_dir.exists())
print("ecCodes DLL exists:", (dll_dir / "eccodes.dll").exists())

if dll_dir.exists():
    os.environ["PATH"] = str(dll_dir) + os.pathsep + os.environ.get("PATH", "")
    if hasattr(os, "add_dll_directory"):
        os.add_dll_directory(str(dll_dir))

import eccodes
print("ecCodes version:", eccodes.codes_get_api_version())
```


```python

```

## 2. Inspecting the dataset


```python
print(temp_df.data_vars)        # available data variables
print(temp_df.coords)           # coordinate names and values
print(temp_df.dims)             # dimension sizes
print(temp_df.attrs)            # global metadata
print(temp_df["tasmax"].attrs)      # metadata for one variable, if it is named tp
```

    Data variables:
        tasmax   (valid_time, latitude, longitude) float32 37MB ...
        tasmin   (valid_time, latitude, longitude) float32 37MB ...
    Coordinates:
      * latitude    (latitude) float64 264B 28.0 27.75 27.5 ... 20.5 20.25 20.0
      * longitude   (longitude) float64 200B 87.0 87.25 87.5 ... 92.5 92.75 93.0
      * valid_time  (valid_time) datetime64[ns] 91kB 1989-01-01 ... 2019-12-31
    FrozenMappingWarningOnValuesAccess({'valid_time': 11322, 'latitude': 33, 'longitude': 25})
    {'GRIB_centre': 'ecmf', 'GRIB_centreDescription': 'European Centre for Medium-Range Weather Forecasts', 'GRIB_subCentre': 0, 'Conventions': 'CF-1.7', 'institution': 'European Centre for Medium-Range Weather Forecasts', 'history': '2026-02-18T15:22 GRIB to CDM+CF via cfgrib-0.9.15.1/ecCodes-2.42.0 with {"source": "2m_temperature.grib", "filter_by_keys": {"stream": ["oper"]}, "encode_cf": ["parameter", "time", "geography", "vertical"]}\nearthkit.transforms.aggregate.temporal.daily_reduce(2m_temperature_stream-oper, how=max, **{\'time_shift\': {\'hours\': 6}})'}
    {'GRIB_paramId': 167, 'GRIB_dataType': 'an', 'GRIB_numberOfPoints': 825, 'GRIB_typeOfLevel': 'surface', 'GRIB_stepUnits': 1, 'GRIB_stepType': 'instant', 'GRIB_gridType': 'regular_ll', 'GRIB_uvRelativeToGrid': 0, 'GRIB_NV': 0, 'GRIB_Nx': 25, 'GRIB_Ny': 33, 'GRIB_cfName': 'unknown', 'GRIB_cfVarName': 't2m', 'GRIB_gridDefinitionDescription': 'Latitude/Longitude Grid', 'GRIB_iDirectionIncrementInDegrees': 0.25, 'GRIB_iScansNegatively': 0, 'GRIB_jDirectionIncrementInDegrees': 0.25, 'GRIB_jPointsAreConsecutive': 0, 'GRIB_jScansPositively': 0, 'GRIB_latitudeOfFirstGridPointInDegrees': 28.0, 'GRIB_latitudeOfLastGridPointInDegrees': 20.0, 'GRIB_longitudeOfFirstGridPointInDegrees': 87.0, 'GRIB_longitudeOfLastGridPointInDegrees': 93.0, 'GRIB_missingValue': 3.4028234663852886e+38, 'GRIB_name': '2 metre temperature', 'GRIB_shortName': '2t', 'GRIB_totalNumber': 0, 'GRIB_units': 'K', 'long_name': 'Daily maximum near-surface air temperature', 'units': '°C', 'standard_name': 'unknown', 'GRIB_surface': 0.0}
    


```python
# List variable names
list(temp_df.data_vars)

# Inspect a variable's dimensions, units, and missing values
var = temp_df["tasmax"]              # replace tasmax with your variable name
print(var.dims)
print(var.coords)
print(var.shape)
print(var.dtype)
print(var.isnull().sum().compute())  # compute if using Dask/lazy data
```

    ('valid_time', 'latitude', 'longitude')
    Coordinates:
      * latitude    (latitude) float64 264B 28.0 27.75 27.5 ... 20.5 20.25 20.0
      * longitude   (longitude) float64 200B 87.0 87.25 87.5 ... 92.5 92.75 93.0
      * valid_time  (valid_time) datetime64[ns] 91kB 1989-01-01 ... 2019-12-31
    (11322, 33, 25)
    float32
    <xarray.DataArray 'tasmax' ()> Size: 4B
    array(0)
    

## 3. Filtering dataset by time and location

We use `.sel` method to filter our data based on a specific or a range of time and/or location.

```python
# filtering by time
temp_df.sel(valid_time = "2000")
temp_df.sel(valid_time = "2000-07")

# filtering by time range
temp_df.sel(valid_time = slice("2000-01-01", "2000-12-31"))
```


```python
cell = temp_df.sel(latitude=23.8, longitude=90.4, method="nearest")
# If we don't have the exact coordinates, we can use the method = "nearest" to select the nearest grid points.

# Check which coordinates were selected
print(cell.latitude.values, cell.longitude.values)
```

    23.75 90.5
    


```python
# First time step, first 10 latitude rows, first 15 longitude columns
subset = temp_df.isel(valid_time=0, latitude=slice(0, 10), longitude=slice(0, 15))
```

### 3.2 Some things about filter based on geographic region

>The direction of latitude coordinates matters. Some datasets store latitude from north to south (descending), while others store it south to north (ascending). Check the coordinate values first.


```python
temp_df.latitude.values
```




    array([28.  , 27.75, 27.5 , 27.25, 27.  , 26.75, 26.5 , 26.25, 26.  ,
           25.75, 25.5 , 25.25, 25.  , 24.75, 24.5 , 24.25, 24.  , 23.75,
           23.5 , 23.25, 23.  , 22.75, 22.5 , 22.25, 22.  , 21.75, 21.5 ,
           21.25, 21.  , 20.75, 20.5 , 20.25, 20.  ])



This dataset has a descending latitude.


```python
# Example for descending latitude (common in some reanalysis files)
bd = temp_df.sel(
    latitude=slice(26.7, 20.5),
    longitude=slice(88.0, 92.8)
)
bd.latitude.values
```




    array([26.5 , 26.25, 26.  , 25.75, 25.5 , 25.25, 25.  , 24.75, 24.5 ,
           24.25, 24.  , 23.75, 23.5 , 23.25, 23.  , 22.75, 22.5 , 22.25,
           22.  , 21.75, 21.5 , 21.25, 21.  , 20.75, 20.5 ])




```python
# Example for ascending latitude
bd = ds.sel(
    latitude=slice(20.5, 26.7),
    longitude=slice(88.0, 92.8)
)

bd.latitude.values
```




    array([], dtype=float64)



**Tools & Libraries:** Python · Xarray · Jupyter Notebook · NumPy · Pandas · Matplotlib
