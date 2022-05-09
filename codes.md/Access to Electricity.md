```python
import pandas as pd
from matplotlib import pyplot as plt
import numpy as np
```


```python
# Creating regional lists
EUCA = 'Albania; Armenia; Azerbaijan; Belarus; Bosnia and Herzegovina; Bulgaria; Croatia; Georgia; Kazakhstan; Kyrgyzstan; Montenegro; Republic of Moldova; Romania; Russian Federation; Serbia; Tajikistan; Macedonia; Turkey; Turkmenistan; Ukraine; Uzbekistan'
EUCA = EUCA.replace(';', ',')
EUCA = EUCA.split(', ')

EAP = 'Australia; Brunei Darussalam; Cambodia; China; Cook Islands; Democratic People’s Republic of Korea; Fiji; Indonesia; Japan; Kiribati; Lao People’s Democratic Republic; Malaysia; Marshall Islands; Micronesia; Mongolia; Myanmar; Nauru; New Zealand; Niue; Palau; Papua New Guinea; Philippines; Republic of Korea; Samoa; Singapore; Solomon Islands; Thailand; Timor-Leste; Tokelau ; Tonga; Tuvalu; Vanuatu; Vietnam'
EAP = EAP.replace(';', ',')
EAP = EAP.split(', ')

SAS = ['Afghanistan', 'Bangladesh', 'Bhutan', 'India', 'Maldives', 'Nepal', 'Pakistan', 'Sri Lanka']

WEU = 'Andorra; Austria; Belgium; Cyprus; Czechia; Denmark; Estonia; Finland; France; Germany; Greece; Holy See; Hungary; Iceland; Ireland; Italy; Latvia; Liechtenstein; Lithuania; Luxembourg; Malta; Monaco; Netherlands; Norway; Poland; Portugal; San Marino; Slovakia; Slovenia; Spain; Sweden; Switzerland; United Kingdom'
WEU = WEU.replace(';', ',')
WEU = WEU.split(', ')

LAC = 'Anguilla; Antigua and Barbuda; Argentina; Bahamas; Barbados; Belize; Bolivia; Brazil; British Virgin Islands; Chile; Colombia; Costa Rica; Cuba; Dominica; Dominican Republic; Ecuador; El Salvador; Grenada; Guatemala; Guyana; Haiti; Honduras; Jamaica; Mexico; Montserrat; Nicaragua; Panama; Paraguay; Peru; Saint Kitts and Nevis; Saint Lucia; Saint Vincent and the Grenadines; Suriname; Trinidad and Tobago; Turks and Caicos Islands; Uruguay; Venezuela'
LAC = LAC.replace(';', ',')
LAC = LAC.split(', ')

MENA = 'Algeria; Bahrain; Egypt, Arab Rep.; Iran; Iraq; Israel; Jordan; Kuwait; Lebanon; Libya; Morocco; Oman; Qatar; Saudi Arabia; State of Palestine; Syrian Arab Republic; Tunisia; United Arab Emirates; Yemen'
MENA = MENA.replace(';', ',')
MENA = MENA.split(', ')

NA = ['Canada', 'United States']

ESAF = 'Angola; Botswana; Burundi; Comoros; Djibouti; Eritrea; Ethiopia; Kenya; Lesotho; Madagascar; Malawi; Mauritius; Mozambique; Namibia; Rwanda; Seychelles; Somalia; South Africa; South Sudan; Sudan; Swaziland; Uganda; United Republic of Tanzania; Zambia; Zimbabwe'
ESAF = ESAF.replace(';', ',')
ESAF = ESAF.split(', ')

WCAF = 'Benin; Burkina Faso; Cabo Verde; Cameroon; Central African Republic; Chad; Congo; Côte d’Ivoire; Democratic Republic of the Congo; Equatorial Guinea; Gabon; Gambia; Ghana; Guinea; Guinea-Bissau; Liberia; Mali; Mauritania; Niger; Nigeria; Sao Tome and Principe; Senegal; Sierra Leone; Togo'
WCAF = WCAF.replace(';', ',')
WCAF = WCAF.split(', ')

reg_list = ['EUCA', 'EAP', 'SAS', 'WEU', 'LAC', 'MENA', 'NA', 'ESAF', 'WCAF']
```


