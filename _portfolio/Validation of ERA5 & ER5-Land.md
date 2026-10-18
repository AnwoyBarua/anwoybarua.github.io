---
title: "Validation of ERA5 and ERA5-Land reanalysis data (code)"
date: 2026-04-20
excerpt: "This post contains part of my codes used during my research project on validation of ERA5 and ERA5-Land.<br/>
<img src='/images/Portfolio Projects/Validation of ERA5 and ERA5Land/figures//Validation_of ERA5Land_(cover_page).png'>"
collection: portfolio
order: 1
---

## Matching Timezone and calendar of station and ERA5-Land data

Timezone of ERA5-Land was converted to local UTC+6 time zone and calendar type of BMD data matches with ERA5 Land data


```python
import xarray as xr
import pandas as pd
import numpy as np
```


```python
ERA5_Land = xr.open_dataset(r"D:\CMIP6 Project\Thesis work\Data Analysis\Data\ERA5Land_Data\merged_data\ERA5_Land_Daily_Tmin_Tmax_1950_2019(unmasked_localized).nc",
                            chunks = {"time": 365})
```


```python
ERA5_Land
```




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
</style><pre class='xr-text-repr-fallback'>&lt;xarray.Dataset&gt; Size: 625MB
Dimensions:     (latitude: 65, longitude: 47, valid_time: 25568)
Coordinates:
  * latitude    (latitude) float64 520B 27.0 26.9 26.8 26.7 ... 20.8 20.7 20.6
  * longitude   (longitude) float64 376B 88.0 88.1 88.2 88.3 ... 92.4 92.5 92.6
    number      int64 8B ...
  * valid_time  (valid_time) datetime64[ns] 205kB 1950-01-01 ... 2020-01-01