```python
xls = pd.ExcelFile('data/elec_access_data2020.xls')
df1 = pd.read_excel(xls, 'Summary')
df2 = pd.read_excel(xls, 'Developing Asia')
df3 = pd.read_excel(xls, 'Africa')
df4 = pd.read_excel(xls, 'Central and South America')
df5 = pd.read_excel(xls, 'Middle East')
df3.head(10)
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
      <th>Unnamed: 0</th>
      <th>Unnamed: 1</th>
      <th>Unnamed: 2</th>
      <th>Unnamed: 3</th>
      <th>Unnamed: 4</th>
      <th>Unnamed: 5</th>
      <th>Unnamed: 6</th>
      <th>Unnamed: 7</th>
      <th>Unnamed: 8</th>
      <th>Unnamed: 9</th>
      <th>Unnamed: 10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <th>1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Source: IEA, World Energy Outlook-2020</td>
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
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Electricity Access in Africa</td>
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
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Proportion of the population with access to el...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Population without access (million)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>National</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Urban</td>
      <td>Rural</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2000</td>
      <td>2005</td>
      <td>2010</td>
      <td>2015</td>
      <td>2019</td>
      <td>2019</td>
      <td>2019</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Africa</td>
      <td>0.355</td>
      <td>0.395</td>
      <td>0.437</td>
      <td>0.492</td>
      <td>0.557</td>
      <td>0.808</td>
      <td>0.368</td>
      <td>579.2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>North Africa</td>
      <td>0.905</td>
      <td>0.969</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&lt;1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Algeria</td>
      <td>0.98</td>
      <td>0.983</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>0.967</td>
      <td>&lt;1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>Egypt</td>
      <td>0.938</td>
      <td>0.983</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&gt;99%</td>
      <td>&lt;1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.columns = range(df2.shape[1])
df2.columns = pd.to_datetime(df2.loc[5], format='%Y')
df2.columns = df2.columns.year
df2 = df2[7:]
df3.columns = range(df3.shape[1])
df3.columns = pd.to_datetime(df3.loc[5], format='%Y')
df3.columns = df3.columns.year
df3 = df3[7:]
df4.columns = range(df4.shape[1])
df4.columns = pd.to_datetime(df4.loc[5], format='%Y')
df4.columns = df4.columns.year
df4 = df4[7:]
df5.columns = range(df5.shape[1])
df5.columns = pd.to_datetime(df5.loc[5], format='%Y')
df5.columns = df5.columns.year
df5 = df5[7:]
```


```python
# Combine all piecemeal data from IEA into one dataframe.
global_ae = pd.concat([df2, df3, df4, df5]).dropna(how='all', axis=1)
global_ae.columns = global_ae.columns.fillna('country')
global_ae = global_ae.replace('>99%', 1.)
global_ae = global_ae.iloc[:,:6].reset_index()
global_ae = global_ae.drop('index', axis=1)
global_ae.insert(6, 'region', np.nan)
global_ae.columns = ['country', 2000, 2005, 2010, 2015, 2019, 'region']
global_ae
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
      <th>country</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2019</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>China</td>
      <td>0.986</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>0.43</td>
      <td>0.577</td>
      <td>0.679</td>
      <td>0.789</td>
      <td>1.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Indonesia</td>
      <td>0.534</td>
      <td>0.561</td>
      <td>0.672</td>
      <td>0.883</td>
      <td>1.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Other Southeast Asia</td>
      <td>0.645</td>
      <td>0.754</td>
      <td>0.793</td>
      <td>0.846</td>
      <td>0.908</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brunei</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>109</th>
      <td>Saudi Arabia</td>
      <td>0.977</td>
      <td>0.972</td>
      <td>0.99</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Syria</td>
      <td>0.859</td>
      <td>0.905</td>
      <td>0.927</td>
      <td>0.930</td>
      <td>0.923</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>111</th>
      <td>Qatar</td>
      <td>0.95</td>
      <td>0.969</td>
      <td>0.987</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>112</th>
      <td>United Arab Emirates</td>
      <td>0.96</td>
      <td>0.935</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Yemen</td>
      <td>0.5</td>
      <td>0.369</td>
      <td>0.396</td>
      <td>0.460</td>
      <td>0.465</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>114 rows × 7 columns</p>
</div>




```python
# Assigning each country to a region based on list fron UNICEF.
for index in range(global_ae.shape[0]):
    if global_ae.loc[index, 'country'] in EUCA:
        global_ae.loc[index, 'region'] = 'EUCA'
    elif global_ae.loc[index, 'country'] in EAP:
        global_ae.loc[index, 'region'] = 'EAP'
    elif global_ae.loc[index, 'country'] in SAS:
        global_ae.loc[index, 'region'] = 'SAS'
    elif global_ae.loc[index, 'country'] in WEU:
        global_ae.loc[index, 'region'] = 'WEU'    
    elif global_ae.loc[index, 'country'] in LAC:
        global_ae.loc[index, 'region'] = 'LAC'        
    elif global_ae.loc[index, 'country'] in MENA:
        global_ae.loc[index, 'region'] = 'MENA'    
    elif global_ae.loc[index, 'country'] in NA:
        global_ae.loc[index, 'region'] = 'NA'    
    elif global_ae.loc[index, 'country'] in ESAF:
        global_ae.loc[index, 'region'] = 'ESAF'
    elif global_ae.loc[index, 'country'] in WCAF:
        global_ae.loc[index, 'region'] = 'WCAF'    
    else: pass



# Classifying null regions for relevant countries
null_reg = global_ae[global_ae.region.isna()]
global_ae.loc[4,'region'] = 'EAP'
global_ae.loc[6,'region'] = 'EAP'
global_ae.loc[50,'region'] = 'WCAF'
global_ae.loc[55,'region'] = 'WCAF'
global_ae.loc[77,'region'] = 'ESAF'
global_ae.loc[78,'region'] = 'ESAF'
global_ae.loc[110,'region'] = 'MENA'

# Drop all other countries
global_ae = global_ae[global_ae.region.notna()]
global_ae
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
      <th>country</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2019</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>China</td>
      <td>0.986</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>0.43</td>
      <td>0.577</td>
      <td>0.679</td>
      <td>0.789</td>
      <td>1.000</td>
      <td>SAS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Indonesia</td>
      <td>0.534</td>
      <td>0.561</td>
      <td>0.672</td>
      <td>0.883</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brunei</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cambodia</td>
      <td>0.043</td>
      <td>0.118</td>
      <td>0.229</td>
      <td>0.494</td>
      <td>0.748</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>109</th>
      <td>Saudi Arabia</td>
      <td>0.977</td>
      <td>0.972</td>
      <td>0.99</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>MENA</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Syria</td>
      <td>0.859</td>
      <td>0.905</td>
      <td>0.927</td>
      <td>0.930</td>
      <td>0.923</td>
      <td>MENA</td>
    </tr>
    <tr>
      <th>111</th>
      <td>Qatar</td>
      <td>0.95</td>
      <td>0.969</td>
      <td>0.987</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>MENA</td>
    </tr>
    <tr>
      <th>112</th>
      <td>United Arab Emirates</td>
      <td>0.96</td>
      <td>0.935</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>MENA</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Yemen</td>
      <td>0.5</td>
      <td>0.369</td>
      <td>0.396</td>
      <td>0.460</td>
      <td>0.465</td>
      <td>MENA</td>
    </tr>
  </tbody>
</table>
<p>103 rows × 7 columns</p>
</div>