Data variables:
    t2m_min     (valid_time, latitude, longitude) float32 312MB dask.array&lt;chunksize=(25568, 65, 47), meta=np.ndarray&gt;
    t2m_max     (valid_time, latitude, longitude) float32 312MB dask.array&lt;chunksize=(25568, 65, 47), meta=np.ndarray&gt;</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.Dataset</div></div><ul class='xr-sections'><li class='xr-section-item'><input id='section-671b8d91-b54d-4282-9a12-a948156d2f06' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-671b8d91-b54d-4282-9a12-a948156d2f06' class='xr-section-summary'  title='Expand/collapse section'>Dimensions:</label><div class='xr-section-inline-details'><ul class='xr-dim-list'><li><span class='xr-has-index'>latitude</span>: 65</li><li><span class='xr-has-index'>longitude</span>: 47</li><li><span class='xr-has-index'>valid_time</span>: 25568</li></ul></div><div class='xr-section-details'></div></li><li class='xr-section-item'><input id='section-5bfeab6f-8a7e-4b66-afd1-89c441ac98fa' class='xr-section-summary-in' type='checkbox'  checked><label for='section-5bfeab6f-8a7e-4b66-afd1-89c441ac98fa' class='xr-section-summary' >Coordinates: <span>(4)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>latitude</span></div><div class='xr-var-dims'>(latitude)</div><div class='xr-var-dtype'>float64</div><div class='xr-var-preview xr-preview'>27.0 26.9 26.8 ... 20.8 20.7 20.6</div><input id='attrs-dba1e275-4e29-4242-9dd9-6b9d07e7f9fd' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-dba1e275-4e29-4242-9dd9-6b9d07e7f9fd' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-446d2e5d-0b51-4a84-8d03-0fd4b5edaeea' class='xr-var-data-in' type='checkbox'><label for='data-446d2e5d-0b51-4a84-8d03-0fd4b5edaeea' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>units :</span></dt><dd>degrees_north</dd><dt><span>standard_name :</span></dt><dd>latitude</dd><dt><span>long_name :</span></dt><dd>latitude</dd><dt><span>stored_direction :</span></dt><dd>decreasing</dd></dl></div><div class='xr-var-data'><pre>array([27. , 26.9, 26.8, 26.7, 26.6, 26.5, 26.4, 26.3, 26.2, 26.1, 26. , 25.9,
       25.8, 25.7, 25.6, 25.5, 25.4, 25.3, 25.2, 25.1, 25. , 24.9, 24.8, 24.7,
       24.6, 24.5, 24.4, 24.3, 24.2, 24.1, 24. , 23.9, 23.8, 23.7, 23.6, 23.5,
       23.4, 23.3, 23.2, 23.1, 23. , 22.9, 22.8, 22.7, 22.6, 22.5, 22.4, 22.3,
       22.2, 22.1, 22. , 21.9, 21.8, 21.7, 21.6, 21.5, 21.4, 21.3, 21.2, 21.1,
       21. , 20.9, 20.8, 20.7, 20.6])</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>longitude</span></div><div class='xr-var-dims'>(longitude)</div><div class='xr-var-dtype'>float64</div><div class='xr-var-preview xr-preview'>88.0 88.1 88.2 ... 92.4 92.5 92.6</div><input id='attrs-11b50893-d1d2-45da-898a-38d227108dd2' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-11b50893-d1d2-45da-898a-38d227108dd2' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-69064e88-ae28-4924-bfd5-e2128999b91b' class='xr-var-data-in' type='checkbox'><label for='data-69064e88-ae28-4924-bfd5-e2128999b91b' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>units :</span></dt><dd>degrees_east</dd><dt><span>standard_name :</span></dt><dd>longitude</dd><dt><span>long_name :</span></dt><dd>longitude</dd></dl></div><div class='xr-var-data'><pre>array([88. , 88.1, 88.2, 88.3, 88.4, 88.5, 88.6, 88.7, 88.8, 88.9, 89. , 89.1,
       89.2, 89.3, 89.4, 89.5, 89.6, 89.7, 89.8, 89.9, 90. , 90.1, 90.2, 90.3,
       90.4, 90.5, 90.6, 90.7, 90.8, 90.9, 91. , 91.1, 91.2, 91.3, 91.4, 91.5,
       91.6, 91.7, 91.8, 91.9, 92. , 92.1, 92.2, 92.3, 92.4, 92.5, 92.6])</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span>number</span></div><div class='xr-var-dims'>()</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>...</div><input id='attrs-8d658010-83a6-4482-a0bb-58c076ee4d93' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-8d658010-83a6-4482-a0bb-58c076ee4d93' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-bccbdb47-0025-4009-9326-df2539919000' class='xr-var-data-in' type='checkbox'><label for='data-bccbdb47-0025-4009-9326-df2539919000' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>ensemble member numerical id</dd><dt><span>units :</span></dt><dd>1</dd><dt><span>standard_name :</span></dt><dd>realization</dd></dl></div><div class='xr-var-data'><pre>[1 values with dtype=int64]</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>valid_time</span></div><div class='xr-var-dims'>(valid_time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1950-01-01 ... 2020-01-01</div><input id='attrs-a2f50e09-e87c-40b9-8323-41e7d22830d8' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-a2f50e09-e87c-40b9-8323-41e7d22830d8' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-18040864-014b-4bc7-8ab7-9fe4c63156a7' class='xr-var-data-in' type='checkbox'><label for='data-18040864-014b-4bc7-8ab7-9fe4c63156a7' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([&#x27;1950-01-01T00:00:00.000000000&#x27;, &#x27;1950-01-02T00:00:00.000000000&#x27;,
       &#x27;1950-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-30T00:00:00.000000000&#x27;,
       &#x27;2019-12-31T00:00:00.000000000&#x27;, &#x27;2020-01-01T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-51d2d880-c161-490b-948f-dee878ddcb99' class='xr-section-summary-in' type='checkbox'  checked><label for='section-51d2d880-c161-490b-948f-dee878ddcb99' class='xr-section-summary' >Data variables: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>t2m_min</span></div><div class='xr-var-dims'>(valid_time, latitude, longitude)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(25568, 65, 47), meta=np.ndarray&gt;</div><input id='attrs-5e178923-a591-448b-8405-0e64ec497f95' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-5e178923-a591-448b-8405-0e64ec497f95' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-5bdadefa-5def-42ee-b855-bbd824a24929' class='xr-var-data-in' type='checkbox'><label for='data-5bdadefa-5def-42ee-b855-bbd824a24929' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily minimum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 297.97 MiB </td>
                        <td> 297.97 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (25568, 65, 47) </td>
                        <td> (25568, 65, 47) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 2 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="156" height="146" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="10" y1="0" x2="80" y2="70" style="stroke-width:2" />
  <line x1="10" y1="25" x2="80" y2="96" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="10" y1="0" x2="10" y2="25" style="stroke-width:2" />
  <line x1="80" y1="70" x2="80" y2="96" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="10.0,0.0 80.58823529411765,70.58823529411765 80.58823529411765,96.00085180870013 10.0,25.412616514582485" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Horizontal lines -->
  <line x1="10" y1="0" x2="35" y2="0" style="stroke-width:2" />
  <line x1="80" y1="70" x2="106" y2="70" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="10" y1="0" x2="80" y2="70" style="stroke-width:2" />
  <line x1="35" y1="0" x2="106" y2="70" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="10.0,0.0 35.41261651458248,0.0 106.00085180870013,70.58823529411765 80.58823529411765,70.58823529411765" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Horizontal lines -->
  <line x1="80" y1="70" x2="106" y2="70" style="stroke-width:2" />
  <line x1="80" y1="96" x2="106" y2="96" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="80" y1="70" x2="80" y2="96" style="stroke-width:2" />
  <line x1="106" y1="70" x2="106" y2="96" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="80.58823529411765,70.58823529411765 106.00085180870013,70.58823529411765 106.00085180870013,96.00085180870013 80.58823529411765,96.00085180870013" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="93.29454355140889" y="116.00085180870013" font-size="1.0rem" font-weight="100" text-anchor="middle" >47</text>
  <text x="126.00085180870013" y="83.29454355140889" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(0,126.00085180870013,83.29454355140889)">65</text>
  <text x="35.294117647058826" y="80.70673416164131" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(45,35.294117647058826,80.70673416164131)">25568</text>
</svg>
        </td>
    </tr>
</table></div></li><li class='xr-var-item'><div class='xr-var-name'><span>t2m_max</span></div><div class='xr-var-dims'>(valid_time, latitude, longitude)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(25568, 65, 47), meta=np.ndarray&gt;</div><input id='attrs-a80e2ef0-e93d-4b77-95ac-c2c5ab692a4e' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-a80e2ef0-e93d-4b77-95ac-c2c5ab692a4e' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-ceea32d9-db9a-45c5-af59-327784430c2c' class='xr-var-data-in' type='checkbox'><label for='data-ceea32d9-db9a-45c5-af59-327784430c2c' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily maximum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 297.97 MiB </td>
                        <td> 297.97 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (25568, 65, 47) </td>
                        <td> (25568, 65, 47) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 2 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="156" height="146" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="10" y1="0" x2="80" y2="70" style="stroke-width:2" />
  <line x1="10" y1="25" x2="80" y2="96" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="10" y1="0" x2="10" y2="25" style="stroke-width:2" />
  <line x1="80" y1="70" x2="80" y2="96" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="10.0,0.0 80.58823529411765,70.58823529411765 80.58823529411765,96.00085180870013 10.0,25.412616514582485" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Horizontal lines -->
  <line x1="10" y1="0" x2="35" y2="0" style="stroke-width:2" />
  <line x1="80" y1="70" x2="106" y2="70" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="10" y1="0" x2="80" y2="70" style="stroke-width:2" />
  <line x1="35" y1="0" x2="106" y2="70" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="10.0,0.0 35.41261651458248,0.0 106.00085180870013,70.58823529411765 80.58823529411765,70.58823529411765" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Horizontal lines -->
  <line x1="80" y1="70" x2="106" y2="70" style="stroke-width:2" />
  <line x1="80" y1="96" x2="106" y2="96" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="80" y1="70" x2="80" y2="96" style="stroke-width:2" />
  <line x1="106" y1="70" x2="106" y2="96" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="80.58823529411765,70.58823529411765 106.00085180870013,70.58823529411765 106.00085180870013,96.00085180870013 80.58823529411765,96.00085180870013" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="93.29454355140889" y="116.00085180870013" font-size="1.0rem" font-weight="100" text-anchor="middle" >47</text>
  <text x="126.00085180870013" y="83.29454355140889" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(0,126.00085180870013,83.29454355140889)">65</text>
  <text x="35.294117647058826" y="80.70673416164131" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(45,35.294117647058826,80.70673416164131)">25568</text>
</svg>
        </td>
    </tr>
</table></div></li></ul></div></li><li class='xr-section-item'><input id='section-cc6b3875-55ae-4b58-b115-b5afc0ac392f' class='xr-section-summary-in' type='checkbox'  ><label for='section-cc6b3875-55ae-4b58-b115-b5afc0ac392f' class='xr-section-summary' >Indexes: <span>(3)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-index-name'><div>latitude</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-6dbd7509-00ba-40b5-a2fa-583f0ba03477' class='xr-index-data-in' type='checkbox'/><label for='index-6dbd7509-00ba-40b5-a2fa-583f0ba03477' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(Index([              27.0,               26.9, 26.799999999999997,
       26.699999999999996, 26.599999999999994, 26.499999999999993,
        26.39999999999999,  26.29999999999999,  26.19999999999999,
       26.099999999999987, 25.999999999999986, 25.899999999999984,
       25.799999999999983,  25.69999999999998,  25.59999999999998,
        25.49999999999998, 25.399999999999977, 25.299999999999976,
       25.199999999999974, 25.099999999999973,  24.99999999999997,
        24.89999999999997,  24.79999999999997, 24.699999999999967,
       24.599999999999966, 24.499999999999964, 24.399999999999963,
        24.29999999999996,  24.19999999999996,  24.09999999999996,
       23.999999999999957, 23.899999999999956, 23.799999999999955,
       23.699999999999953,  23.59999999999995,  23.49999999999995,
        23.39999999999995, 23.299999999999947, 23.199999999999946,
       23.099999999999945, 22.999999999999943,  22.89999999999994,
        22.79999999999994,  22.69999999999994, 22.599999999999937,
       22.499999999999936, 22.399999999999935, 22.299999999999933,
       22.199999999999932,  22.09999999999993,  21.99999999999993,
       21.899999999999928, 21.799999999999926, 21.699999999999925,
       21.599999999999923, 21.499999999999922,  21.39999999999992,
        21.29999999999992, 21.199999999999918, 21.099999999999916,
       20.999999999999915, 20.899999999999913, 20.799999999999912,
        20.69999999999991,               20.6],
      dtype=&#x27;float64&#x27;, name=&#x27;latitude&#x27;))</pre></div></li><li class='xr-var-item'><div class='xr-index-name'><div>longitude</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-7ed1951d-71c1-4261-bf76-c7d8aab214dd' class='xr-index-data-in' type='checkbox'/><label for='index-7ed1951d-71c1-4261-bf76-c7d8aab214dd' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(Index([             88.0,              88.1, 88.19999999999999,
       88.29999999999998, 88.39999999999998, 88.49999999999997,
       88.59999999999997, 88.69999999999996, 88.79999999999995,
       88.89999999999995, 88.99999999999994, 89.09999999999994,
       89.19999999999993, 89.29999999999993, 89.39999999999992,
       89.49999999999991, 89.59999999999991,  89.6999999999999,
        89.7999999999999, 89.89999999999989, 89.99999999999989,
       90.09999999999988, 90.19999999999987, 90.29999999999987,
       90.39999999999986, 90.49999999999986, 90.59999999999985,
       90.69999999999985, 90.79999999999984, 90.89999999999984,
       90.99999999999983, 91.09999999999982, 91.19999999999982,
       91.29999999999981,  91.3999999999998,  91.4999999999998,
        91.5999999999998, 91.69999999999979, 91.79999999999978,
       91.89999999999978, 91.99999999999977, 92.09999999999977,
       92.19999999999976, 92.29999999999976, 92.39999999999975,
       92.49999999999974,              92.6],
      dtype=&#x27;float64&#x27;, name=&#x27;longitude&#x27;))</pre></div></li><li class='xr-var-item'><div class='xr-index-name'><div>valid_time</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-04638b81-6202-44b8-96b4-f9bceefe3dca' class='xr-index-data-in' type='checkbox'/><label for='index-04638b81-6202-44b8-96b4-f9bceefe3dca' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(DatetimeIndex([&#x27;1950-01-01&#x27;, &#x27;1950-01-02&#x27;, &#x27;1950-01-03&#x27;, &#x27;1950-01-04&#x27;,
               &#x27;1950-01-05&#x27;, &#x27;1950-01-06&#x27;, &#x27;1950-01-07&#x27;, &#x27;1950-01-08&#x27;,
               &#x27;1950-01-09&#x27;, &#x27;1950-01-10&#x27;,
               ...
               &#x27;2019-12-23&#x27;, &#x27;2019-12-24&#x27;, &#x27;2019-12-25&#x27;, &#x27;2019-12-26&#x27;,
               &#x27;2019-12-27&#x27;, &#x27;2019-12-28&#x27;, &#x27;2019-12-29&#x27;, &#x27;2019-12-30&#x27;,
               &#x27;2019-12-31&#x27;, &#x27;2020-01-01&#x27;],
              dtype=&#x27;datetime64[ns]&#x27;, name=&#x27;valid_time&#x27;, length=25568, freq=None))</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-b118d6e6-08c5-44ac-8f06-363c3dc3b093' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-b118d6e6-08c5-44ac-8f06-363c3dc3b093' class='xr-section-summary'  title='Expand/collapse section'>Attributes: <span>(0)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'></dl></div></li></ul></div></div>




```python
25568 * 59 * 46
```




    69391552




```python
BMD_temp_data = pd.read_csv(r"D:\CMIP6 Project\Thesis work\BMD_stations Data\BMD_temp_data_cleaned(2).csv")
```


```python
BMD_temp_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Station_ID</th>
      <th>Tmax</th>
      <th>Date</th>
      <th>Tmin</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11111</td>
      <td>26.4</td>
      <td>1989-01-01</td>
      <td>14.7</td>
      <td>23.78</td>
      <td>90.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11111</td>
      <td>27.8</td>
      <td>1989-02-01</td>
      <td>11.6</td>
      <td>23.78</td>
      <td>90.39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11111</td>
      <td>33.0</td>
      <td>1989-03-01</td>
      <td>19.7</td>
      <td>23.78</td>
      <td>90.39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11111</td>
      <td>33.3</td>
      <td>1989-04-01</td>
      <td>22.3</td>
      <td>23.78</td>
      <td>90.39</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11111</td>
      <td>33.3</td>
      <td>1989-05-01</td>
      <td>24.4</td>
      <td>23.78</td>
      <td>90.39</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>350247</th>
      <td>11929</td>
      <td>34.0</td>
      <td>2019-05-31</td>
      <td>27.0</td>
      <td>20.87</td>
      <td>92.26</td>
    </tr>
    <tr>
      <th>350248</th>
      <td>11929</td>
      <td>31.2</td>
      <td>2019-07-31</td>
      <td>24.5</td>
      <td>20.87</td>
      <td>92.26</td>
    </tr>
    <tr>
      <th>350249</th>
      <td>11929</td>
      <td>32.8</td>
      <td>2019-08-31</td>
      <td>25.5</td>
      <td>20.87</td>
      <td>92.26</td>
    </tr>
    <tr>
      <th>350250</th>
      <td>11929</td>
      <td>32.5</td>
      <td>2019-10-31</td>
      <td>24.5</td>
      <td>20.87</td>
      <td>92.26</td>
    </tr>
    <tr>
      <th>350251</th>
      <td>11929</td>
      <td>28.6</td>
      <td>2019-12-31</td>
      <td>14.5</td>
      <td>20.87</td>
      <td>92.26</td>
    </tr>
  </tbody>
</table>
<p>350252 rows × 6 columns</p>
</div>




```python
BMD_temp_data["Date"] = pd.to_datetime(BMD_temp_data["Date"])
```


```python
era5_start = pd.to_datetime(ERA5_Land.valid_time.min().values)
era5_end   = pd.to_datetime(ERA5_Land.valid_time.max().values)

bmd_start = BMD_temp_data["Date"].min()
bmd_end   = BMD_temp_data["Date"].max()

start = max(era5_start, bmd_start)
end   = min(era5_end, bmd_end)

print("Overlap:", start, "to", end)
```

    Overlap: 1989-01-01 00:00:00 to 2019-12-31 00:00:00
    


```python
ERA5_Land = ERA5_Land.sel(valid_time = slice(start, end))
```


```python
BMD_temp_data = BMD_temp_data.query("Date >= @start and Date <= @end")
```

### Station Location


```python
ERA5_Land.valid_time
```




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
</style><pre class='xr-text-repr-fallback'>&lt;xarray.DataArray &#x27;valid_time&#x27; (valid_time: 11322)&gt; Size: 91kB
array([&#x27;1989-01-01T00:00:00.000000000&#x27;, &#x27;1989-01-02T00:00:00.000000000&#x27;,
       &#x27;1989-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-29T00:00:00.000000000&#x27;,
       &#x27;2019-12-30T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)
Coordinates:
    number      int64 8B ...
  * valid_time  (valid_time) datetime64[ns] 91kB 1989-01-01 ... 2019-12-31</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.DataArray</div><div class='xr-array-name'>'valid_time'</div><ul class='xr-dim-list'><li><span class='xr-has-index'>valid_time</span>: 11322</li></ul></div><ul class='xr-sections'><li class='xr-section-item'><div class='xr-array-wrap'><input id='section-7c3d4576-9d02-41d4-ac01-6ffedc9339b1' class='xr-array-in' type='checkbox' checked><label for='section-7c3d4576-9d02-41d4-ac01-6ffedc9339b1' title='Show/hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-array-preview xr-preview'><span>1989-01-01 1989-01-02 1989-01-03 ... 2019-12-29 2019-12-30 2019-12-31</span></div><div class='xr-array-data'><pre>array([&#x27;1989-01-01T00:00:00.000000000&#x27;, &#x27;1989-01-02T00:00:00.000000000&#x27;,
       &#x27;1989-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-29T00:00:00.000000000&#x27;,
       &#x27;2019-12-30T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></div></li><li class='xr-section-item'><input id='section-b1140b95-4f47-47d7-af18-08a4bb74f68d' class='xr-section-summary-in' type='checkbox'  checked><label for='section-b1140b95-4f47-47d7-af18-08a4bb74f68d' class='xr-section-summary' >Coordinates: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>number</span></div><div class='xr-var-dims'>()</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>...</div><input id='attrs-c0ddaf69-7792-4e0e-bd7f-450bfe22fc48' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-c0ddaf69-7792-4e0e-bd7f-450bfe22fc48' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-bff459ce-d16c-403d-804e-21ee286e9a76' class='xr-var-data-in' type='checkbox'><label for='data-bff459ce-d16c-403d-804e-21ee286e9a76' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>ensemble member numerical id</dd><dt><span>units :</span></dt><dd>1</dd><dt><span>standard_name :</span></dt><dd>realization</dd></dl></div><div class='xr-var-data'><pre>[1 values with dtype=int64]</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>valid_time</span></div><div class='xr-var-dims'>(valid_time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1989-01-01 ... 2019-12-31</div><input id='attrs-e14b84be-fa0d-4cc0-a52a-ab826489ba7b' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-e14b84be-fa0d-4cc0-a52a-ab826489ba7b' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-de9d3b83-5dea-4526-8d7e-3ed8a7a99e22' class='xr-var-data-in' type='checkbox'><label for='data-de9d3b83-5dea-4526-8d7e-3ed8a7a99e22' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([&#x27;1989-01-01T00:00:00.000000000&#x27;, &#x27;1989-01-02T00:00:00.000000000&#x27;,
       &#x27;1989-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-29T00:00:00.000000000&#x27;,
       &#x27;2019-12-30T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-728fd520-44d7-48af-8d76-f6733bb97019' class='xr-section-summary-in' type='checkbox'  ><label for='section-728fd520-44d7-48af-8d76-f6733bb97019' class='xr-section-summary' >Indexes: <span>(1)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-index-name'><div>valid_time</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-7b342374-7f67-42a8-9f0e-fb957d8041b4' class='xr-index-data-in' type='checkbox'/><label for='index-7b342374-7f67-42a8-9f0e-fb957d8041b4' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(DatetimeIndex([&#x27;1989-01-01&#x27;, &#x27;1989-01-02&#x27;, &#x27;1989-01-03&#x27;, &#x27;1989-01-04&#x27;,
               &#x27;1989-01-05&#x27;, &#x27;1989-01-06&#x27;, &#x27;1989-01-07&#x27;, &#x27;1989-01-08&#x27;,
               &#x27;1989-01-09&#x27;, &#x27;1989-01-10&#x27;,
               ...
               &#x27;2019-12-22&#x27;, &#x27;2019-12-23&#x27;, &#x27;2019-12-24&#x27;, &#x27;2019-12-25&#x27;,
               &#x27;2019-12-26&#x27;, &#x27;2019-12-27&#x27;, &#x27;2019-12-28&#x27;, &#x27;2019-12-29&#x27;,
               &#x27;2019-12-30&#x27;, &#x27;2019-12-31&#x27;],
              dtype=&#x27;datetime64[ns]&#x27;, name=&#x27;valid_time&#x27;, length=11322, freq=None))</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-228cf2fa-e12a-4d9c-82f5-548deb6da216' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-228cf2fa-e12a-4d9c-82f5-548deb6da216' class='xr-section-summary'  title='Expand/collapse section'>Attributes: <span>(0)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'></dl></div></li></ul></div></div>




```python
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
import cartopy.feature as cfeature

# ------------------------------------------
# 2. Select 1 day (example: 2005-06-15)
# ------------------------------------------
date = "2012-12-31T00:00:00.000000000"
tmax = ERA5_Land["t2m_max"].sel(valid_time=date)  # change variable name if needed

# ----------------------l--------------------
# 3. Clip the data to Bangladesh extent
# ------------------------------------------
bd_extent = {
    "lon_min": 88.0,
    "lon_max": 93.0,
    "lat_min": 20.5,
    "lat_max": 26.7
}


# ------------------------------------------
# 4. Plot map
# ------------------------------------------
plt.figure(figsize=(10, 8))
ax = plt.axes(projection=ccrs.PlateCarree())

# Plot temperature data
temp_plot = tmax.plot(
    ax=ax,
    transform=ccrs.PlateCarree(),
    cmap="coolwarm",
    cbar_kwargs={"label": "Daily Max Temperature (°C)"}
)

# Add borders and coastlines
ax.add_feature(cfeature.BORDERS, linewidth=1)
ax.add_feature(cfeature.COASTLINE, linewidth=1)

# Set map extent to Bangladesh
ax.set_extent([
    bd_extent["lon_min"],
    bd_extent["lon_max"],
    bd_extent["lat_min"],
    bd_extent["lat_max"]
], crs=ccrs.PlateCarree())

# ------------------------------------------
# 5. Add station locations
# ------------------------------------------

# Plot station points
ax.scatter(
    BMD_temp_data["Longitude"],
    BMD_temp_data["Latitude"],
    color="black",
    s= 5,
    marker="o",
    transform=ccrs.PlateCarree(),
    zorder=5,
    label="Stations"
)

lons = BMD_temp_data["Longitude"].values
lats = BMD_temp_data["Latitude"].values
ids = BMD_temp_data["Station_ID"].values

# # Faster annotation loop (zip is faster than iterrows)
# for lon, lat, sid in zip(lons, lats, ids):
#     ax.annotate(
#         sid,
#         xy=(lon, lat),
#         xytext=(3, 3),  # offset in points (better than adding 0.05 degrees)
#         textcoords="offset points",
#         fontsize=7,
#         transform=ccrs.PlateCarree(),
#         zorder=6
#     )

# Title
plt.title(f"ERA5-Land Daily Maximum Temperature (Clipped) — {date}")

plt.show()
```


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_14_0.png)
    


## Spatial Matching


```python
stations = pd.DataFrame({
    "station": BMD_temp_data["Station_ID"],
    "lat": BMD_temp_data["Latitude"],
    "lon": BMD_temp_data["Longitude"]
}).drop_duplicates().sort_values("station")

stations = stations.set_index("station")
```

### Bilinear Interpolation to match ERA5 Land with BMD


```python
ERA5_interpolated = ERA5_Land.interp(
    latitude = xr.DataArray(stations["lat"], dims="station"),
    longitude=xr.DataArray(stations["lon"], dims="station"),
    method="linear"
)
```


```python
ERA5_interpolated
```




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
</style><pre class='xr-text-repr-fallback'>&lt;xarray.Dataset&gt; Size: 3MB
Dimensions:     (valid_time: 11322, station: 31)
Coordinates:
    number      int64 8B ...
  * valid_time  (valid_time) datetime64[ns] 91kB 1989-01-01 ... 2019-12-31
    latitude    (station) float64 248B 25.63 25.72 24.35 ... 24.15 23.64 22.43
    longitude   (station) float64 248B 88.66 89.26 88.56 ... 89.55 88.84 89.66
  * station     (station) int64 248B 10120 10208 10320 ... 41909 41926 41958
Data variables:
    t2m_min     (valid_time, station) float32 1MB dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;
    t2m_max     (valid_time, station) float32 1MB dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.Dataset</div></div><ul class='xr-sections'><li class='xr-section-item'><input id='section-757db6a6-abe5-47b4-b64a-e9bf965d79cc' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-757db6a6-abe5-47b4-b64a-e9bf965d79cc' class='xr-section-summary'  title='Expand/collapse section'>Dimensions:</label><div class='xr-section-inline-details'><ul class='xr-dim-list'><li><span class='xr-has-index'>valid_time</span>: 11322</li><li><span class='xr-has-index'>station</span>: 31</li></ul></div><div class='xr-section-details'></div></li><li class='xr-section-item'><input id='section-1fc77a31-05b2-477d-b537-9255ab744fba' class='xr-section-summary-in' type='checkbox'  checked><label for='section-1fc77a31-05b2-477d-b537-9255ab744fba' class='xr-section-summary' >Coordinates: <span>(5)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>number</span></div><div class='xr-var-dims'>()</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>...</div><input id='attrs-c7c6ba73-7955-41ec-8b29-75b4e6013dcc' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-c7c6ba73-7955-41ec-8b29-75b4e6013dcc' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-26942b2b-36f2-4114-a934-8cf21ab3601a' class='xr-var-data-in' type='checkbox'><label for='data-26942b2b-36f2-4114-a934-8cf21ab3601a' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>ensemble member numerical id</dd><dt><span>units :</span></dt><dd>1</dd><dt><span>standard_name :</span></dt><dd>realization</dd></dl></div><div class='xr-var-data'><pre>[1 values with dtype=int64]</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>valid_time</span></div><div class='xr-var-dims'>(valid_time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1989-01-01 ... 2019-12-31</div><input id='attrs-ee24e6d5-6e6f-4479-935f-a1d2fed3629e' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-ee24e6d5-6e6f-4479-935f-a1d2fed3629e' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-89017a6c-ed4f-40cd-87ff-dc7d17d58cbc' class='xr-var-data-in' type='checkbox'><label for='data-89017a6c-ed4f-40cd-87ff-dc7d17d58cbc' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([&#x27;1989-01-01T00:00:00.000000000&#x27;, &#x27;1989-01-02T00:00:00.000000000&#x27;,
       &#x27;1989-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-29T00:00:00.000000000&#x27;,
       &#x27;2019-12-30T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span>latitude</span></div><div class='xr-var-dims'>(station)</div><div class='xr-var-dtype'>float64</div><div class='xr-var-preview xr-preview'>25.63 25.72 24.35 ... 23.64 22.43</div><input id='attrs-c0651208-ecaf-4436-8001-89ae4aaa3a88' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-c0651208-ecaf-4436-8001-89ae4aaa3a88' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-3ef764ef-c874-4ee9-8d1d-cc618dc05bdb' class='xr-var-data-in' type='checkbox'><label for='data-3ef764ef-c874-4ee9-8d1d-cc618dc05bdb' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([25.63, 25.72, 24.35, 24.88, 24.75, 24.88, 24.29, 24.12, 23.78,
       23.48, 23.26, 23.17, 23.61, 23.17, 22.8 , 22.68, 22.7 , 22.68,
       23.01, 22.83, 22.64, 21.83, 21.46, 20.87, 22.67, 22.36, 21.98,
       25.75, 24.15, 23.64, 22.43])</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span>longitude</span></div><div class='xr-var-dims'>(station)</div><div class='xr-var-dtype'>float64</div><div class='xr-var-preview xr-preview'>88.66 89.26 88.56 ... 88.84 89.66</div><input id='attrs-f4c04af5-85db-40dc-96e2-26e8bbb05dcc' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-f4c04af5-85db-40dc-96e2-26e8bbb05dcc' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-0114ee70-05e2-4284-995b-320689bfbf70' class='xr-var-data-in' type='checkbox'><label for='data-0114ee70-05e2-4284-995b-320689bfbf70' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([88.66, 89.26, 88.56, 89.36, 90.41, 91.93, 91.73, 89.04, 90.39,
       91.19, 90.67, 89.22, 89.84, 90.18, 89.58, 89.07, 90.38, 90.66,
       91.37, 91.08, 91.64, 91.84, 91.98, 92.26, 92.2 , 90.34, 90.22,
       88.92, 89.55, 88.84, 89.66])</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>station</span></div><div class='xr-var-dims'>(station)</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>10120 10208 10320 ... 41926 41958</div><input id='attrs-f2a0e099-f4e3-479d-8dd8-4401c55243ec' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-f2a0e099-f4e3-479d-8dd8-4401c55243ec' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-5a8a39ae-31be-4b28-bb29-432e767ec8d9' class='xr-var-data-in' type='checkbox'><label for='data-5a8a39ae-31be-4b28-bb29-432e767ec8d9' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([10120, 10208, 10320, 10408, 10609, 10705, 10724, 10910, 11111, 11313,
       11316, 11407, 11505, 11513, 11604, 11610, 11704, 11706, 11805, 11809,
       11912, 11925, 11927, 11929, 12007, 12103, 12110, 41858, 41909, 41926,
       41958], dtype=int64)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-1a9a3715-a2c8-4ffc-aa81-ee8ad58e189a' class='xr-section-summary-in' type='checkbox'  checked><label for='section-1a9a3715-a2c8-4ffc-aa81-ee8ad58e189a' class='xr-section-summary' >Data variables: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>t2m_min</span></div><div class='xr-var-dims'>(valid_time, station)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</div><input id='attrs-b2593d65-4cb0-4652-8d80-9c45c6821d0c' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-b2593d65-4cb0-4652-8d80-9c45c6821d0c' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-15e2efba-3866-48e6-97f7-a529d9207c75' class='xr-var-data-in' type='checkbox'><label for='data-15e2efba-3866-48e6-97f7-a529d9207c75' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily minimum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 1.34 MiB </td>
                        <td> 1.34 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (11322, 31) </td>
                        <td> (11322, 31) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 16 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="75" height="170" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="0" y1="0" x2="25" y2="0" style="stroke-width:2" />
  <line x1="0" y1="120" x2="25" y2="120" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="0" y1="0" x2="0" y2="120" style="stroke-width:2" />
  <line x1="25" y1="0" x2="25" y2="120" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="0.0,0.0 25.412616514582485,0.0 25.412616514582485,120.0 0.0,120.0" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="12.706308257291242" y="140.0" font-size="1.0rem" font-weight="100" text-anchor="middle" >31</text>
  <text x="45.41261651458248" y="60.0" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(-90,45.41261651458248,60.0)">11322</text>
</svg>
        </td>
    </tr>
</table></div></li><li class='xr-var-item'><div class='xr-var-name'><span>t2m_max</span></div><div class='xr-var-dims'>(valid_time, station)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</div><input id='attrs-d531bdb1-d136-4c28-8706-6810528d8385' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-d531bdb1-d136-4c28-8706-6810528d8385' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-dd756131-a175-4682-a723-03ee5491b29e' class='xr-var-data-in' type='checkbox'><label for='data-dd756131-a175-4682-a723-03ee5491b29e' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily maximum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 1.34 MiB </td>
                        <td> 1.34 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (11322, 31) </td>
                        <td> (11322, 31) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 16 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="75" height="170" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="0" y1="0" x2="25" y2="0" style="stroke-width:2" />
  <line x1="0" y1="120" x2="25" y2="120" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="0" y1="0" x2="0" y2="120" style="stroke-width:2" />
  <line x1="25" y1="0" x2="25" y2="120" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="0.0,0.0 25.412616514582485,0.0 25.412616514582485,120.0 0.0,120.0" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="12.706308257291242" y="140.0" font-size="1.0rem" font-weight="100" text-anchor="middle" >31</text>
  <text x="45.41261651458248" y="60.0" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(-90,45.41261651458248,60.0)">11322</text>
</svg>
        </td>
    </tr>
</table></div></li></ul></div></li><li class='xr-section-item'><input id='section-83854a90-8a1a-4a09-a67a-c5180a716ead' class='xr-section-summary-in' type='checkbox'  ><label for='section-83854a90-8a1a-4a09-a67a-c5180a716ead' class='xr-section-summary' >Indexes: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-index-name'><div>valid_time</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-374aa621-1b7a-4203-8062-c68ae5d53d2f' class='xr-index-data-in' type='checkbox'/><label for='index-374aa621-1b7a-4203-8062-c68ae5d53d2f' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(DatetimeIndex([&#x27;1989-01-01&#x27;, &#x27;1989-01-02&#x27;, &#x27;1989-01-03&#x27;, &#x27;1989-01-04&#x27;,
               &#x27;1989-01-05&#x27;, &#x27;1989-01-06&#x27;, &#x27;1989-01-07&#x27;, &#x27;1989-01-08&#x27;,
               &#x27;1989-01-09&#x27;, &#x27;1989-01-10&#x27;,
               ...
               &#x27;2019-12-22&#x27;, &#x27;2019-12-23&#x27;, &#x27;2019-12-24&#x27;, &#x27;2019-12-25&#x27;,
               &#x27;2019-12-26&#x27;, &#x27;2019-12-27&#x27;, &#x27;2019-12-28&#x27;, &#x27;2019-12-29&#x27;,
               &#x27;2019-12-30&#x27;, &#x27;2019-12-31&#x27;],
              dtype=&#x27;datetime64[ns]&#x27;, name=&#x27;valid_time&#x27;, length=11322, freq=None))</pre></div></li><li class='xr-var-item'><div class='xr-index-name'><div>station</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-2f3b7910-41af-49c0-bf18-a2b0b15686c6' class='xr-index-data-in' type='checkbox'/><label for='index-2f3b7910-41af-49c0-bf18-a2b0b15686c6' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(Index([10120, 10208, 10320, 10408, 10609, 10705, 10724, 10910, 11111, 11313,
       11316, 11407, 11505, 11513, 11604, 11610, 11704, 11706, 11805, 11809,
       11912, 11925, 11927, 11929, 12007, 12103, 12110, 41858, 41909, 41926,
       41958],
      dtype=&#x27;int64&#x27;, name=&#x27;station&#x27;))</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-6e030084-844c-4f8c-a58b-a5579590afd2' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-6e030084-844c-4f8c-a58b-a5579590afd2' class='xr-section-summary'  title='Expand/collapse section'>Attributes: <span>(0)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'></dl></div></li></ul></div></div>




```python
ERA5_interpolated_df = ERA5_interpolated.to_dataframe().reset_index().copy()
```


```python
ERA5_interpolated_df.query("station == 10724").isnull().sum()
```




    valid_time    0
    station       0
    number        0
    t2m_min       0
    t2m_max       0
    latitude      0
    longitude     0
    dtype: int64




```python
ERA5_interpolated_df.groupby("station").agg({
    't2m_min': ['min', 'max', 'mean', 'std'],
    't2m_max': ['min', 'max', 'mean', 'std']
}).sort_values("station")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">t2m_min</th>
      <th colspan="4" halign="left">t2m_max</th>
    </tr>
    <tr>
      <th></th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
    </tr>
    <tr>
      <th>station</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10120</th>
      <td>6.412379</td>
      <td>28.491783</td>
      <td>20.257843</td>
      <td>5.286250</td>
      <td>16.551578</td>
      <td>42.772448</td>
      <td>29.296266</td>
      <td>3.785527</td>
    </tr>
    <tr>
      <th>10208</th>
      <td>6.322086</td>
      <td>28.380123</td>
      <td>20.373954</td>
      <td>5.087419</td>
      <td>16.131735</td>
      <td>42.586959</td>
      <td>29.050219</td>
      <td>3.478245</td>
    </tr>
    <tr>
      <th>10320</th>
      <td>6.700494</td>
      <td>30.944928</td>
      <td>21.271502</td>
      <td>5.178701</td>
      <td>15.995563</td>
      <td>43.347028</td>
      <td>29.989999</td>
      <td>4.078047</td>
    </tr>
    <tr>
      <th>10408</th>
      <td>6.154918</td>
      <td>29.357701</td>
      <td>20.625156</td>
      <td>5.201029</td>
      <td>16.048512</td>
      <td>42.540719</td>
      <td>29.566232</td>
      <td>3.591045</td>
    </tr>
    <tr>
      <th>10609</th>
      <td>6.615167</td>
      <td>28.250275</td>
      <td>20.491554</td>
      <td>4.943889</td>
      <td>17.064716</td>
      <td>39.282672</td>
      <td>29.214862</td>
      <td>3.192209</td>
    </tr>
    <tr>
      <th>10705</th>
      <td>7.010919</td>
      <td>27.096500</td>
      <td>19.938147</td>
      <td>5.042058</td>
      <td>15.921823</td>
      <td>36.444723</td>
      <td>28.313082</td>
      <td>3.051478</td>
    </tr>
    <tr>
      <th>10724</th>
      <td>7.161569</td>
      <td>27.963370</td>
      <td>20.600480</td>
      <td>4.916576</td>
      <td>16.259147</td>
      <td>37.779030</td>
      <td>29.067945</td>
      <td>3.141100</td>
    </tr>
    <tr>
      <th>10910</th>
      <td>6.554049</td>
      <td>31.218561</td>
      <td>21.222470</td>
      <td>5.201077</td>
      <td>16.450416</td>
      <td>42.501608</td>
      <td>29.928881</td>
      <td>3.822689</td>
    </tr>
    <tr>
      <th>11111</th>
      <td>7.718297</td>
      <td>29.686793</td>
      <td>21.546357</td>
      <td>4.871126</td>
      <td>17.077047</td>
      <td>39.126959</td>
      <td>29.582719</td>
      <td>3.204785</td>
    </tr>
    <tr>
      <th>11313</th>
      <td>6.950573</td>
      <td>28.728336</td>
      <td>21.072713</td>
      <td>4.921459</td>
      <td>17.327682</td>
      <td>38.998668</td>
      <td>29.452167</td>
      <td>2.984413</td>
    </tr>
    <tr>
      <th>11316</th>
      <td>9.774635</td>
      <td>29.395602</td>
      <td>22.273267</td>
      <td>4.410081</td>
      <td>17.833815</td>
      <td>38.058146</td>
      <td>29.202964</td>
      <td>3.057549</td>
    </tr>
    <tr>
      <th>11407</th>
      <td>7.077291</td>
      <td>30.774073</td>
      <td>21.438167</td>
      <td>5.245564</td>
      <td>16.693766</td>
      <td>41.306920</td>
      <td>30.231537</td>
      <td>3.553976</td>
    </tr>
    <tr>
      <th>11505</th>
      <td>8.928385</td>
      <td>30.255504</td>
      <td>22.051437</td>
      <td>4.609079</td>
      <td>16.493546</td>
      <td>39.976578</td>
      <td>29.620647</td>
      <td>3.461003</td>
    </tr>
    <tr>
      <th>11513</th>
      <td>8.612526</td>
      <td>29.877614</td>
      <td>21.797809</td>
      <td>4.730350</td>
      <td>17.527203</td>
      <td>39.711149</td>
      <td>29.714050</td>
      <td>3.267853</td>
    </tr>
    <tr>
      <th>11604</th>
      <td>8.815924</td>
      <td>30.452545</td>
      <td>22.065483</td>
      <td>4.857384</td>
      <td>17.398102</td>
      <td>40.336383</td>
      <td>30.015319</td>
      <td>3.320520</td>
    </tr>
    <tr>
      <th>11610</th>
      <td>9.215221</td>
      <td>30.768600</td>
      <td>22.591497</td>
      <td>4.736520</td>
      <td>17.368649</td>
      <td>39.986505</td>
      <td>29.969724</td>
      <td>3.428891</td>
    </tr>
    <tr>
      <th>11704</th>
      <td>9.271344</td>
      <td>29.680182</td>
      <td>22.244039</td>
      <td>4.550566</td>
      <td>17.913727</td>
      <td>38.773688</td>
      <td>29.508578</td>
      <td>3.126911</td>
    </tr>
    <tr>
      <th>11706</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11805</th>
      <td>7.403014</td>
      <td>28.553590</td>
      <td>21.252864</td>
      <td>4.910786</td>
      <td>17.918053</td>
      <td>39.111979</td>
      <td>29.392524</td>
      <td>2.783592</td>
    </tr>
    <tr>
      <th>11809</th>
      <td>8.200573</td>
      <td>29.069928</td>
      <td>21.657615</td>
      <td>4.883584</td>
      <td>17.970065</td>
      <td>38.980914</td>
      <td>29.227233</td>
      <td>2.738281</td>
    </tr>
    <tr>
      <th>11912</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11925</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11927</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11929</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12007</th>
      <td>10.781818</td>
      <td>27.833893</td>
      <td>21.472983</td>
      <td>4.041542</td>
      <td>17.580621</td>
      <td>38.572223</td>
      <td>29.217029</td>
      <td>3.034111</td>
    </tr>
    <tr>
      <th>12103</th>
      <td>9.213492</td>
      <td>29.808073</td>
      <td>22.183727</td>
      <td>4.712824</td>
      <td>17.706227</td>
      <td>39.206989</td>
      <td>29.573670</td>
      <td>2.967243</td>
    </tr>
    <tr>
      <th>12110</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>41858</th>
      <td>6.183942</td>
      <td>28.256549</td>
      <td>20.259963</td>
      <td>5.156502</td>
      <td>16.273297</td>
      <td>42.776959</td>
      <td>29.128408</td>
      <td>3.599653</td>
    </tr>
    <tr>
      <th>41909</th>
      <td>7.383209</td>
      <td>30.576080</td>
      <td>21.373266</td>
      <td>5.030683</td>
      <td>16.713043</td>
      <td>41.350800</td>
      <td>29.707446</td>
      <td>3.597685</td>
    </tr>
    <tr>
      <th>41926</th>
      <td>6.560924</td>
      <td>31.327760</td>
      <td>21.306985</td>
      <td>5.249911</td>
      <td>15.735485</td>
      <td>42.600719</td>
      <td>30.132265</td>
      <td>3.895679</td>
    </tr>
    <tr>
      <th>41958</th>
      <td>9.880143</td>
      <td>30.354303</td>
      <td>22.474237</td>
      <td>4.517624</td>
      <td>17.658937</td>
      <td>39.786930</td>
      <td>29.724687</td>
      <td>3.264485</td>
    </tr>
  </tbody>
</table>
</div>



Missing values are only for coastal regions as bilinear interpolatin is picking null grid cells. (6 regions in total)

#### Using KDTree to bypass nearest null grid cells


```python
mask = ~ERA5_Land["t2m_min"].isel(valid_time = 0).isnull()

lats = ERA5_Land.latitude.values
lons = ERA5_Land.longitude.values

lon2d, lat2d = np.meshgrid(lons, lats)

valid_lats = lat2d[mask.values]
valid_lons = lon2d[mask.values]
```


```python
from scipy.spatial import cKDTree

coords = np.column_stack([valid_lats, valid_lons])
tree = cKDTree(coords)
```


```python
station_coords = np.column_stack([
    stations["lat"].values,
    stations["lon"].values
])

dist, idx = tree.query(station_coords)

nearest_lat = valid_lats[idx]
nearest_lon = valid_lons[idx]
```


```python
era_sel_valid = ERA5_Land.sel(
    latitude = xr.DataArray(nearest_lat, dims="station"),
    longitude = xr.DataArray(nearest_lon, dims="station"),
    method="nearest"
)
```

#### Using nearest neighbors where bilinear fails


```python
ERA5_final = ERA5_interpolated.where(~ERA5_interpolated.isnull(), era_sel_valid)
```


```python
ERA5_final
```




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
</style><pre class='xr-text-repr-fallback'>&lt;xarray.Dataset&gt; Size: 3MB
Dimensions:     (valid_time: 11322, station: 31)
Coordinates:
    number      int64 8B 0
  * valid_time  (valid_time) datetime64[ns] 91kB 1989-01-01 ... 2019-12-31
  * station     (station) int64 248B 10120 10208 10320 ... 41909 41926 41958
Data variables:
    t2m_min     (valid_time, station) float32 1MB dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;
    t2m_max     (valid_time, station) float32 1MB dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.Dataset</div></div><ul class='xr-sections'><li class='xr-section-item'><input id='section-459781ec-0815-4084-b4a9-b8343601c29e' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-459781ec-0815-4084-b4a9-b8343601c29e' class='xr-section-summary'  title='Expand/collapse section'>Dimensions:</label><div class='xr-section-inline-details'><ul class='xr-dim-list'><li><span class='xr-has-index'>valid_time</span>: 11322</li><li><span class='xr-has-index'>station</span>: 31</li></ul></div><div class='xr-section-details'></div></li><li class='xr-section-item'><input id='section-d92ff848-f2eb-4495-acd4-ec3f2c7959d1' class='xr-section-summary-in' type='checkbox'  checked><label for='section-d92ff848-f2eb-4495-acd4-ec3f2c7959d1' class='xr-section-summary' >Coordinates: <span>(3)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>number</span></div><div class='xr-var-dims'>()</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>0</div><input id='attrs-97d2bcc6-09f0-452b-b389-b095d1644151' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-97d2bcc6-09f0-452b-b389-b095d1644151' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-62274716-5564-43d5-92bd-f52d05f14aaa' class='xr-var-data-in' type='checkbox'><label for='data-62274716-5564-43d5-92bd-f52d05f14aaa' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>ensemble member numerical id</dd><dt><span>units :</span></dt><dd>1</dd><dt><span>standard_name :</span></dt><dd>realization</dd></dl></div><div class='xr-var-data'><pre>array(0, dtype=int64)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>valid_time</span></div><div class='xr-var-dims'>(valid_time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1989-01-01 ... 2019-12-31</div><input id='attrs-b7f34f6d-8b85-4d1e-8c72-63092af1695f' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-b7f34f6d-8b85-4d1e-8c72-63092af1695f' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-6fdedfe9-ca41-4b1f-806b-732815b07f3b' class='xr-var-data-in' type='checkbox'><label for='data-6fdedfe9-ca41-4b1f-806b-732815b07f3b' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([&#x27;1989-01-01T00:00:00.000000000&#x27;, &#x27;1989-01-02T00:00:00.000000000&#x27;,
       &#x27;1989-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-29T00:00:00.000000000&#x27;,
       &#x27;2019-12-30T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>station</span></div><div class='xr-var-dims'>(station)</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>10120 10208 10320 ... 41926 41958</div><input id='attrs-de91a153-511b-4378-a41c-0e0d133f17fd' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-de91a153-511b-4378-a41c-0e0d133f17fd' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-6db03b2e-fc59-4a99-987d-0174455a7f23' class='xr-var-data-in' type='checkbox'><label for='data-6db03b2e-fc59-4a99-987d-0174455a7f23' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([10120, 10208, 10320, 10408, 10609, 10705, 10724, 10910, 11111, 11313,
       11316, 11407, 11505, 11513, 11604, 11610, 11704, 11706, 11805, 11809,
       11912, 11925, 11927, 11929, 12007, 12103, 12110, 41858, 41909, 41926,
       41958], dtype=int64)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-d7ff1b6f-72cb-4c87-b9f5-5b95818e3249' class='xr-section-summary-in' type='checkbox'  checked><label for='section-d7ff1b6f-72cb-4c87-b9f5-5b95818e3249' class='xr-section-summary' >Data variables: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>t2m_min</span></div><div class='xr-var-dims'>(valid_time, station)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</div><input id='attrs-bd2c8534-2c44-4193-9e03-9f08b6a35c29' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-bd2c8534-2c44-4193-9e03-9f08b6a35c29' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-53eb9ca9-9f77-4744-8dd3-3ddcddba2eed' class='xr-var-data-in' type='checkbox'><label for='data-53eb9ca9-9f77-4744-8dd3-3ddcddba2eed' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily minimum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 1.34 MiB </td>
                        <td> 1.34 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (11322, 31) </td>
                        <td> (11322, 31) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 21 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="75" height="170" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="0" y1="0" x2="25" y2="0" style="stroke-width:2" />
  <line x1="0" y1="120" x2="25" y2="120" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="0" y1="0" x2="0" y2="120" style="stroke-width:2" />
  <line x1="25" y1="0" x2="25" y2="120" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="0.0,0.0 25.412616514582485,0.0 25.412616514582485,120.0 0.0,120.0" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="12.706308257291242" y="140.0" font-size="1.0rem" font-weight="100" text-anchor="middle" >31</text>
  <text x="45.41261651458248" y="60.0" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(-90,45.41261651458248,60.0)">11322</text>
</svg>
        </td>
    </tr>
</table></div></li><li class='xr-var-item'><div class='xr-var-name'><span>t2m_max</span></div><div class='xr-var-dims'>(valid_time, station)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</div><input id='attrs-991a24c2-86e5-40e7-8bb3-603de174e5d0' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-991a24c2-86e5-40e7-8bb3-603de174e5d0' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-c139f511-88cd-4533-a689-79a947a4e7e0' class='xr-var-data-in' type='checkbox'><label for='data-c139f511-88cd-4533-a689-79a947a4e7e0' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily maximum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 1.34 MiB </td>
                        <td> 1.34 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (11322, 31) </td>
                        <td> (11322, 31) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 21 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="75" height="170" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="0" y1="0" x2="25" y2="0" style="stroke-width:2" />
  <line x1="0" y1="120" x2="25" y2="120" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="0" y1="0" x2="0" y2="120" style="stroke-width:2" />
  <line x1="25" y1="0" x2="25" y2="120" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="0.0,0.0 25.412616514582485,0.0 25.412616514582485,120.0 0.0,120.0" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="12.706308257291242" y="140.0" font-size="1.0rem" font-weight="100" text-anchor="middle" >31</text>
  <text x="45.41261651458248" y="60.0" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(-90,45.41261651458248,60.0)">11322</text>
</svg>
        </td>
    </tr>
</table></div></li></ul></div></li><li class='xr-section-item'><input id='section-cf435300-0e67-4661-bac9-35705b75f9a4' class='xr-section-summary-in' type='checkbox'  ><label for='section-cf435300-0e67-4661-bac9-35705b75f9a4' class='xr-section-summary' >Indexes: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-index-name'><div>valid_time</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-682b704c-b416-4349-b4df-dda259247f14' class='xr-index-data-in' type='checkbox'/><label for='index-682b704c-b416-4349-b4df-dda259247f14' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(DatetimeIndex([&#x27;1989-01-01&#x27;, &#x27;1989-01-02&#x27;, &#x27;1989-01-03&#x27;, &#x27;1989-01-04&#x27;,
               &#x27;1989-01-05&#x27;, &#x27;1989-01-06&#x27;, &#x27;1989-01-07&#x27;, &#x27;1989-01-08&#x27;,
               &#x27;1989-01-09&#x27;, &#x27;1989-01-10&#x27;,
               ...
               &#x27;2019-12-22&#x27;, &#x27;2019-12-23&#x27;, &#x27;2019-12-24&#x27;, &#x27;2019-12-25&#x27;,
               &#x27;2019-12-26&#x27;, &#x27;2019-12-27&#x27;, &#x27;2019-12-28&#x27;, &#x27;2019-12-29&#x27;,
               &#x27;2019-12-30&#x27;, &#x27;2019-12-31&#x27;],
              dtype=&#x27;datetime64[ns]&#x27;, name=&#x27;valid_time&#x27;, length=11322, freq=None))</pre></div></li><li class='xr-var-item'><div class='xr-index-name'><div>station</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-f4ac3579-7b92-41c4-a9cd-822e07645437' class='xr-index-data-in' type='checkbox'/><label for='index-f4ac3579-7b92-41c4-a9cd-822e07645437' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(Index([10120, 10208, 10320, 10408, 10609, 10705, 10724, 10910, 11111, 11313,
       11316, 11407, 11505, 11513, 11604, 11610, 11704, 11706, 11805, 11809,
       11912, 11925, 11927, 11929, 12007, 12103, 12110, 41858, 41909, 41926,
       41958],
      dtype=&#x27;int64&#x27;, name=&#x27;station&#x27;))</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-49684e0f-20cb-4597-9d04-4922a084a737' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-49684e0f-20cb-4597-9d04-4922a084a737' class='xr-section-summary'  title='Expand/collapse section'>Attributes: <span>(0)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'></dl></div></li></ul></div></div>



Bilinear Interpolation was failing for more than 12 stations because of missing grid cells. Moreover, for nearest neighbors six stations were giving negative values due to nearest neighbor being a null grid cell. KDTree is utilized to select nearest non-negative cells.

## Validation of the ERA5 Land

#### Station wise min-max temperature.


```python
ERA5_final.to_dataframe().reset_index().groupby("station").agg({
    't2m_min': ['min', 'max', 'mean', 'std'],
    't2m_max': ['min', 'max', 'mean', 'std']
}).sort_values("station")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">t2m_min</th>
      <th colspan="4" halign="left">t2m_max</th>
    </tr>
    <tr>
      <th></th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
    </tr>
    <tr>
      <th>station</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10120</th>
      <td>6.412379</td>
      <td>28.491783</td>
      <td>20.257843</td>
      <td>5.286250</td>
      <td>16.551578</td>
      <td>42.772448</td>
      <td>29.296266</td>
      <td>3.785527</td>
    </tr>
    <tr>
      <th>10208</th>
      <td>6.322086</td>
      <td>28.380123</td>
      <td>20.373954</td>
      <td>5.087419</td>
      <td>16.131735</td>
      <td>42.586959</td>
      <td>29.050219</td>
      <td>3.478245</td>
    </tr>
    <tr>
      <th>10320</th>
      <td>6.700494</td>
      <td>30.944928</td>
      <td>21.271502</td>
      <td>5.178701</td>
      <td>15.995563</td>
      <td>43.347028</td>
      <td>29.989999</td>
      <td>4.078047</td>
    </tr>
    <tr>
      <th>10408</th>
      <td>6.154918</td>
      <td>29.357701</td>
      <td>20.625156</td>
      <td>5.201029</td>
      <td>16.048512</td>
      <td>42.540719</td>
      <td>29.566232</td>
      <td>3.591045</td>
    </tr>
    <tr>
      <th>10609</th>
      <td>6.615167</td>
      <td>28.250275</td>
      <td>20.491554</td>
      <td>4.943889</td>
      <td>17.064716</td>
      <td>39.282672</td>
      <td>29.214862</td>
      <td>3.192209</td>
    </tr>
    <tr>
      <th>10705</th>
      <td>7.010919</td>
      <td>27.096500</td>
      <td>19.938147</td>
      <td>5.042058</td>
      <td>15.921823</td>
      <td>36.444723</td>
      <td>28.313082</td>
      <td>3.051478</td>
    </tr>
    <tr>
      <th>10724</th>
      <td>7.161569</td>
      <td>27.963370</td>
      <td>20.600480</td>
      <td>4.916576</td>
      <td>16.259147</td>
      <td>37.779030</td>
      <td>29.067945</td>
      <td>3.141100</td>
    </tr>
    <tr>
      <th>10910</th>
      <td>6.554049</td>
      <td>31.218561</td>
      <td>21.222470</td>
      <td>5.201077</td>
      <td>16.450416</td>
      <td>42.501608</td>
      <td>29.928881</td>
      <td>3.822689</td>
    </tr>
    <tr>
      <th>11111</th>
      <td>7.718297</td>
      <td>29.686793</td>
      <td>21.546357</td>
      <td>4.871126</td>
      <td>17.077047</td>
      <td>39.126959</td>
      <td>29.582719</td>
      <td>3.204785</td>
    </tr>
    <tr>
      <th>11313</th>
      <td>6.950573</td>
      <td>28.728336</td>
      <td>21.072713</td>
      <td>4.921459</td>
      <td>17.327682</td>
      <td>38.998668</td>
      <td>29.452167</td>
      <td>2.984413</td>
    </tr>
    <tr>
      <th>11316</th>
      <td>9.774635</td>
      <td>29.395602</td>
      <td>22.273267</td>
      <td>4.410081</td>
      <td>17.833815</td>
      <td>38.058146</td>
      <td>29.202964</td>
      <td>3.057549</td>
    </tr>
    <tr>
      <th>11407</th>
      <td>7.077291</td>
      <td>30.774073</td>
      <td>21.438167</td>
      <td>5.245564</td>
      <td>16.693766</td>
      <td>41.306920</td>
      <td>30.231537</td>
      <td>3.553976</td>
    </tr>
    <tr>
      <th>11505</th>
      <td>8.928385</td>
      <td>30.255504</td>
      <td>22.051437</td>
      <td>4.609079</td>
      <td>16.493546</td>
      <td>39.976578</td>
      <td>29.620647</td>
      <td>3.461003</td>
    </tr>
    <tr>
      <th>11513</th>
      <td>8.612526</td>
      <td>29.877614</td>
      <td>21.797809</td>
      <td>4.730350</td>
      <td>17.527203</td>
      <td>39.711149</td>
      <td>29.714050</td>
      <td>3.267853</td>
    </tr>
    <tr>
      <th>11604</th>
      <td>8.815924</td>
      <td>30.452545</td>
      <td>22.065483</td>
      <td>4.857384</td>
      <td>17.398102</td>
      <td>40.336383</td>
      <td>30.015319</td>
      <td>3.320520</td>
    </tr>
    <tr>
      <th>11610</th>
      <td>9.215221</td>
      <td>30.768600</td>
      <td>22.591497</td>
      <td>4.736520</td>
      <td>17.368649</td>
      <td>39.986505</td>
      <td>29.969724</td>
      <td>3.428891</td>
    </tr>
    <tr>
      <th>11704</th>
      <td>9.271344</td>
      <td>29.680182</td>
      <td>22.244039</td>
      <td>4.550566</td>
      <td>17.913727</td>
      <td>38.773688</td>
      <td>29.508578</td>
      <td>3.126911</td>
    </tr>
    <tr>
      <th>11706</th>
      <td>10.488922</td>
      <td>29.530182</td>
      <td>22.794556</td>
      <td>4.221715</td>
      <td>18.256989</td>
      <td>38.422516</td>
      <td>29.036763</td>
      <td>2.969537</td>
    </tr>
    <tr>
      <th>11805</th>
      <td>7.403014</td>
      <td>28.553590</td>
      <td>21.252864</td>
      <td>4.910786</td>
      <td>17.918053</td>
      <td>39.111979</td>
      <td>29.392524</td>
      <td>2.783592</td>
    </tr>
    <tr>
      <th>11809</th>
      <td>8.200573</td>
      <td>29.069928</td>
      <td>21.657615</td>
      <td>4.883584</td>
      <td>17.970065</td>
      <td>38.980914</td>
      <td>29.227233</td>
      <td>2.738281</td>
    </tr>
    <tr>
      <th>11912</th>
      <td>12.255768</td>
      <td>28.853668</td>
      <td>22.574561</td>
      <td>3.789379</td>
      <td>17.785553</td>
      <td>38.077301</td>
      <td>28.306954</td>
      <td>2.480430</td>
    </tr>
    <tr>
      <th>11925</th>
      <td>12.271637</td>
      <td>28.850250</td>
      <td>22.944027</td>
      <td>3.486472</td>
      <td>19.248199</td>
      <td>34.793365</td>
      <td>27.767918</td>
      <td>2.476537</td>
    </tr>
    <tr>
      <th>11927</th>
      <td>11.933258</td>
      <td>28.517731</td>
      <td>22.767665</td>
      <td>3.395087</td>
      <td>19.673737</td>
      <td>35.697662</td>
      <td>28.224306</td>
      <td>2.491416</td>
    </tr>
    <tr>
      <th>11929</th>
      <td>13.353180</td>
      <td>28.346100</td>
      <td>22.840709</td>
      <td>3.212529</td>
      <td>20.769684</td>
      <td>36.162506</td>
      <td>28.431334</td>
      <td>2.156101</td>
    </tr>
    <tr>
      <th>12007</th>
      <td>10.781818</td>
      <td>27.833893</td>
      <td>21.472983</td>
      <td>4.041542</td>
      <td>17.580621</td>
      <td>38.572223</td>
      <td>29.217029</td>
      <td>3.034111</td>
    </tr>
    <tr>
      <th>12103</th>
      <td>9.213492</td>
      <td>29.808073</td>
      <td>22.183727</td>
      <td>4.712824</td>
      <td>17.706227</td>
      <td>39.206989</td>
      <td>29.573670</td>
      <td>2.967243</td>
    </tr>
    <tr>
      <th>12110</th>
      <td>12.133453</td>
      <td>30.245026</td>
      <td>23.475727</td>
      <td>4.092068</td>
      <td>18.591461</td>
      <td>37.176666</td>
      <td>28.696625</td>
      <td>2.544665</td>
    </tr>
    <tr>
      <th>41858</th>
      <td>6.183942</td>
      <td>28.256549</td>
      <td>20.259963</td>
      <td>5.156502</td>
      <td>16.273297</td>
      <td>42.776959</td>
      <td>29.128408</td>
      <td>3.599653</td>
    </tr>
    <tr>
      <th>41909</th>
      <td>7.383209</td>
      <td>30.576080</td>
      <td>21.373266</td>
      <td>5.030683</td>
      <td>16.713043</td>
      <td>41.350800</td>
      <td>29.707446</td>
      <td>3.597685</td>
    </tr>
    <tr>
      <th>41926</th>
      <td>6.560924</td>
      <td>31.327760</td>
      <td>21.306985</td>
      <td>5.249911</td>
      <td>15.735485</td>
      <td>42.600719</td>
      <td>30.132265</td>
      <td>3.895679</td>
    </tr>
    <tr>
      <th>41958</th>
      <td>9.880143</td>
      <td>30.354303</td>
      <td>22.474237</td>
      <td>4.517624</td>
      <td>17.658937</td>
      <td>39.786930</td>
      <td>29.724687</td>
      <td>3.264485</td>
    </tr>
  </tbody>
</table>
</div>




```python
BMD_temp_data.groupby("Station_ID").agg({
    'Tmin': ['min', 'max', 'mean', 'std'],
    'Tmax': ['min', 'max', 'mean', 'std']
}).sort_values("Station_ID")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="4" halign="left">Tmin</th>
      <th colspan="4" halign="left">Tmax</th>
    </tr>
    <tr>
      <th></th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
    </tr>
    <tr>
      <th>Station_ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10120</th>
      <td>3.2</td>
      <td>29.8</td>
      <td>20.165044</td>
      <td>5.959467</td>
      <td>11.0</td>
      <td>41.4</td>
      <td>30.143516</td>
      <td>4.190926</td>
    </tr>
    <tr>
      <th>10208</th>
      <td>3.5</td>
      <td>30.5</td>
      <td>20.383087</td>
      <td>5.655361</td>
      <td>10.9</td>
      <td>39.8</td>
      <td>29.710768</td>
      <td>3.934541</td>
    </tr>
    <tr>
      <th>10320</th>
      <td>3.4</td>
      <td>30.2</td>
      <td>20.585100</td>
      <td>6.100116</td>
      <td>12.6</td>
      <td>43.7</td>
      <td>31.368947</td>
      <td>4.462741</td>
    </tr>
    <tr>
      <th>10408</th>
      <td>4.5</td>
      <td>30.0</td>
      <td>21.137493</td>
      <td>5.538622</td>
      <td>11.0</td>
      <td>44.0</td>
      <td>30.812219</td>
      <td>3.827229</td>
    </tr>
    <tr>
      <th>10609</th>
      <td>4.7</td>
      <td>30.6</td>
      <td>20.929267</td>
      <td>5.443022</td>
      <td>12.7</td>
      <td>38.1</td>
      <td>29.930125</td>
      <td>3.484783</td>
    </tr>
    <tr>
      <th>10705</th>
      <td>3.4</td>
      <td>29.4</td>
      <td>20.813694</td>
      <td>4.650099</td>
      <td>15.0</td>
      <td>39.6</td>
      <td>30.398621</td>
      <td>3.413802</td>
    </tr>
    <tr>
      <th>10724</th>
      <td>4.0</td>
      <td>29.0</td>
      <td>19.584097</td>
      <td>5.948212</td>
      <td>15.0</td>
      <td>39.2</td>
      <td>30.676571</td>
      <td>3.481706</td>
    </tr>
    <tr>
      <th>10910</th>
      <td>3.9</td>
      <td>31.0</td>
      <td>20.648286</td>
      <td>6.113454</td>
      <td>13.5</td>
      <td>43.0</td>
      <td>31.154891</td>
      <td>4.265283</td>
    </tr>
    <tr>
      <th>11111</th>
      <td>6.5</td>
      <td>30.3</td>
      <td>22.032806</td>
      <td>5.058577</td>
      <td>13.4</td>
      <td>40.2</td>
      <td>30.873182</td>
      <td>3.622845</td>
    </tr>
    <tr>
      <th>11313</th>
      <td>5.3</td>
      <td>30.2</td>
      <td>21.138808</td>
      <td>5.210189</td>
      <td>15.2</td>
      <td>39.2</td>
      <td>30.405040</td>
      <td>3.297922</td>
    </tr>
    <tr>
      <th>11316</th>
      <td>7.2</td>
      <td>29.7</td>
      <td>22.083627</td>
      <td>4.793834</td>
      <td>15.0</td>
      <td>40.0</td>
      <td>30.713029</td>
      <td>3.488855</td>
    </tr>
    <tr>
      <th>11407</th>
      <td>4.2</td>
      <td>30.0</td>
      <td>20.982325</td>
      <td>5.922744</td>
      <td>13.6</td>
      <td>43.2</td>
      <td>31.906020</td>
      <td>3.938520</td>
    </tr>
    <tr>
      <th>11505</th>
      <td>5.6</td>
      <td>30.0</td>
      <td>21.420237</td>
      <td>5.369222</td>
      <td>13.3</td>
      <td>41.2</td>
      <td>30.844090</td>
      <td>3.802004</td>
    </tr>
    <tr>
      <th>11513</th>
      <td>6.0</td>
      <td>29.5</td>
      <td>21.484272</td>
      <td>5.400612</td>
      <td>14.5</td>
      <td>39.7</td>
      <td>31.025556</td>
      <td>3.523218</td>
    </tr>
    <tr>
      <th>11604</th>
      <td>6.4</td>
      <td>30.0</td>
      <td>21.904400</td>
      <td>5.391311</td>
      <td>13.6</td>
      <td>40.7</td>
      <td>31.419321</td>
      <td>3.707221</td>
    </tr>
    <tr>
      <th>11610</th>
      <td>5.5</td>
      <td>31.3</td>
      <td>21.694822</td>
      <td>5.639526</td>
      <td>13.5</td>
      <td>43.4</td>
      <td>31.391827</td>
      <td>3.715452</td>
    </tr>
    <tr>
      <th>11704</th>
      <td>6.5</td>
      <td>29.8</td>
      <td>21.445988</td>
      <td>5.428201</td>
      <td>15.8</td>
      <td>39.4</td>
      <td>30.821382</td>
      <td>3.236582</td>
    </tr>
    <tr>
      <th>11706</th>
      <td>7.2</td>
      <td>30.4</td>
      <td>21.745178</td>
      <td>5.254986</td>
      <td>15.2</td>
      <td>38.9</td>
      <td>30.569686</td>
      <td>3.069304</td>
    </tr>
    <tr>
      <th>11805</th>
      <td>6.1</td>
      <td>30.0</td>
      <td>21.320725</td>
      <td>4.962469</td>
      <td>16.3</td>
      <td>39.4</td>
      <td>30.422788</td>
      <td>3.081824</td>
    </tr>
    <tr>
      <th>11809</th>
      <td>8.5</td>
      <td>29.8</td>
      <td>22.296520</td>
      <td>4.638249</td>
      <td>15.5</td>
      <td>39.3</td>
      <td>30.493828</td>
      <td>3.386917</td>
    </tr>
    <tr>
      <th>11912</th>
      <td>5.7</td>
      <td>31.0</td>
      <td>20.995132</td>
      <td>5.427792</td>
      <td>17.2</td>
      <td>40.2</td>
      <td>30.964749</td>
      <td>2.813139</td>
    </tr>
    <tr>
      <th>11925</th>
      <td>10.0</td>
      <td>32.0</td>
      <td>22.354721</td>
      <td>4.252070</td>
      <td>18.2</td>
      <td>38.5</td>
      <td>30.093878</td>
      <td>2.704971</td>
    </tr>
    <tr>
      <th>11927</th>
      <td>10.3</td>
      <td>31.0</td>
      <td>22.458922</td>
      <td>3.959521</td>
      <td>19.7</td>
      <td>39.5</td>
      <td>30.925062</td>
      <td>2.563048</td>
    </tr>
    <tr>
      <th>11929</th>
      <td>9.7</td>
      <td>29.5</td>
      <td>22.173823</td>
      <td>4.271971</td>
      <td>21.0</td>
      <td>38.0</td>
      <td>30.429290</td>
      <td>2.242611</td>
    </tr>
    <tr>
      <th>12007</th>
      <td>5.5</td>
      <td>28.8</td>
      <td>20.866150</td>
      <td>4.763227</td>
      <td>16.5</td>
      <td>41.1</td>
      <td>30.957360</td>
      <td>3.275935</td>
    </tr>
    <tr>
      <th>12103</th>
      <td>7.4</td>
      <td>30.0</td>
      <td>22.067839</td>
      <td>4.974604</td>
      <td>15.4</td>
      <td>39.5</td>
      <td>30.876540</td>
      <td>3.233258</td>
    </tr>
    <tr>
      <th>12110</th>
      <td>7.7</td>
      <td>30.4</td>
      <td>22.223292</td>
      <td>5.046664</td>
      <td>15.6</td>
      <td>40.0</td>
      <td>30.619346</td>
      <td>2.907762</td>
    </tr>
    <tr>
      <th>41858</th>
      <td>2.9</td>
      <td>31.0</td>
      <td>20.219003</td>
      <td>5.760257</td>
      <td>11.6</td>
      <td>41.0</td>
      <td>30.112208</td>
      <td>4.101184</td>
    </tr>
    <tr>
      <th>41909</th>
      <td>5.1</td>
      <td>31.0</td>
      <td>20.883697</td>
      <td>5.577681</td>
      <td>13.5</td>
      <td>40.5</td>
      <td>30.678590</td>
      <td>3.928976</td>
    </tr>
    <tr>
      <th>41926</th>
      <td>3.9</td>
      <td>30.0</td>
      <td>20.878134</td>
      <td>6.053535</td>
      <td>12.5</td>
      <td>43.5</td>
      <td>31.610638</td>
      <td>4.298561</td>
    </tr>
    <tr>
      <th>41958</th>
      <td>7.2</td>
      <td>30.5</td>
      <td>22.533336</td>
      <td>4.819382</td>
      <td>14.8</td>
      <td>40.5</td>
      <td>31.127363</td>
      <td>3.602428</td>
    </tr>
  </tbody>
</table>
</div>



After observing the above statistics, I can say that there is a warm-bias in ERA5.

##### Time series Plot ERA5 VS Observational data


```python
ERA5_final
```




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
</style><pre class='xr-text-repr-fallback'>&lt;xarray.Dataset&gt; Size: 3MB
Dimensions:     (valid_time: 11322, station: 31)
Coordinates:
    number      int64 8B 0
  * valid_time  (valid_time) datetime64[ns] 91kB 1989-01-01 ... 2019-12-31
  * station     (station) int64 248B 10120 10208 10320 ... 41909 41926 41958
Data variables:
    t2m_min     (valid_time, station) float32 1MB dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;
    t2m_max     (valid_time, station) float32 1MB dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.Dataset</div></div><ul class='xr-sections'><li class='xr-section-item'><input id='section-2d0b82cc-22b2-4349-949f-da7a1c63f610' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-2d0b82cc-22b2-4349-949f-da7a1c63f610' class='xr-section-summary'  title='Expand/collapse section'>Dimensions:</label><div class='xr-section-inline-details'><ul class='xr-dim-list'><li><span class='xr-has-index'>valid_time</span>: 11322</li><li><span class='xr-has-index'>station</span>: 31</li></ul></div><div class='xr-section-details'></div></li><li class='xr-section-item'><input id='section-92f2dcca-f8d3-4bc2-95be-abb2b5903f77' class='xr-section-summary-in' type='checkbox'  checked><label for='section-92f2dcca-f8d3-4bc2-95be-abb2b5903f77' class='xr-section-summary' >Coordinates: <span>(3)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>number</span></div><div class='xr-var-dims'>()</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>0</div><input id='attrs-d3bfa6b9-56ba-4c8e-9a6a-41b874f5ccda' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-d3bfa6b9-56ba-4c8e-9a6a-41b874f5ccda' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-0e2094f0-69f7-4bb6-9303-5738a4f75309' class='xr-var-data-in' type='checkbox'><label for='data-0e2094f0-69f7-4bb6-9303-5738a4f75309' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>ensemble member numerical id</dd><dt><span>units :</span></dt><dd>1</dd><dt><span>standard_name :</span></dt><dd>realization</dd></dl></div><div class='xr-var-data'><pre>array(0, dtype=int64)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>valid_time</span></div><div class='xr-var-dims'>(valid_time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1989-01-01 ... 2019-12-31</div><input id='attrs-3ddd6741-399d-44a0-963a-e3b6cdc116b0' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-3ddd6741-399d-44a0-963a-e3b6cdc116b0' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-7f52b916-d816-431a-b9c8-b2dd8e07abb5' class='xr-var-data-in' type='checkbox'><label for='data-7f52b916-d816-431a-b9c8-b2dd8e07abb5' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([&#x27;1989-01-01T00:00:00.000000000&#x27;, &#x27;1989-01-02T00:00:00.000000000&#x27;,
       &#x27;1989-01-03T00:00:00.000000000&#x27;, ..., &#x27;2019-12-29T00:00:00.000000000&#x27;,
       &#x27;2019-12-30T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>station</span></div><div class='xr-var-dims'>(station)</div><div class='xr-var-dtype'>int64</div><div class='xr-var-preview xr-preview'>10120 10208 10320 ... 41926 41958</div><input id='attrs-923ecb8c-5f04-43a3-a7a8-a0d067f50761' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-923ecb8c-5f04-43a3-a7a8-a0d067f50761' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-b5cb1efd-63b6-41e0-85e7-0ccb5c7347a2' class='xr-var-data-in' type='checkbox'><label for='data-b5cb1efd-63b6-41e0-85e7-0ccb5c7347a2' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([10120, 10208, 10320, 10408, 10609, 10705, 10724, 10910, 11111, 11313,
       11316, 11407, 11505, 11513, 11604, 11610, 11704, 11706, 11805, 11809,
       11912, 11925, 11927, 11929, 12007, 12103, 12110, 41858, 41909, 41926,
       41958], dtype=int64)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-d24c7503-0a32-4e08-a4e2-a0e153ced131' class='xr-section-summary-in' type='checkbox'  checked><label for='section-d24c7503-0a32-4e08-a4e2-a0e153ced131' class='xr-section-summary' >Data variables: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>t2m_min</span></div><div class='xr-var-dims'>(valid_time, station)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</div><input id='attrs-02e188d2-594a-41c6-866a-1ffa7741e20b' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-02e188d2-594a-41c6-866a-1ffa7741e20b' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-871108c7-6143-4b4a-945f-3843f7de0392' class='xr-var-data-in' type='checkbox'><label for='data-871108c7-6143-4b4a-945f-3843f7de0392' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily minimum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 1.34 MiB </td>
                        <td> 1.34 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (11322, 31) </td>
                        <td> (11322, 31) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 21 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="75" height="170" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="0" y1="0" x2="25" y2="0" style="stroke-width:2" />
  <line x1="0" y1="120" x2="25" y2="120" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="0" y1="0" x2="0" y2="120" style="stroke-width:2" />
  <line x1="25" y1="0" x2="25" y2="120" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="0.0,0.0 25.412616514582485,0.0 25.412616514582485,120.0 0.0,120.0" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="12.706308257291242" y="140.0" font-size="1.0rem" font-weight="100" text-anchor="middle" >31</text>
  <text x="45.41261651458248" y="60.0" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(-90,45.41261651458248,60.0)">11322</text>
</svg>
        </td>
    </tr>
</table></div></li><li class='xr-var-item'><div class='xr-var-name'><span>t2m_max</span></div><div class='xr-var-dims'>(valid_time, station)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>dask.array&lt;chunksize=(11322, 31), meta=np.ndarray&gt;</div><input id='attrs-757c0a34-a564-4ee2-9002-30245cca77b4' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-757c0a34-a564-4ee2-9002-30245cca77b4' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-385b6314-1e9c-4ee6-b1f0-9687066dbc7c' class='xr-var-data-in' type='checkbox'><label for='data-385b6314-1e9c-4ee6-b1f0-9687066dbc7c' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>GRIB_paramId :</span></dt><dd>167</dd><dt><span>GRIB_dataType :</span></dt><dd>fc</dd><dt><span>GRIB_numberOfPoints :</span></dt><dd>3055</dd><dt><span>GRIB_typeOfLevel :</span></dt><dd>surface</dd><dt><span>GRIB_stepUnits :</span></dt><dd>1</dd><dt><span>GRIB_stepType :</span></dt><dd>instant</dd><dt><span>GRIB_gridType :</span></dt><dd>regular_ll</dd><dt><span>GRIB_uvRelativeToGrid :</span></dt><dd>0</dd><dt><span>GRIB_NV :</span></dt><dd>0</dd><dt><span>GRIB_Nx :</span></dt><dd>47</dd><dt><span>GRIB_Ny :</span></dt><dd>65</dd><dt><span>GRIB_cfName :</span></dt><dd>unknown</dd><dt><span>GRIB_cfVarName :</span></dt><dd>t2m</dd><dt><span>GRIB_gridDefinitionDescription :</span></dt><dd>Latitude/Longitude Grid</dd><dt><span>GRIB_iDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_iScansNegatively :</span></dt><dd>0</dd><dt><span>GRIB_jDirectionIncrementInDegrees :</span></dt><dd>0.1</dd><dt><span>GRIB_jPointsAreConsecutive :</span></dt><dd>0</dd><dt><span>GRIB_jScansPositively :</span></dt><dd>0</dd><dt><span>GRIB_latitudeOfFirstGridPointInDegrees :</span></dt><dd>27.0</dd><dt><span>GRIB_latitudeOfLastGridPointInDegrees :</span></dt><dd>20.6</dd><dt><span>GRIB_longitudeOfFirstGridPointInDegrees :</span></dt><dd>88.0</dd><dt><span>GRIB_longitudeOfLastGridPointInDegrees :</span></dt><dd>92.6</dd><dt><span>GRIB_missingValue :</span></dt><dd>3.4028234663852886e+38</dd><dt><span>GRIB_name :</span></dt><dd>2 metre temperature</dd><dt><span>GRIB_shortName :</span></dt><dd>2t</dd><dt><span>GRIB_totalNumber :</span></dt><dd>0</dd><dt><span>GRIB_units :</span></dt><dd>K</dd><dt><span>long_name :</span></dt><dd>Daily maximum 2m air temperature</dd><dt><span>units :</span></dt><dd>degC</dd><dt><span>standard_name :</span></dt><dd>unknown</dd><dt><span>GRIB_surface :</span></dt><dd>0.0</dd></dl></div><div class='xr-var-data'><table>
    <tr>
        <td>
            <table style="border-collapse: collapse;">
                <thead>
                    <tr>
                        <td> </td>
                        <th> Array </th>
                        <th> Chunk </th>
                    </tr>
                </thead>
                <tbody>

                    <tr>
                        <th> Bytes </th>
                        <td> 1.34 MiB </td>
                        <td> 1.34 MiB </td>
                    </tr>

                    <tr>
                        <th> Shape </th>
                        <td> (11322, 31) </td>
                        <td> (11322, 31) </td>
                    </tr>
                    <tr>
                        <th> Dask graph </th>
                        <td colspan="2"> 1 chunks in 21 graph layers </td>
                    </tr>
                    <tr>
                        <th> Data type </th>
                        <td colspan="2"> float32 numpy.ndarray </td>
                    </tr>
                </tbody>
            </table>
        </td>
        <td>
        <svg width="75" height="170" style="stroke:rgb(0,0,0);stroke-width:1" >

  <!-- Horizontal lines -->
  <line x1="0" y1="0" x2="25" y2="0" style="stroke-width:2" />
  <line x1="0" y1="120" x2="25" y2="120" style="stroke-width:2" />

  <!-- Vertical lines -->
  <line x1="0" y1="0" x2="0" y2="120" style="stroke-width:2" />
  <line x1="25" y1="0" x2="25" y2="120" style="stroke-width:2" />

  <!-- Colored Rectangle -->
  <polygon points="0.0,0.0 25.412616514582485,0.0 25.412616514582485,120.0 0.0,120.0" style="fill:#ECB172A0;stroke-width:0"/>

  <!-- Text -->
  <text x="12.706308257291242" y="140.0" font-size="1.0rem" font-weight="100" text-anchor="middle" >31</text>
  <text x="45.41261651458248" y="60.0" font-size="1.0rem" font-weight="100" text-anchor="middle" transform="rotate(-90,45.41261651458248,60.0)">11322</text>
</svg>
        </td>
    </tr>
</table></div></li></ul></div></li><li class='xr-section-item'><input id='section-f7bc6954-bd4d-4c5a-b798-b7dbb09887fd' class='xr-section-summary-in' type='checkbox'  ><label for='section-f7bc6954-bd4d-4c5a-b798-b7dbb09887fd' class='xr-section-summary' >Indexes: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-index-name'><div>valid_time</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-43886c30-2216-4ba6-a6e7-d17d1f7db7c7' class='xr-index-data-in' type='checkbox'/><label for='index-43886c30-2216-4ba6-a6e7-d17d1f7db7c7' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(DatetimeIndex([&#x27;1989-01-01&#x27;, &#x27;1989-01-02&#x27;, &#x27;1989-01-03&#x27;, &#x27;1989-01-04&#x27;,
               &#x27;1989-01-05&#x27;, &#x27;1989-01-06&#x27;, &#x27;1989-01-07&#x27;, &#x27;1989-01-08&#x27;,
               &#x27;1989-01-09&#x27;, &#x27;1989-01-10&#x27;,
               ...
               &#x27;2019-12-22&#x27;, &#x27;2019-12-23&#x27;, &#x27;2019-12-24&#x27;, &#x27;2019-12-25&#x27;,
               &#x27;2019-12-26&#x27;, &#x27;2019-12-27&#x27;, &#x27;2019-12-28&#x27;, &#x27;2019-12-29&#x27;,
               &#x27;2019-12-30&#x27;, &#x27;2019-12-31&#x27;],
              dtype=&#x27;datetime64[ns]&#x27;, name=&#x27;valid_time&#x27;, length=11322, freq=None))</pre></div></li><li class='xr-var-item'><div class='xr-index-name'><div>station</div></div><div class='xr-index-preview'>PandasIndex</div><input type='checkbox' disabled/><label></label><input id='index-4c175601-ff65-44d3-bffd-8036a24284cb' class='xr-index-data-in' type='checkbox'/><label for='index-4c175601-ff65-44d3-bffd-8036a24284cb' title='Show/Hide index repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-index-data'><pre>PandasIndex(Index([10120, 10208, 10320, 10408, 10609, 10705, 10724, 10910, 11111, 11313,
       11316, 11407, 11505, 11513, 11604, 11610, 11704, 11706, 11805, 11809,
       11912, 11925, 11927, 11929, 12007, 12103, 12110, 41858, 41909, 41926,
       41958],
      dtype=&#x27;int64&#x27;, name=&#x27;station&#x27;))</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-fb8e572f-19ce-488e-8041-1966718bc51b' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-fb8e572f-19ce-488e-8041-1966718bc51b' class='xr-section-summary'  title='Expand/collapse section'>Attributes: <span>(0)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'></dl></div></li></ul></div></div>




```python
ERA5_final_df = ERA5_final.to_dataframe().reset_index().copy().drop(columns = ['number'])
```


```python
ERA5_final_df.rename(columns = {"t2m_min": "Tmin", "t2m_max": "Tmax",
                                    "valid_time": "Date", "station": "Station_ID"}, inplace = True)
```


```python
# Save this file for later use (Extreme Indices, and Statistical Test):
# ERA5_final_df.to_csv(r"D:\CMIP6 Project\Thesis work\Data Analysis\Data\ERA5Land_Data\interpolated data\ERA5_Land_interpolated.csv", index = False)
```

#### Visual Inspection:


```python
import matplotlib.pyplot as plt

# Select data for a specific station:
station_id = 11111
df_era5 = ERA5_final_df.query("Station_ID == @station_id")
df_bmd = BMD_temp_data.query("Station_ID == @station_id")

# Convert "Date" columns to datetime and sort by date
df_era5["Date"] = pd.to_datetime(df_era5["Date"])
df_era5 = df_era5.sort_values("Date")

df_bmd["Date"] = pd.to_datetime(df_bmd["Date"])
df_bmd = df_bmd.sort_values("Date")


# Create figure
plt.figure(figsize=(12, 6))

# Plot ERA5 (Red, Dotted)
plt.plot(
    df_era5['Date'],
    df_era5['Tmax'],
    color='red',
    linestyle='-',
    alpha=0.5,
    label='ERA5-Land Tmax'
)

# Plot BMD (Blue, Solid)
plt.plot(
    df_bmd['Date'],
    df_bmd['Tmax'],
    color='blue',
    linestyle='-',
    alpha=0.3,
    label='BMD Tmax'
)

# Labels and title
plt.xlabel('Date')
plt.ylabel('Maximum Temperature (°C)')
plt.title(f'Daily Maximum Temperature: ERA5-Land vs BMD - Station ID: {station_id}')

# Legend
plt.legend()

# Improve layout
plt.tight_layout()

# Show plot
plt.show()
```


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_44_0.png)
    


Dark shaded color means complete alignment.


```python
# Create figure
plt.figure(figsize=(12, 6))

# Plot ERA5 (Red, Dotted)
plt.plot(
    df_era5['Date'],
    df_era5['Tmin'],
    color='red',
    linestyle='-',
    alpha=0.5,
    label='ERA5-Land Tmin'
)

# Plot BMD (Blue, Solid)
plt.plot(
    df_bmd['Date'],
    df_bmd['Tmin'],
    color='blue',
    linestyle='-',
    alpha=0.3,
    label='BMD Tmin'
)

# Labels and title
plt.xlabel('Date')
plt.ylabel('Minimum Temperature (°C)')
plt.title(f'Daily Minimum Temperature: ERA5-Land vs BMD - Station ID: {station_id}')

# Legend
plt.legend()

# Improve layout
plt.tight_layout()

# Show plot
plt.show()
```


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_46_0.png)
    


#### Stationwise correlation, RMSE, and Mean Bias


```python
df_merged = pd.merge(
    BMD_temp_data,
    ERA5_final_df,
    on=['Station_ID', 'Date'],
    suffixes=('_bmd', '_era5'),
    how='inner'
)
```


```python
df_merged.isna().sum()
```




    Station_ID       0
    Tmax_bmd      1233
    Date             0
    Tmin_bmd      1362
    Latitude         0
    Longitude        0
    Tmin_era5        0
    Tmax_era5        0
    dtype: int64




```python
df_merged = df_merged.dropna(subset=['Tmin_bmd', 'Tmin_era5', 'Tmax_bmd', 'Tmax_era5'])
```


```python
bmd_st_name = pd.read_csv(r"D:\CMIP6 Project\Thesis work\BMD_stations Data\MaxTempAverRain (1).csv")
```


```python
df_merged = pd.merge(
    df_merged,
    bmd_st_name.loc[:, ["Stn_Name", "Stn_ID"]],
    left_on="Station_ID",
    right_on="Stn_ID",
    how="left"
)
```


```python
import numpy as np
from scipy.stats import pearsonr


def rmse(obs, sim):
    return np.sqrt(np.mean((sim - obs) ** 2))


def bias(obs, sim):
    return np.mean(sim - obs)


def corr(obs, sim):
    return pearsonr(obs, sim)[0]

def mae(obs, sim):
    return np.mean(np.abs(sim - obs))
```


```python
results = []

for station, group in df_merged.groupby('Stn_Name'):

    obs = group['Tmax_bmd']
    sim = group['Tmax_era5']

    r = corr(obs, sim)
    r_rmse = rmse(obs, sim)
    r_mae = mae(obs, sim)
    r_bias = bias(obs, sim)

    results.append({
        'station_id': station,
        'Correlation': r,
        'RMSE (°C)': r_rmse,
        "MAE (°C)": r_mae,
        'Mean Bias (°C)': r_bias,
        'Missing Days': 11321 - len(group)
    })


df_metrics = pd.DataFrame(results)

```


```python
print("Overall Metrics for Tmax:")
df_metrics
```

    Overall Metrics for Tmax:
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>station_id</th>
      <th>Correlation</th>
      <th>RMSE (°C)</th>
      <th>MAE (°C)</th>
      <th>Mean Bias (°C)</th>
      <th>Missing Days</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Barisal</td>
      <td>0.899101</td>
      <td>1.943085</td>
      <td>1.637737</td>
      <td>-1.312560</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bhola</td>
      <td>0.895486</td>
      <td>2.068009</td>
      <td>1.789841</td>
      <td>-1.536216</td>
      <td>241</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bogra</td>
      <td>0.893167</td>
      <td>2.132864</td>
      <td>1.785701</td>
      <td>-1.249413</td>
      <td>53</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chandpur</td>
      <td>0.904391</td>
      <td>2.121893</td>
      <td>1.801667</td>
      <td>-1.506347</td>
      <td>79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chuadanga</td>
      <td>0.937204</td>
      <td>2.113695</td>
      <td>1.782615</td>
      <td>-1.484119</td>
      <td>16</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Comilla</td>
      <td>0.874059</td>
      <td>1.866869</td>
      <td>1.540787</td>
      <td>-0.952655</td>
      <td>16</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cox's Bazar</td>
      <td>0.868301</td>
      <td>2.996366</td>
      <td>2.750040</td>
      <td>-2.700266</td>
      <td>28</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Dhaka</td>
      <td>0.922925</td>
      <td>1.906563</td>
      <td>1.603062</td>
      <td>-1.292344</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Dinajpur</td>
      <td>0.901994</td>
      <td>2.000067</td>
      <td>1.617733</td>
      <td>-0.851832</td>
      <td>22</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Faridpur</td>
      <td>0.927449</td>
      <td>1.877200</td>
      <td>1.563969</td>
      <td>-1.224177</td>
      <td>25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Feni</td>
      <td>0.869745</td>
      <td>1.844985</td>
      <td>1.526159</td>
      <td>-1.038716</td>
      <td>99</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Ishurdi</td>
      <td>0.939958</td>
      <td>1.917720</td>
      <td>1.583985</td>
      <td>-1.233522</td>
      <td>17</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Jessore</td>
      <td>0.926002</td>
      <td>2.249131</td>
      <td>1.915988</td>
      <td>-1.686008</td>
      <td>38</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Khepupara</td>
      <td>0.903524</td>
      <td>2.299527</td>
      <td>2.046775</td>
      <td>-1.930730</td>
      <td>36</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Khulna</td>
      <td>0.910232</td>
      <td>2.082155</td>
      <td>1.723965</td>
      <td>-1.405709</td>
      <td>10</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Kutubdia</td>
      <td>0.887875</td>
      <td>2.636019</td>
      <td>2.384397</td>
      <td>-2.322544</td>
      <td>134</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Madaripur</td>
      <td>0.912839</td>
      <td>1.971950</td>
      <td>1.663936</td>
      <td>-1.341305</td>
      <td>338</td>
    </tr>
    <tr>
      <th>17</th>
      <td>MaijdeeCourt</td>
      <td>0.883857</td>
      <td>2.041308</td>
      <td>1.667049</td>
      <td>-1.263498</td>
      <td>169</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Mongla</td>
      <td>0.915524</td>
      <td>2.018248</td>
      <td>1.677803</td>
      <td>-1.404491</td>
      <td>13</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Mymensingh</td>
      <td>0.885133</td>
      <td>1.775353</td>
      <td>1.411911</td>
      <td>-0.714661</td>
      <td>9</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Patuakhali</td>
      <td>0.895704</td>
      <td>1.941002</td>
      <td>1.614801</td>
      <td>-1.302138</td>
      <td>12</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Rajshahi</td>
      <td>0.939609</td>
      <td>2.068394</td>
      <td>1.723744</td>
      <td>-1.389242</td>
      <td>34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Rangamati</td>
      <td>0.896204</td>
      <td>2.261545</td>
      <td>1.944847</td>
      <td>-1.728864</td>
      <td>178</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Rangpur</td>
      <td>0.893970</td>
      <td>1.883619</td>
      <td>1.490916</td>
      <td>-0.661474</td>
      <td>12</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Satkhira</td>
      <td>0.926908</td>
      <td>1.996473</td>
      <td>1.682351</td>
      <td>-1.428754</td>
      <td>20</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Sitakunda</td>
      <td>0.880597</td>
      <td>2.975434</td>
      <td>2.738066</td>
      <td>-2.659711</td>
      <td>193</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Srimangal</td>
      <td>0.902426</td>
      <td>2.202529</td>
      <td>1.908509</td>
      <td>-1.611512</td>
      <td>106</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Syedpur</td>
      <td>0.895177</td>
      <td>2.074865</td>
      <td>1.690975</td>
      <td>-0.978229</td>
      <td>769</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Sylhet</td>
      <td>0.885027</td>
      <td>2.621758</td>
      <td>2.318249</td>
      <td>-2.084910</td>
      <td>10</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Tangail</td>
      <td>0.910102</td>
      <td>1.896549</td>
      <td>1.549974</td>
      <td>-0.972465</td>
      <td>8</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Teknaf</td>
      <td>0.840256</td>
      <td>2.354036</td>
      <td>2.075474</td>
      <td>-1.995419</td>
      <td>174</td>
    </tr>
  </tbody>
</table>
</div>



Overall, there is a good alignment of ERA5 Land with BMD station data

The validation results indicate strong agreement between ERA5-Land and BMD observations, with correlation coefficients ranging from 0.87 to 0.94 and RMSE values mostly below 2.5°C. A systematic negative bias (–1 to –2.7°C) was observed, indicating underestimation of Tmax by ERA5-Land. These results demonstrate that ERA5-Land reliably represents the temporal variability of daily maximum temperature and is suitable as a reference dataset for bias correction of CMIP6 outputs.

##### Station wise Comparison for Tmin


```python
results = []

for station, group in df_merged.groupby('Stn_Name'):

    obs = group['Tmin_bmd']
    sim = group['Tmin_era5']

    r = corr(obs, sim)
    r_rmse = rmse(obs, sim)
    r_mae = mae(obs, sim)
    r_bias = bias(obs, sim)

    results.append({
        'station_id': station,
        'Correlation': r,
        'RMSE (°C)': r_rmse,
        'MAE (°C)': r_mae,
        'Mean Bias (°C)': r_bias,
        'Missing Days': 11321 - len(group)
    })


df_metrics_min = pd.DataFrame(results)
print("Overall Metrics for Tmin:")
df_metrics_min
```

    Overall Metrics for Tmin:
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>station_id</th>
      <th>Correlation</th>
      <th>RMSE (°C)</th>
      <th>MAE (°C)</th>
      <th>Mean Bias (°C)</th>
      <th>Missing Days</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Barisal</td>
      <td>0.967247</td>
      <td>1.738818</td>
      <td>1.285983</td>
      <td>0.797960</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bhola</td>
      <td>0.966740</td>
      <td>1.905052</td>
      <td>1.380481</td>
      <td>1.038662</td>
      <td>241</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bogra</td>
      <td>0.972833</td>
      <td>1.393051</td>
      <td>1.123921</td>
      <td>-0.516531</td>
      <td>53</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chandpur</td>
      <td>0.964391</td>
      <td>1.297924</td>
      <td>0.964366</td>
      <td>0.189379</td>
      <td>79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chuadanga</td>
      <td>0.973229</td>
      <td>1.591065</td>
      <td>1.222485</td>
      <td>0.428231</td>
      <td>16</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Comilla</td>
      <td>0.964721</td>
      <td>1.377464</td>
      <td>1.050279</td>
      <td>-0.067933</td>
      <td>16</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cox's Bazar</td>
      <td>0.955526</td>
      <td>1.268859</td>
      <td>0.932709</td>
      <td>0.310247</td>
      <td>28</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Dhaka</td>
      <td>0.959329</td>
      <td>1.508846</td>
      <td>1.214102</td>
      <td>-0.486744</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Dinajpur</td>
      <td>0.975210</td>
      <td>1.422448</td>
      <td>1.119306</td>
      <td>0.092067</td>
      <td>22</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Faridpur</td>
      <td>0.964188</td>
      <td>1.658198</td>
      <td>1.251539</td>
      <td>0.632643</td>
      <td>25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Feni</td>
      <td>0.962588</td>
      <td>1.354687</td>
      <td>0.983305</td>
      <td>-0.078106</td>
      <td>99</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Ishurdi</td>
      <td>0.973922</td>
      <td>1.679059</td>
      <td>1.292877</td>
      <td>0.573197</td>
      <td>17</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Jessore</td>
      <td>0.972443</td>
      <td>1.545053</td>
      <td>1.171778</td>
      <td>0.459551</td>
      <td>38</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Khepupara</td>
      <td>0.961261</td>
      <td>2.013808</td>
      <td>1.504338</td>
      <td>1.244820</td>
      <td>36</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Khulna</td>
      <td>0.963596</td>
      <td>1.489717</td>
      <td>1.134981</td>
      <td>0.162243</td>
      <td>10</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Kutubdia</td>
      <td>0.948595</td>
      <td>1.568917</td>
      <td>1.158132</td>
      <td>0.595911</td>
      <td>134</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Madaripur</td>
      <td>0.965035</td>
      <td>1.523270</td>
      <td>1.166498</td>
      <td>0.290087</td>
      <td>338</td>
    </tr>
    <tr>
      <th>17</th>
      <td>MaijdeeCourt</td>
      <td>0.951949</td>
      <td>1.594563</td>
      <td>1.239393</td>
      <td>-0.576673</td>
      <td>169</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Mongla</td>
      <td>0.965309</td>
      <td>1.266866</td>
      <td>0.956352</td>
      <td>-0.057047</td>
      <td>13</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Mymensingh</td>
      <td>0.969525</td>
      <td>1.442319</td>
      <td>1.172017</td>
      <td>-0.436755</td>
      <td>9</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Patuakhali</td>
      <td>0.966823</td>
      <td>1.279948</td>
      <td>0.943418</td>
      <td>0.117011</td>
      <td>12</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Rajshahi</td>
      <td>0.973142</td>
      <td>1.736140</td>
      <td>1.326564</td>
      <td>0.681853</td>
      <td>34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Rangamati</td>
      <td>0.961789</td>
      <td>1.564727</td>
      <td>1.162497</td>
      <td>0.661660</td>
      <td>178</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Rangpur</td>
      <td>0.972084</td>
      <td>1.388900</td>
      <td>1.088237</td>
      <td>-0.009215</td>
      <td>12</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Satkhira</td>
      <td>0.965819</td>
      <td>1.856273</td>
      <td>1.393382</td>
      <td>0.896819</td>
      <td>20</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Sitakunda</td>
      <td>0.962004</td>
      <td>2.571498</td>
      <td>1.865894</td>
      <td>1.546527</td>
      <td>193</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Srimangal</td>
      <td>0.972348</td>
      <td>1.915190</td>
      <td>1.427218</td>
      <td>0.992119</td>
      <td>106</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Syedpur</td>
      <td>0.971117</td>
      <td>1.443901</td>
      <td>1.133046</td>
      <td>0.056812</td>
      <td>769</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Sylhet</td>
      <td>0.963773</td>
      <td>1.618981</td>
      <td>1.320147</td>
      <td>-0.877004</td>
      <td>10</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Tangail</td>
      <td>0.970051</td>
      <td>1.490004</td>
      <td>1.125666</td>
      <td>0.490330</td>
      <td>8</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Teknaf</td>
      <td>0.948770</td>
      <td>1.712345</td>
      <td>1.255294</td>
      <td>0.649354</td>
      <td>174</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_metrics_min.to_csv(r"D:\CMIP6 Project\Thesis work\Data Analysis\Data\Error metrics\ERA5L_Tmin_metrics.csv", index = False)
```

#### Hexbin Density Plot


```python
from scipy.stats import linregress
```


```python
from scipy.stats import linregress
import matplotlib.pyplot as plt

def density_scatter_plot(
    x, y,
    title="",
    xlabel="",
    ylabel="",
    panel_label=None,
    ax=None,
    label_fontsize=14,
    tick_fontsize=12,
    title_fontsize=14,
    panel_fontsize=16
):
    if ax is None:
        fig, ax = plt.subplots(figsize=(7, 6))

    # Hexbin density plot
    hb = ax.hexbin(
        x, y,
        gridsize=80,
        bins='log',
        cmap='viridis',
        mincnt=1
    )

    # Colorbar
    cb = plt.colorbar(hb, ax=ax)
    cb.set_label("Collocation Count (log scale)", fontsize=12)
    cb.ax.tick_params(labelsize=11)

    # 1:1 line
    min_val = min(x.min(), y.min())
    max_val = max(x.max(), y.max())

    ax.plot(
        [min_val, max_val],
        [min_val, max_val],
        'b--',
        lw=2,
        label='1:1 Line'
    )

    # Regression line
    slope, intercept, r, p, _ = linregress(x, y)

    ax.plot(
        x,
        slope * x + intercept,
        'r',
        lw=2,
        label='Regression'
    )

    # Axis labels
    ax.set_xlabel(xlabel, fontsize=label_fontsize)
    ax.set_ylabel(ylabel, fontsize=label_fontsize)

    # Tick font size
    ax.tick_params(axis='both', labelsize=tick_fontsize)

    # Title
    ax.set_title(
        f"{title}\nSlope = {slope:.2f}",
        fontsize=title_fontsize
    )


    # Panel label (a), (b), (c), ...
    if panel_label is not None:
        ax.text(
            -0.12, 1.08,               # x, y position (outside upper-left corner)
            f"({panel_label})",
            transform=ax.transAxes,
            fontsize=panel_fontsize,
            fontweight="bold",
            va="top",
            ha="left",
            clip_on=False              # ensures the label isn't clipped
        )

    ax.legend(fontsize=11)

    return ax
```


```python
fig, ax = plt.subplots(figsize=(7, 6))

density_scatter_plot(
    df_merged['Tmax_bmd'],
    df_merged['Tmax_era5'],
    xlabel="BMD Tmax (°C)",
    ylabel="ERA5-Land Tmax (°C)",
    panel_label="b",
    ax=ax
)

plt.tight_layout()

fig.savefig(
    "D:\CMIP6 Project\Thesis work\Table and Charts\Modifed charts\ERA5Land_tmax_density_scatter_plot.png",
    dpi=600,
    bbox_inches="tight"
)
```


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_64_0.png)
    


The hexbin density scatter plot indicates strong agreement between ERA5-Land and BMD observations, with a high correlation coefficient (r = 0.893). The majority of data points are concentrated along the 1:1 line, particularly in the range of 25–35°C, demonstrating good performance under typical climatic conditions. The regression slope (0.82) and the position of the fitted line below the 1:1 line indicate a systematic underestimation of Tmax by ERA5-Land, especially at higher temperatures. The relatively narrow spread around the regression line suggests moderate random error, while deviations at extreme values reflect reduced performance during heatwave events. Overall, the consistent and linear error structure supports the suitability of ERA5-Land as a reference dataset for bias correction


```python
fig, ax = plt.subplots(figsize=(7, 6))

density_scatter_plot(
    df_merged['Tmin_bmd'],
    df_merged['Tmin_era5'],
    xlabel = "BMD Tmin (°C)",
    ylabel = "ERA5-Land Tmin (°C)",
    panel_label="b",
    ax=ax
)

plt.tight_layout()

fig.savefig(
    "D:\CMIP6 Project\Thesis work\Table and Charts\Modifed charts\ERA5-Land_tmin_density_scatter_plot.png",
    dpi=600,
    bbox_inches="tight"
)
```


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_66_0.png)
    


#### Seasonal Evaluation

I will divide dataset into four seasons: Winter (Dec-Feb), Pre-Moonsoon (March-May), Moonsoon (June-Auguest), Post-Moonsoon (Oct-Nov)


```python
df = df_merged.copy()

df['month'] = df['Date'].dt.month

def get_season(month):

    if month in [12, 1, 2]:
        return 'Winter (DJF)'
    elif month in [3, 4, 5]:
        return 'Pre-monsoon (MAM)'
    elif month in [6, 7, 8, 9]:
        return 'Monsoon (JJAS)'
    else:
        return 'Post-monsoon (ON)'


df['season'] = df['month'].apply(get_season)

```

##### Seasonal Metrics (All Stations Combined)

For Tmax


```python
seasonal_results = []

for season, g in df.groupby('season'):

    obs = g['Tmax_bmd']
    sim = g['Tmax_era5']

    seasonal_results.append({
        'Season': season,
        'Correlation': corr(obs, sim),
        'RMSE (°C)': rmse(obs, sim),
        'MAE (°C)': mae(obs, sim),
        'Bias (°C)': bias(obs, sim)
    })

print("Sesonal Metrics for Tmax:")
df_seasonal_max = pd.DataFrame(seasonal_results)

df_seasonal_max

```

    Sesonal Metrics for Tmax:
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Season</th>
      <th>Correlation</th>
      <th>RMSE (°C)</th>
      <th>MAE (°C)</th>
      <th>Bias (°C)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Monsoon (JJAS)</td>
      <td>0.758526</td>
      <td>2.312071</td>
      <td>2.020203</td>
      <td>-1.831061</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Post-monsoon (ON)</td>
      <td>0.844551</td>
      <td>2.403183</td>
      <td>2.164631</td>
      <td>-2.068258</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Pre-monsoon (MAM)</td>
      <td>0.812826</td>
      <td>2.015210</td>
      <td>1.630170</td>
      <td>-1.053579</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Winter (DJF)</td>
      <td>0.834527</td>
      <td>1.873233</td>
      <td>1.480978</td>
      <td>-0.960740</td>
    </tr>
  </tbody>
</table>
</div>




```python
obs = df["Tmax_bmd"]
sim = df["Tmax_era5"]
overall_metrics_Tmax = pd.DataFrame({
        'Season': "Overall",
        'Correlation': corr(obs, sim),
        'RMSE (°C)': rmse(obs, sim),
        'MAE (°C)': mae(obs, sim),
        'Bias (°C)': bias(obs, sim)
}, index = [0])
```


```python
df_Tmax = pd.concat([df_seasonal_max, overall_metrics_Tmax], ignore_index=True).round(3)
df_Tmax
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Season</th>
      <th>Correlation</th>
      <th>RMSE (°C)</th>
      <th>MAE (°C)</th>
      <th>Bias (°C)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Monsoon (JJAS)</td>
      <td>0.759</td>
      <td>2.312</td>
      <td>2.020</td>
      <td>-1.831</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Post-monsoon (ON)</td>
      <td>0.845</td>
      <td>2.403</td>
      <td>2.165</td>
      <td>-2.068</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Pre-monsoon (MAM)</td>
      <td>0.813</td>
      <td>2.015</td>
      <td>1.630</td>
      <td>-1.054</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Winter (DJF)</td>
      <td>0.835</td>
      <td>1.873</td>
      <td>1.481</td>
      <td>-0.961</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Overall</td>
      <td>0.897</td>
      <td>2.154</td>
      <td>1.813</td>
      <td>-1.460</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df_Tmax.to_csv(r"D:\CMIP6 Project\Thesis work\Table and Charts\ERA5-Land_Tmax_metrics_seasonal_overall.csv", index = False)
```

For Tmin:


```python
seasonal_results = []

for season, g in df.groupby('season'):

    obs = g['Tmin_bmd']
    sim = g['Tmin_era5']

    seasonal_results.append({
        'Season': season,
        'Correlation': corr(obs, sim),
        'RMSE (°C)': rmse(obs, sim),
        'MAE (°C)': mae(obs, sim),
        'Bias (°C)': bias(obs, sim)
    })

print("Sesonal Metrics for Tmin:")
df_seasonal_min = pd.DataFrame(seasonal_results)

df_seasonal_min

```

    Sesonal Metrics for Tmin:
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Season</th>
      <th>Correlation</th>
      <th>RMSE (°C)</th>
      <th>MAE (°C)</th>
      <th>Bias (°C)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Monsoon (JJAS)</td>
      <td>0.530839</td>
      <td>1.085342</td>
      <td>0.831987</td>
      <td>-0.288820</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Post-monsoon (ON)</td>
      <td>0.914902</td>
      <td>1.386063</td>
      <td>1.081253</td>
      <td>-0.156158</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Pre-monsoon (MAM)</td>
      <td>0.864068</td>
      <td>1.826284</td>
      <td>1.367359</td>
      <td>0.647656</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Winter (DJF)</td>
      <td>0.836893</td>
      <td>2.046812</td>
      <td>1.628293</td>
      <td>1.113549</td>
    </tr>
  </tbody>
</table>
</div>




```python
obs = df["Tmin_bmd"]
sim = df["Tmin_era5"]
overall_metrics_Tmin = pd.DataFrame({
        'Season': "Overall",
        'Correlation': corr(obs, sim),
        'RMSE (°C)': rmse(obs, sim),
        'MAE (°C)': mae(obs, sim),
        'Bias (°C)': bias(obs, sim)
}, index = [0])

df_Tmin = pd.concat([df_seasonal_min, overall_metrics_Tmin], ignore_index=True).round(3)
df_Tmin
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Season</th>
      <th>Correlation</th>
      <th>RMSE (°C)</th>
      <th>MAE (°C)</th>
      <th>Bias (°C)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Monsoon (JJAS)</td>
      <td>0.531</td>
      <td>1.085</td>
      <td>0.832</td>
      <td>-0.289</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Post-monsoon (ON)</td>
      <td>0.915</td>
      <td>1.386</td>
      <td>1.081</td>
      <td>-0.156</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Pre-monsoon (MAM)</td>
      <td>0.864</td>
      <td>1.826</td>
      <td>1.367</td>
      <td>0.648</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Winter (DJF)</td>
      <td>0.837</td>
      <td>2.047</td>
      <td>1.628</td>
      <td>1.114</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Overall</td>
      <td>0.958</td>
      <td>1.609</td>
      <td>1.205</td>
      <td>0.316</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_Tmin.to_csv(r"D:\CMIP6 Project\Thesis work\Table and Charts\ERA5Land_Tmin_metrics_seasonal_overall.csv", index = False)
```

##### Seasonal Hexabin Plots:


```python
def seasonal_hexbin(df, var1, var2, season, ax, var3):

    d = df[df['season'] == season]

    density_scatter_plot(
        d[var1],
        d[var2],
        title= f"{season}",
        ax=ax,
    )


seasons = df['season'].unique()

fig, ax = plt.subplots(2, 2, figsize=(10,8))

ax = ax.flatten()

for i, s in enumerate(seasons):
    seasonal_hexbin(df, "Tmax_bmd", "Tmax_era5",s, ax[i], "Tmax")

fig.supxlabel("BMD Tmax (°C)", fontsize=12)
fig.supylabel("ERA5-Land Tmax (°C)", fontsize=12)
# fig.suptitle("Seasonal Validation of ERA5-Land Tmax", fontsize=16, weight="bold")

plt.tight_layout()
plt.show()
```


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_81_0.png)
    



```python
seasons = df['season'].unique()

fig, ax = plt.subplots(2, 2, figsize=(10,8))

ax = ax.flatten()

for i, s in enumerate(seasons):
    seasonal_hexbin(df, "Tmin_bmd", "Tmin_era5",s, ax[i], "Tmin")

fig.supxlabel("BMD Tmin (°C)", fontsize=14)
fig.supylabel("ERA5-Land Tmin (°C)", fontsize=14)
plt.tight_layout()
plt.show()
```


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_82_0.png)
    


##### Seasonal Metrics (Station Wise) For Maximum Temperature


```python
season_station = []

for (st, season), g in df.groupby(['Stn_Name', 'season']):

    obs = g['Tmax_bmd']
    sim = g['Tmax_era5']

    season_station.append({
        'Station': st,
        'Season': season,
        'Correlation': corr(obs, sim),
        'RMSE': rmse(obs, sim),
        'MAE': mae(obs, sim),
        'Bias': bias(obs, sim)
    })

# print("Station wise Seasonal Metrics for Tmax:")
df_season_station = pd.DataFrame(season_station)

# # pd.set_option('display.max_rows', 500)
# df_season_station
```


```python
season_order = [
    'Winter (DJF)',
    'Pre-monsoon (MAM)',
    'Monsoon (JJAS)',
    'Post-monsoon (ON)'
]

df_season_station['Season'] = pd.Categorical(
    df_season_station['Season'],
    categories=season_order,
    ordered=True
)
```

##### Seasonal Comparison by Boxplot

##### Tmax


```python
import seaborn as sns
# Set style
sns.set_style("whitegrid")
sns.set_context("talk")   # bigger fonts

# Create figure
fig, axes = plt.subplots(
    nrows=4,
    ncols=1,
    figsize=(10, 12),
    sharex=True
)

# -----------------------------
# 1. Correlation
# -----------------------------
sns.boxplot(
    data=df_season_station,
    x="Season",
    y="Correlation",
    ax=axes[0],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[0].set_ylabel("Correlation (r)")
axes[0].set_title("Seasonal Validation of ERA5-Land Tmax", fontsize=16, weight="bold")


# -----------------------------
# 2. RMSE
# -----------------------------
sns.boxplot(
    data=df_season_station,
    x="Season",
    y="RMSE",
    ax=axes[1],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[1].set_ylabel("RMSE (°C)")


#---------------------
# 3. MAE
#---------------------
sns.boxplot(
    data=df_season_station,
    x="Season",
    y="MAE",
    ax=axes[2],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[2].set_ylabel("MAE (°C)")

# -----------------------------
# 3. Bias
# -----------------------------
sns.boxplot(
    data=df_season_station,
    x="Season",
    y="Bias",
    ax=axes[3],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[3].set_ylabel("Bias (°C)")
axes[3].set_xlabel("Season")
# Enable x labels
axes[3].tick_params(labelbottom=True)

# Add zero line for bias
axes[3].axhline(0, color="black", linestyle="--", linewidth=1)


# -----------------------------
# Final Layout
# -----------------------------
plt.tight_layout()
plt.show()
```

    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2471159410.py:17: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2471159410.py:34: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2471159410.py:50: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2471159410.py:65: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_88_1.png)
    


#### Boxplot for Tmin:


```python
season_station = []

for (st, season), g in df.groupby(['Stn_Name', 'season']):

    obs = g['Tmin_bmd']
    sim = g['Tmin_era5']

    season_station.append({
        'Station': st,
        'Season': season,
        'Correlation': corr(obs, sim),
        'RMSE': rmse(obs, sim),
        'MAE': mae(obs, sim),
        'Bias': bias(obs, sim)
    })

# print("Station wise Seasonal Metrics for Tmin:")
df_season_station_Tmin = pd.DataFrame(season_station)

# # pd.set_option('display.max_rows', 500)
# df_season_station_Tmin
```


```python
season_order = [
    'Winter (DJF)',
    'Pre-monsoon (MAM)',
    'Monsoon (JJAS)',
    'Post-monsoon (ON)'
]

df_season_station_Tmin['Season'] = pd.Categorical(
    df_season_station_Tmin['Season'],
    categories=season_order,
    ordered=True
)
```


```python
import seaborn as sns
# Set style
sns.set_style("whitegrid")
sns.set_context("talk")   # bigger fonts

# Create figure
fig, axes = plt.subplots(
    nrows=4,
    ncols=1,
    figsize=(10, 12),
    sharex=True
)

# -----------------------------
# 1. Correlation
# -----------------------------
sns.boxplot(
    data=df_season_station_Tmin,
    x="Season",
    y="Correlation",
    ax=axes[0],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[0].set_ylabel("Correlation (r)")
axes[0].set_title("Seasonal Validation of ERA5-Land Tmin", fontsize=16, weight="bold")


# -----------------------------
# 2. RMSE
# -----------------------------
sns.boxplot(
    data=df_season_station_Tmin,
    x="Season",
    y="RMSE",
    ax=axes[1],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[1].set_ylabel("RMSE (°C)")


#---------------------
# 3. MAE
#---------------------
sns.boxplot(
    data=df_season_station_Tmin,
    x="Season",
    y="MAE",
    ax=axes[2],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[2].set_ylabel("MAE (°C)")

# -----------------------------
# 3. Bias
# -----------------------------
sns.boxplot(
    data=df_season_station_Tmin,
    x="Season",
    y="Bias",
    ax=axes[3],
    width=0.6,
    showfliers=False,
    palette="Blues"
)

axes[3].set_ylabel("Bias (°C)")
axes[3].set_xlabel("Season")
# Enable x labels
axes[3].tick_params(labelbottom=True)

# Add zero line for bias
axes[3].axhline(0, color="black", linestyle="--", linewidth=1)


# -----------------------------
# Final Layout
# -----------------------------
plt.tight_layout()
plt.show()
```

    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2815008242.py:17: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2815008242.py:34: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2815008242.py:50: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    C:\Users\Anwoy\AppData\Local\Temp\ipykernel_17300\2815008242.py:65: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(
    


    
![png](\images\Portfolio Projects\Validation of ERA5 and ERA5Land\figures/Validation_of_ERA5Land_92_1.png)
    