```python
import geonamescache
import geopandas
import ast
```

    /Users/Jane/opt/anaconda3/lib/python3.9/site-packages/geopandas/_compat.py:111: UserWarning: The Shapely GEOS version (3.10.2-CAPI-1.16.0) is incompatible with the GEOS version PyGEOS was compiled with (3.10.1-CAPI-1.16.0). Conversions between both will be slow.
      warnings.warn(



```python
gc = geonamescache.GeonamesCache()
countries = pd.DataFrame(gc.get_countries()).T
continents = pd.DataFrame(gc.get_continents()).T
world = geopandas.read_file(geopandas.datasets.get_path('naturalearth_lowres'))
cities = geopandas.read_file(geopandas.datasets.get_path('naturalearth_cities'))
```


```python
cities
world.plot()
world
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
      <th>pop_est</th>
      <th>continent</th>
      <th>name</th>
      <th>iso_a3</th>
      <th>gdp_md_est</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>920938</td>
      <td>Oceania</td>
      <td>Fiji</td>
      <td>FJI</td>
      <td>8374.0</td>
      <td>MULTIPOLYGON (((180.00000 -16.06713, 180.00000...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>53950935</td>
      <td>Africa</td>
      <td>Tanzania</td>
      <td>TZA</td>
      <td>150600.0</td>
      <td>POLYGON ((33.90371 -0.95000, 34.07262 -1.05982...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>603253</td>
      <td>Africa</td>
      <td>W. Sahara</td>
      <td>ESH</td>
      <td>906.5</td>
      <td>POLYGON ((-8.66559 27.65643, -8.66512 27.58948...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35623680</td>
      <td>North America</td>
      <td>Canada</td>
      <td>CAN</td>
      <td>1674000.0</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -122.9742...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>326625791</td>
      <td>North America</td>
      <td>United States of America</td>
      <td>USA</td>
      <td>18560000.0</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -120.0000...</td>
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
      <th>172</th>
      <td>7111024</td>
      <td>Europe</td>
      <td>Serbia</td>
      <td>SRB</td>
      <td>101800.0</td>
      <td>POLYGON ((18.82982 45.90887, 18.82984 45.90888...</td>
    </tr>
    <tr>
      <th>173</th>
      <td>642550</td>
      <td>Europe</td>
      <td>Montenegro</td>
      <td>MNE</td>
      <td>10610.0</td>
      <td>POLYGON ((20.07070 42.58863, 19.80161 42.50009...</td>
    </tr>
    <tr>
      <th>174</th>
      <td>1895250</td>
      <td>Europe</td>
      <td>Kosovo</td>
      <td>-99</td>
      <td>18490.0</td>
      <td>POLYGON ((20.59025 41.85541, 20.52295 42.21787...</td>
    </tr>
    <tr>
      <th>175</th>
      <td>1218208</td>
      <td>North America</td>
      <td>Trinidad and Tobago</td>
      <td>TTO</td>
      <td>43570.0</td>
      <td>POLYGON ((-61.68000 10.76000, -61.10500 10.890...</td>
    </tr>
    <tr>
      <th>176</th>
      <td>13026129</td>
      <td>Africa</td>
      <td>S. Sudan</td>
      <td>SSD</td>
      <td>20880.0</td>
      <td>POLYGON ((30.83385 3.50917, 29.95350 4.17370, ...</td>
    </tr>
  </tbody>
</table>
<p>177 rows × 6 columns</p>
</div>




    
![png](output_8_1.png)
    



```python
global_ae
world = world.rename(columns={'name':'country'})
new_world = pd.merge(world, global_ae, on='country', how='left')
new_world
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
      <th>pop_est</th>
      <th>continent</th>
      <th>country</th>
      <th>iso_a3</th>
      <th>gdp_md_est</th>
      <th>geometry</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2019</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>920938</td>
      <td>Oceania</td>
      <td>Fiji</td>
      <td>FJI</td>
      <td>8374.0</td>
      <td>MULTIPOLYGON (((180.00000 -16.06713, 180.00000...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>53950935</td>
      <td>Africa</td>
      <td>Tanzania</td>
      <td>TZA</td>
      <td>150600.0</td>
      <td>POLYGON ((33.90371 -0.95000, 34.07262 -1.05982...</td>
      <td>0.105</td>
      <td>0.116</td>
      <td>0.18</td>
      <td>0.30</td>
      <td>0.395</td>
      <td>ESAF</td>
    </tr>
    <tr>
      <th>2</th>
      <td>603253</td>
      <td>Africa</td>
      <td>W. Sahara</td>
      <td>ESH</td>
      <td>906.5</td>
      <td>POLYGON ((-8.66559 27.65643, -8.66512 27.58948...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35623680</td>
      <td>North America</td>
      <td>Canada</td>
      <td>CAN</td>
      <td>1674000.0</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -122.9742...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>326625791</td>
      <td>North America</td>
      <td>United States of America</td>
      <td>USA</td>
      <td>18560000.0</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -120.0000...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>172</th>
      <td>7111024</td>
      <td>Europe</td>
      <td>Serbia</td>
      <td>SRB</td>
      <td>101800.0</td>
      <td>POLYGON ((18.82982 45.90887, 18.82984 45.90888...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>173</th>
      <td>642550</td>
      <td>Europe</td>
      <td>Montenegro</td>
      <td>MNE</td>
      <td>10610.0</td>
      <td>POLYGON ((20.07070 42.58863, 19.80161 42.50009...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>174</th>
      <td>1895250</td>
      <td>Europe</td>
      <td>Kosovo</td>
      <td>-99</td>
      <td>18490.0</td>
      <td>POLYGON ((20.59025 41.85541, 20.52295 42.21787...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>175</th>
      <td>1218208</td>
      <td>North America</td>
      <td>Trinidad and Tobago</td>
      <td>TTO</td>
      <td>43570.0</td>
      <td>POLYGON ((-61.68000 10.76000, -61.10500 10.890...</td>
      <td>0.99</td>
      <td>1.0</td>
      <td>0.99</td>
      <td>0.98</td>
      <td>1.000</td>
      <td>LAC</td>
    </tr>
    <tr>
      <th>176</th>
      <td>13026129</td>
      <td>Africa</td>
      <td>S. Sudan</td>
      <td>SSD</td>
      <td>20880.0</td>
      <td>POLYGON ((30.83385 3.50917, 29.95350 4.17370, ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>177 rows × 12 columns</p>
</div>




```python
import seaborn as sns
sns.set(style="darkgrid")
palette = sns.color_palette("bright", 10)

new_world.plot(column=2019, cmap='PRGn', legend=True, figsize=(15,10), missing_kwds={'color': 'lightgrey'})

```




    <AxesSubplot:>




    
![png](output_10_1.png)
    



```python

```


```python
world.plot?
```


```python
# 195 countries as of today
countries    # 252 recognized countries is too much
world    # 177 recognized countries
foo = pd.merge(world, global_ae, on='country', how='left').set_index('country')
foo[foo.region.isna()].iloc[:,2:]

# IEA did not analyze data from "developed countries" ie Europe and North Am, or the Caribbean... (~80 countries)
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
      <th>iso_a3</th>
      <th>gdp_md_est</th>
      <th>geometry</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2019</th>
      <th>region</th>
    </tr>
    <tr>
      <th>country</th>
      <th></th>
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
      <th>Fiji</th>
      <td>FJI</td>
      <td>8374.0</td>
      <td>MULTIPOLYGON (((180.00000 -16.06713, 180.00000...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>W. Sahara</th>
      <td>ESH</td>
      <td>906.5</td>
      <td>POLYGON ((-8.66559 27.65643, -8.66512 27.58948...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>CAN</td>
      <td>1674000.0</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -122.9742...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>United States of America</th>
      <td>USA</td>
      <td>18560000.0</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -120.0000...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Kazakhstan</th>
      <td>KAZ</td>
      <td>460700.0</td>
      <td>POLYGON ((87.35997 49.21498, 86.59878 48.54918...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Macedonia</th>
      <td>MKD</td>
      <td>29520.0</td>
      <td>POLYGON ((22.38053 42.32026, 22.88137 41.99930...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Serbia</th>
      <td>SRB</td>
      <td>101800.0</td>
      <td>POLYGON ((18.82982 45.90887, 18.82984 45.90888...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Montenegro</th>
      <td>MNE</td>
      <td>10610.0</td>
      <td>POLYGON ((20.07070 42.58863, 19.80161 42.50009...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Kosovo</th>
      <td>-99</td>
      <td>18490.0</td>
      <td>POLYGON ((20.59025 41.85541, 20.52295 42.21787...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>S. Sudan</th>
      <td>SSD</td>
      <td>20880.0</td>
      <td>POLYGON ((30.83385 3.50917, 29.95350 4.17370, ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>88 rows × 9 columns</p>
</div>




```python
# attempting to manually add missing countries. fail
global_ae.head(10)
global_ae.at[113] = ['United States',1.,1.,1.,1.,1., 'NA']
global_ae.at[114] = ['Japan',1.,1.,1.,1.,1., 'EAP']
global_ae.at[115] = ['United Kingdom',1.,1.,1.,1.,1., 'WEU']
global_ae.at[116] = ['Denmark',1.,1.,1.,1.,1., 'WEU']
global_ae.at[117] = ['Italy',1.,1.,1.,1.,1., 'WEU']
global_ae.at[118] = ['Australia',1.,1.,1.,1.,1., 'EAP']
```

    /Users/Jane/opt/anaconda3/lib/python3.9/site-packages/pandas/core/indexing.py:1797: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self._setitem_single_column(loc, v, pi)
    /Users/Jane/opt/anaconda3/lib/python3.9/site-packages/pandas/core/frame.py:3834: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self.loc[index, col] = value



```python
## europe list
for index in range(world.shape[0]):
    if world.loc[index, 'continent'] == 'Europe':
        print(world.loc[index, 'country'])
```

    Russia
    Norway
    France
    Sweden
    Belarus
    Ukraine
    Poland
    Austria
    Hungary
    Moldova
    Romania
    Lithuania
    Latvia
    Estonia
    Germany
    Bulgaria
    Greece
    Albania
    Croatia
    Switzerland
    Luxembourg
    Belgium
    Netherlands
    Portugal
    Spain
    Ireland
    Italy
    Denmark
    United Kingdom
    Iceland
    Slovenia
    Finland
    Slovakia
    Czechia
    Bosnia and Herz.
    Macedonia
    Serbia
    Montenegro
    Kosovo



```python
foo[foo.region.isna()].plot()

```




    <AxesSubplot:>




    
![png](output_16_1.png)
    



```python
global_ae[['country',2019.0]].sort_values(2019.0, ascending=False).head(40)
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
      <th>country</th>
      <th>2019</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>China</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Seychelles</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>83</th>
      <td>Brazil</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>85</th>
      <td>Costa Rica</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>86</th>
      <td>Cuba</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Paraguay</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Trinidad and Tobago</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Uruguay</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Venezuela</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Bahrain</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Iran</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Jordan</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Kuwait</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Lebanon</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>109</th>
      <td>Saudi Arabia</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>111</th>
      <td>Qatar</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>112</th>
      <td>United Arab Emirates</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>113</th>
      <td>United States</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Japan</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>115</th>
      <td>United Kingdom</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Denmark</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Italy</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Mauritius</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Australia</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Morocco</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Tunisia</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Libya</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Vietnam</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Thailand</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Singapore</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Sri Lanka</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Algeria</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Malaysia</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Egypt</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brunei</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Indonesia</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Argentina</td>
      <td>0.988</td>
    </tr>
    <tr>
      <th>108</th>
      <td>Oman</td>
      <td>0.987</td>
    </tr>
    <tr>
      <th>93</th>
      <td>Jamaica</td>
      <td>0.986</td>
    </tr>
  </tbody>
</table>
</div>




```python
global_ae
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
      <th>country</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2019</th>
      <th>region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>China</td>
      <td>0.986</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>0.43</td>
      <td>0.577</td>
      <td>0.679</td>
      <td>0.789</td>
      <td>1.000</td>
      <td>SAS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Indonesia</td>
      <td>0.534</td>
      <td>0.561</td>
      <td>0.672</td>
      <td>0.883</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brunei</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cambodia</td>
      <td>0.043</td>
      <td>0.118</td>
      <td>0.229</td>
      <td>0.494</td>
      <td>0.748</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Japan</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
    <tr>
      <th>115</th>
      <td>United Kingdom</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>WEU</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Denmark</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>WEU</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Italy</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>WEU</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Australia</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>EAP</td>
    </tr>
  </tbody>
</table>
<p>108 rows × 7 columns</p>
</div>




```python

```
