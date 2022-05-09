```python
import pandas as pd
from matplotlib import pyplot as plt
from matplotlib import ticker as tick
import matplotlib.colors as mcolors
import seaborn as sns
import numpy as np
%matplotlib inline
```

# INWARD REMITTANCES (receiving, incoming)


```python
inrem = pd.read_excel('inward_remit.xlsx')
```


```python
inrem = inrem[:216]
inrem = inrem[:216]
inrem = inrem.dropna(how='all')
inrem0 = inrem.replace(np.nan, 0)
inrem0 = inrem0.rename(columns={"Migrant remittance inflows (US$ million)": "Inflow Country", "Remittances as a share of GDP in 2021e (%)": "remit_gdp"}).set_index('Inflow Country').replace(' ', np.nan)
# rename country column, rename %GDP column, set country column as index, replace empty value with Nan
inrem0['total_rem'] = inrem0.sum(axis=1)
# add column for aggregate remittances
inrem0.insert(42, 'pct_gdp', value=((1*inrem0['remit_gdp']).astype(str) + "%"))
# add column for percent gdp, converted to percent
colors=['salmon','blue','yellow','magenta','mediumspringgreen','powderblue','blueviolet','goldenrod','crimson','g']
```


```python
import datapackage
data_url = 'https://datahub.io/core/cpi-us/datapackage.json'

# to load Data Package into storage
package = datapackage.Package(data_url)

resources = package.resources
for resource in resources:
    if resource.tabular:
        data = pd.read_csv(resource.descriptor['path'])
        print (data)
```

                Date    Index  Inflation
    0     1913-01-01    9.800        NaN
    1     1913-02-01    9.800       0.00
    2     1913-03-01    9.800       0.00
    3     1913-04-01    9.800       0.00
    4     1913-05-01    9.700      -1.02
    ...          ...      ...        ...
    1208  2013-09-01  234.149       0.12
    1209  2013-10-01  233.546      -0.26
    1210  2013-11-01  233.069      -0.20
    1211  2013-12-01  233.049      -0.01
    1212  2014-01-01  233.916       0.37
    
    [1213 rows x 3 columns]
                Date    Index  Inflation
    0     1913-01-01    9.800        NaN
    1     1913-02-01    9.800       0.00
    2     1913-03-01    9.800       0.00
    3     1913-04-01    9.800       0.00
    4     1913-05-01    9.700      -1.02
    ...          ...      ...        ...
    1208  2013-09-01  234.149       0.12
    1209  2013-10-01  233.546      -0.26
    1210  2013-11-01  233.069      -0.20
    1211  2013-12-01  233.049      -0.01
    1212  2014-01-01  233.916       0.37
    
    [1213 rows x 3 columns]



```python
import cpi
```


```python
adj = pd.read_excel('data/inward_remit.xlsx')
adj = adj.set_index('Migrant remittance inflows (US$ million)')[:214]
adj = adj.rename(columns={'index':'year','2021e':2021, 'Migrant remittance inflows (US$ million)':'inflow_country'}).drop('Remittances as a share of GDP in 2021e (%)',axis=1)
adj.index.rename('index', inplace=True)
adj = adj.T
```


```python
adj
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
      <th>index</th>
      <th>Afghanistan</th>
      <th>Albania</th>
      <th>Algeria</th>
      <th>American Samoa</th>
      <th>Andorra</th>
      <th>Angola</th>
      <th>Antigua and Barbuda</th>
      <th>Argentina</th>
      <th>Armenia</th>
      <th>Aruba</th>
      <th>...</th>
      <th>Uruguay</th>
      <th>Uzbekistan</th>
      <th>Vanuatu</th>
      <th>Venezuela, RB</th>
      <th>Vietnam</th>
      <th>Virgin Islands (U.S.)</th>
      <th>West Bank and Gaza</th>
      <th>Yemen, Rep.</th>
      <th>Zambia</th>
      <th>Zimbabwe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1980</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>406.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16.891617</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>447.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>42.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>28.294628</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>507.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>28.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9.35478</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.895335</td>
    </tr>
    <tr>
      <th>1983</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>392.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>28.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.145182</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19.556181</td>
    </tr>
    <tr>
      <th>1984</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>329.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.468008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.806287</td>
    </tr>
    <tr>
      <th>1985</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>313.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>27.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.735109</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.619641</td>
    </tr>
    <tr>
      <th>1986</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>358.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.185185</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.022562</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.785055</td>
    </tr>
    <tr>
      <th>1987</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>487.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.744444</td>
      <td>34.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.4628</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.143026</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>379.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12.337037</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.009554</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.382946</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>345.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13.196296</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.319443</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.712249</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>352.44176</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>9.4</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>6.888202</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1500.0</td>
      <td>0.0</td>
      <td>0.487599</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>232.990263</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.731844</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>6.967351</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>998.0</td>
      <td>0.0</td>
      <td>0.282919</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>0.0</td>
      <td>151.8</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>15.4</td>
      <td>0.0</td>
      <td>1.731844</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>6.813023</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1020.0</td>
      <td>0.0</td>
      <td>0.410772</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>0.0</td>
      <td>332.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>7.925926</td>
      <td>57.7</td>
      <td>0.2</td>
      <td>2.402235</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>4.943892</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1040.0</td>
      <td>0.0</td>
      <td>0.508734</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>0.0</td>
      <td>307.1</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>8.614815</td>
      <td>62.4</td>
      <td>11.12</td>
      <td>3.631285</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>5.758934</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1060.0</td>
      <td>0.0</td>
      <td>0.599092</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>0.0</td>
      <td>427.3</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>63.6</td>
      <td>71.35</td>
      <td>1.340782</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>6.128564</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>582.1</td>
      <td>1080.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1996</th>
      <td>0.0</td>
      <td>550.9</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.142</td>
      <td>8.940741</td>
      <td>65.0</td>
      <td>153.73</td>
      <td>1.620112</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>542.3</td>
      <td>1140.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1997</th>
      <td>0.0</td>
      <td>300.3</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>9.537037</td>
      <td>65.7</td>
      <td>228.9864</td>
      <td>1.843575</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>17.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>623.3</td>
      <td>1170.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>0.0</td>
      <td>504.14</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>18.755556</td>
      <td>68.5</td>
      <td>166.64797</td>
      <td>1.620112</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>7.780196</td>
      <td>17.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1058.245498</td>
      <td>1200.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1999</th>
      <td>0.0</td>
      <td>407.2</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>18.394444</td>
      <td>64.3</td>
      <td>182.652132</td>
      <td>0.608939</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>9.620369</td>
      <td>17.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1096.285162</td>
      <td>1220.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>0.0</td>
      <td>597.8</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>17.342963</td>
      <td>86.343659</td>
      <td>182.16</td>
      <td>1.083799</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>13.50673</td>
      <td>17.0</td>
      <td>1340.0</td>
      <td>NaN</td>
      <td>863.8</td>
      <td>1290.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>0.0</td>
      <td>699.3</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>23.676667</td>
      <td>189.6</td>
      <td>209.24</td>
      <td>1.335196</td>
      <td>...</td>
      <td>0.006038</td>
      <td>NaN</td>
      <td>18.430386</td>
      <td>19.0</td>
      <td>1100.0</td>
      <td>NaN</td>
      <td>805.742463</td>
      <td>1300.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>0.0</td>
      <td>733.57</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>14.242167</td>
      <td>206.63</td>
      <td>263.89</td>
      <td>1.329609</td>
      <td>...</td>
      <td>36.053</td>
      <td>NaN</td>
      <td>4.097123</td>
      <td>19.0</td>
      <td>1770.0</td>
      <td>NaN</td>
      <td>771.775118</td>
      <td>1290.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>0.0</td>
      <td>888.748582</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>16.372237</td>
      <td>273.42</td>
      <td>335.86</td>
      <td>0.273743</td>
      <td>...</td>
      <td>61.753293</td>
      <td>NaN</td>
      <td>3.995373</td>
      <td>208.0</td>
      <td>2100.0</td>
      <td>NaN</td>
      <td>310.077968</td>
      <td>1270.0</td>
      <td>36.3</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>0.0</td>
      <td>1160.672105</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>17.601626</td>
      <td>311.78</td>
      <td>787.51951</td>
      <td>1.458101</td>
      <td>...</td>
      <td>69.896167</td>
      <td>NaN</td>
      <td>4.930017</td>
      <td>143.0</td>
      <td>2310.0</td>
      <td>NaN</td>
      <td>398.558393</td>
      <td>1280.0</td>
      <td>48.4</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>0.0</td>
      <td>1289.704316</td>
      <td>170.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>18.305489</td>
      <td>432.09</td>
      <td>915.231162</td>
      <td>0.819846</td>
      <td>...</td>
      <td>76.74039</td>
      <td>NaN</td>
      <td>5.097613</td>
      <td>148.0</td>
      <td>3150.0</td>
      <td>NaN</td>
      <td>378.337239</td>
      <td>1282.599</td>
      <td>52.9</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>0.0</td>
      <td>1359.467325</td>
      <td>189.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>19.32572</td>
      <td>540.7</td>
      <td>1169.173063</td>
      <td>1.036166</td>
      <td>...</td>
      <td>88.93462</td>
      <td>NaN</td>
      <td>4.989727</td>
      <td>165.0</td>
      <td>3800.0</td>
      <td>NaN</td>
      <td>464.056318</td>
      <td>1282.6</td>
      <td>57.68</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>0.0</td>
      <td>1468.02</td>
      <td>99.004563</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>20.783287</td>
      <td>606.498927</td>
      <td>1644.375091</td>
      <td>5.195531</td>
      <td>...</td>
      <td>96.476</td>
      <td>NaN</td>
      <td>5.543183</td>
      <td>151.0</td>
      <td>6180.0</td>
      <td>NaN</td>
      <td>598.543423</td>
      <td>1321.52</td>
      <td>59.3</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>89.5</td>
      <td>1865.6</td>
      <td>103.631887</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>82.084</td>
      <td>21.828403</td>
      <td>705.144403</td>
      <td>1904.067123</td>
      <td>6.759777</td>
      <td>...</td>
      <td>107.912</td>
      <td>NaN</td>
      <td>8.90663</td>
      <td>137.0</td>
      <td>6805.0</td>
      <td>NaN</td>
      <td>740.724366</td>
      <td>1410.52</td>
      <td>68.195</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>140.695166</td>
      <td>1717.698012</td>
      <td>150.336961</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.2</td>
      <td>20.658719</td>
      <td>628.542376</td>
      <td>1439.809232</td>
      <td>9.050279</td>
      <td>...</td>
      <td>101.073</td>
      <td>NaN</td>
      <td>11.492044</td>
      <td>132.0</td>
      <td>6020.0</td>
      <td>NaN</td>
      <td>755.235908</td>
      <td>1160.0</td>
      <td>41.264</td>
      <td>648.6</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>378.206657</td>
      <td>1586.574271</td>
      <td>196.6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.972037</td>
      <td>20.197667</td>
      <td>644.30074</td>
      <td>1669.336819</td>
      <td>4.972067</td>
      <td>...</td>
      <td>124.891</td>
      <td>3437.519158</td>
      <td>11.8</td>
      <td>143.0</td>
      <td>8260.0</td>
      <td>NaN</td>
      <td>927.139387</td>
      <td>1526.0</td>
      <td>43.657312</td>
      <td>748.6</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>179.116561</td>
      <td>1552.078514</td>
      <td>202.869816</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.204751</td>
      <td>20.29261</td>
      <td>697.379575</td>
      <td>1798.624692</td>
      <td>5.307263</td>
      <td>...</td>
      <td>128.836</td>
      <td>4910.053573</td>
      <td>21.765886</td>
      <td>138.0</td>
      <td>8600.0</td>
      <td>NaN</td>
      <td>1141.713036</td>
      <td>1403.92</td>
      <td>46.276751</td>
      <td>882.300191</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>219.416087</td>
      <td>1419.772515</td>
      <td>214.841269</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>40.348854</td>
      <td>20.85622</td>
      <td>577.532962</td>
      <td>1914.983997</td>
      <td>4.860335</td>
      <td>...</td>
      <td>91.6</td>
      <td>6089.643562</td>
      <td>22.036538</td>
      <td>118.0</td>
      <td>10000.0</td>
      <td>NaN</td>
      <td>1737.049553</td>
      <td>3351.0</td>
      <td>72.864</td>
      <td>944.572788</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>347.165292</td>
      <td>1281.848114</td>
      <td>209.601443</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>36.637411</td>
      <td>21.127351</td>
      <td>535.004409</td>
      <td>2192.193827</td>
      <td>6.337951</td>
      <td>...</td>
      <td>98.848478</td>
      <td>6443.498684</td>
      <td>23.710131</td>
      <td>120.0</td>
      <td>11000.0</td>
      <td>NaN</td>
      <td>1489.335822</td>
      <td>3342.5</td>
      <td>53.980262</td>
      <td>783.247848</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>253.367822</td>
      <td>1421.007454</td>
      <td>2452.442617</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.971119</td>
      <td>32.1</td>
      <td>505.346892</td>
      <td>2078.618315</td>
      <td>7.465211</td>
      <td>...</td>
      <td>97.830785</td>
      <td>6815.207509</td>
      <td>64.091052</td>
      <td>128.0</td>
      <td>12000.0</td>
      <td>NaN</td>
      <td>1804.542445</td>
      <td>3350.5</td>
      <td>58.300302</td>
      <td>735.0</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>348.624717</td>
      <td>1290.863508</td>
      <td>1997.393458</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.114712</td>
      <td>31.244412</td>
      <td>494.433532</td>
      <td>1491.475903</td>
      <td>8.083713</td>
      <td>...</td>
      <td>90.267058</td>
      <td>4843.179722</td>
      <td>104.193107</td>
      <td>161.0</td>
      <td>13000.0</td>
      <td>NaN</td>
      <td>1817.412109</td>
      <td>3350.5</td>
      <td>47.046538</td>
      <td>790.4</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>627.710802</td>
      <td>1306.009167</td>
      <td>1989.023597</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.988048</td>
      <td>26.705676</td>
      <td>391.579048</td>
      <td>1382.330887</td>
      <td>52.7</td>
      <td>...</td>
      <td>90.443153</td>
      <td>5795.061401</td>
      <td>80.626634</td>
      <td>279.0</td>
      <td>14000.0</td>
      <td>NaN</td>
      <td>2086.576176</td>
      <td>3770.584</td>
      <td>38.464441</td>
      <td>750.3</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>822.73163</td>
      <td>1311.822432</td>
      <td>1791.887073</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.418196</td>
      <td>24.020044</td>
      <td>479.93746</td>
      <td>1538.655752</td>
      <td>56.14034</td>
      <td>...</td>
      <td>109.381555</td>
      <td>7130.151739</td>
      <td>25.987675</td>
      <td>279.0</td>
      <td>15000.0</td>
      <td>NaN</td>
      <td>2378.923437</td>
      <td>NaN</td>
      <td>93.644095</td>
      <td>1013.367658</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>803.546454</td>
      <td>1458.210056</td>
      <td>1984.998399</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.579247</td>
      <td>24.706009</td>
      <td>506.543246</td>
      <td>1488.016544</td>
      <td>36.920295</td>
      <td>...</td>
      <td>113.957699</td>
      <td>7609.613692</td>
      <td>35.10344</td>
      <td>279.0</td>
      <td>16000.0</td>
      <td>NaN</td>
      <td>2833.912788</td>
      <td>NaN</td>
      <td>106.965626</td>
      <td>897.902104</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>828.571904</td>
      <td>1472.812242</td>
      <td>1785.838683</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.445473</td>
      <td>24.706009</td>
      <td>541.741887</td>
      <td>1527.961727</td>
      <td>34.264018</td>
      <td>...</td>
      <td>112.271708</td>
      <td>8545.813107</td>
      <td>74.997098</td>
      <td>279.0</td>
      <td>17000.0</td>
      <td>NaN</td>
      <td>3152.859814</td>
      <td>NaN</td>
      <td>98.259121</td>
      <td>921.726525</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>788.917115</td>
      <td>1465.987212</td>
      <td>1699.608935</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.053051</td>
      <td>24.706009</td>
      <td>630.973885</td>
      <td>1327.006085</td>
      <td>35.002158</td>
      <td>...</td>
      <td>110.716491</td>
      <td>6979.795069</td>
      <td>87.467129</td>
      <td>279.0</td>
      <td>17200.0</td>
      <td>NaN</td>
      <td>2645.805425</td>
      <td>NaN</td>
      <td>134.864832</td>
      <td>1209.718045</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>627.710802</td>
      <td>1600</td>
      <td>1759.095247</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.845093</td>
      <td>24.706009</td>
      <td>961.138354</td>
      <td>1228.37</td>
      <td>37.659358</td>
      <td>...</td>
      <td>115.839331</td>
      <td>7600</td>
      <td>74.8026</td>
      <td>279</td>
      <td>18060</td>
      <td>NaN</td>
      <td>2890.4</td>
      <td>NaN</td>
      <td>141.608073</td>
      <td>1354.88421</td>
    </tr>
  </tbody>
</table>
<p>42 rows × 214 columns</p>
</div>




```python

# adj['adjusted'] = adj.apply(lambda x: cpi.inflate(x.MEDIAN_HOUSEHOLD_INCOME, x.YEAR), axis=1) for i in adj.iloc[i]

```


```python
adj.iloc[4]
```




    index
    Afghanistan                   NaN
    Albania                       NaN
    Algeria                     329.0
    American Samoa                NaN
    Andorra                       NaN
                               ...   
    Virgin Islands (U.S.)         NaN
    West Bank and Gaza            NaN
    Yemen, Rep.                   NaN
    Zambia                        NaN
    Zimbabwe                 3.806287
    Name: 1984, Length: 214, dtype: object



# (GLOBAL) Countries RECEIVING the most remittances

### Top 10 Remittance Receiving Countries: 
### India, China, Mexico, Philippines, France, Egypt, Nigeria, Germany, Pakistan, Bangladesh


```python
plt.axes(xlabel='Country', ylabel='Remittances Received (billions)')
plt.rc('font', size=14)
col = ['#CD7F32','#CC5500','#F28C28','#E3963E','#FFBF00','#DAA520','#FFC000','#FFEA00','#FAC898','#FFE5B4']
plt.title('Countries Receiving the Most Remittances Overall', fontsize=16)
inrem0.sort_values('total_rem', ascending=False).total_rem[2:12].plot(kind='bar', color=col, fontsize=14)

plt.gca().spines[['top', 'right']].set_visible(False)
plt.ticklabel_format(style='plain', axis='y')
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
fig = plt.show()

```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_35236/3358225703.py:9: UserWarning:
    
    FixedFormatter should only be used together with FixedLocator
    



    
![png](output_12_1.png)
    



```python
import plotly
```


```python
print(plotly.offline.plot(fig, include_plotlyjs=False, output_type='div'))
```


    ---------------------------------------------------------------------------

    PlotlyError                               Traceback (most recent call last)

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_35236/238782760.py in <module>
    ----> 1 print(plotly.offline.plot(fig, include_plotlyjs=False, output_type='div'))
    

    ~/opt/anaconda3/lib/python3.9/site-packages/plotly/offline/offline.py in plot(figure_or_data, show_link, link_text, validate, output_type, include_plotlyjs, filename, auto_open, image, image_filename, image_width, image_height, config, include_mathjax, auto_play, animation_opts)
        571     config.setdefault("linkText", link_text)
        572 
    --> 573     figure = tools.return_figure_from_figure_or_data(figure_or_data, validate)
        574     width = figure.get("layout", {}).get("width", "100%")
        575     height = figure.get("layout", {}).get("height", "100%")


    ~/opt/anaconda3/lib/python3.9/site-packages/plotly/tools.py in return_figure_from_figure_or_data(figure_or_data, validate_figure)
        542         validated = True
        543     else:
    --> 544         raise exceptions.PlotlyError(
        545             "The `figure_or_data` positional "
        546             "argument must be "


    PlotlyError: The `figure_or_data` positional argument must be `dict`-like, `list`-like, or an instance of plotly.graph_objs.Figure


### Top RECEIVERS (1-5, 6-10, 11-15)


```python
inrem_countries = inrem0.sort_values('total_rem', ascending=False)[2:]
inrem_countries = inrem_countries.drop('remit_gdp', axis=1).drop('total_rem', axis=1).drop('pct_gdp', axis=1)
```


```python
# Formatting
plt.figure(figsize=(7,5))
plt.axes(title='Top 5 Remittance Receivers', xlabel='Year', ylabel='Annual Remittances (USD billion)')
plt.rc('font', size=14)    # overall font
plt.gca().spines[['top', 'right']].set_visible(False)    # remove top and right figure bounds (aesthetic)
plt.ticklabel_format(style='plain', axis='y')    # remove '1e6' (million) multiplier from y-axis

for i in range(5):
    inrem_countries.iloc[i].plot()
    
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])    # change y-labels to billions
plt.legend(loc='best', fontsize=12)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2684825556.py:11: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])    # change y-labels to billions



    
![png](output_17_1.png)
    



```python
# Top Receivers (#6-10)
plt.figure(figsize=(7,5))
plt.axes(title='Ranks 6-10 Remittance Receivers', xlabel='Year', ylabel='Annual Remittances (USD billions)')
plt.rc('font', size=14)   
plt.gca().spines[['top', 'right']].set_visible(False)

plt.ticklabel_format(style='plain', axis='y')
for i in range(5,10):
    inrem_countries.iloc[i].plot()

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])    # change y-labels to billions
plt.legend(loc='best', fontsize=12)
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/558974298.py:11: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])    # change y-labels to billions





    <matplotlib.legend.Legend at 0x7fb29f9cbca0>




    
![png](output_18_2.png)
    



```python
# Top Senders (#11-15)
plt.figure(figsize=(7,5))
plt.axes(title='Ranks 11-15 Remittance Receivers', xlabel='Year', ylabel='Annual Remittances (USD billions)')
plt.rc('font', size=14)   
plt.gca().spines[['top', 'right']].set_visible(False)
plt.ticklabel_format(style='plain', axis='y')

for i in range(10, 15):
    inrem_countries.iloc[i].plot()

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=12)
plt.close()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1936985037.py:11: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])


# Percent of GDP from Remittances (top 10)


```python
top_gdp = inrem0.sort_values('remit_gdp', ascending=False)
top_gdp = pd.DataFrame(top_gdp['remit_gdp'])
```


```python
plt.figure(figsize=(7,5))
top_gdp[:10].plot(kind='bar', fontsize=14, ylim=(0,55), color=['b','b','k','m'], xlabel='Country', ylabel='% GDP from Remittances', legend=False)

plt.title('Countries with Highest % of GDP from Remittances', fontsize=16)
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.rc('font', size=14)  

plt.show()
```


    <Figure size 504x360 with 0 Axes>



    
![png](output_22_1.png)
    


# Regional Remittance INFLOWS Analysis


```python
import geonamescache
import ast
gc = geonamescache.GeonamesCache()
countries = pd.DataFrame(gc.get_countries()).T
continents = pd.DataFrame(gc.get_continents()).T
```


```python
continents = continents.rename(columns={'continentCode': 'continentcode'})
# cleaning up imported column to merge on so it matches
mapp = pd.merge(countries, continents, on='continentcode', how='left')
# mapping countries onto continents dictionary
mapp = mapp.rename(columns={'name_x': 'Inflow Country'})
# renaming to match col in next merge
mapp2 = mapp[['Inflow Country', 'continentcode', 'capital', 'population_x', 'currencycode', 'languages', 'geonameid']]
# selecting data columns from mapp I want in order to map continent codes (& other data) onto WB dataset
in_global = inrem0.merge(mapp2, on='Inflow Country', how='left')
```

#### Isolating countries with null continent codes to match them


```python
null_cont = in_global[['Inflow Country', 'continentcode']]
null_cont.continentcode.isna().describe()
# 35 uncategorized countries
null_cont['null'] = null_cont['continentcode'].isna()
null_cont = null_cont.sort_values('null', ascending=False)[1:35]
# creating df to identify countries with null continentcode. will update their values in broader df
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1046373033.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      null_cont['null'] = null_cont['continentcode'].isna()



```python
null_cont.index
in_global.at[105, 'continentcode'] = 'AS'
in_global.at[128, 'continentcode'] = 'OC'
in_global.at[211, 'continentcode'] = 'AS'
in_global.at[13, 'continentcode'] = 'CB'
in_global.at[210, 'continentcode'] = 'AS'
in_global.at[209, 'continentcode'] = 'CB'
in_global.at[102, 'continentcode'] = 'AS'
in_global.at[101, 'continentcode'] = 'AS'
in_global.at[106, 'continentcode'] = 'AS'
in_global.at[207, 'continentcode'] = 'SA'
in_global.at[70, 'continentcode'] = 'AF'
in_global.at[190, 'continentcode'] = 'AS'
in_global.at[158, 'continentcode'] = 'EU'
in_global.at[64, 'continentcode'] = 'EU'
in_global.at[62, 'continentcode'] = 'AF'
in_global.at[57, 'continentcode'] = 'AF'
in_global.at[169, 'continentcode'] = 'CB'
in_global.at[170, 'continentcode'] = 'EU'
in_global.at[84, 'continentcode'] = 'AS'
in_global.at[142, 'continentcode'] = 'EU'
in_global.at[46, 'continentcode'] = 'AF'
in_global.at[89, 'continentcode'] = 'AS'
in_global.at[44, 'continentcode'] = 'AF'
in_global.at[43, 'continentcode'] = 'AF'
in_global.at[178, 'continentcode'] = 'CB'
in_global.at[179, 'continentcode'] = 'CB'
in_global.at[180, 'continentcode'] = 'CB'
in_global.at[181, 'continentcode'] = 'CB'
in_global.at[38, 'continentcode'] = 'EU'
in_global.at[186, 'continentcode'] = 'AS'
in_global.at[31, 'continentcode'] = 'AF'
in_global.at[27, 'continentcode'] = 'AS'

continent_dict = {
    'AS': 'Asia',
    'AF': 'Africa',
    'SA': 'South America',
    'NA': 'North America',
    'EU': 'Europe',
    'OC': 'Oceania',
    'CB': 'Caribbean'
}
in_global['continent'] = in_global.continentcode.map(continent_dict)
in_global.continent.isna().describe()    # 2 with null continent ('World', 'LICs')

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

# With these lists... create new column to identify region
in_global.shape
in_global.insert(52, 'region', np.nan)
```


```python
# Assigning each country to a region based on list fron UNICEF.
for index in range(in_global.shape[0]):
    if in_global.loc[index, 'Inflow Country'] in EUCA:
        in_global.loc[index, 'region'] = 'EUCA'
    elif in_global.loc[index, 'Inflow Country'] in EAP:
        in_global.loc[index, 'region'] = 'EAP'
    elif in_global.loc[index, 'Inflow Country'] in SAS:
        in_global.loc[index, 'region'] = 'SAS'
    elif in_global.loc[index, 'Inflow Country'] in WEU:
        in_global.loc[index, 'region'] = 'WEU'
    elif in_global.loc[index, 'Inflow Country'] in LAC:
        in_global.loc[index, 'region'] = 'LAC'
    elif in_global.loc[index, 'Inflow Country'] in MENA:
        in_global.loc[index, 'region'] = 'MENA'
    elif in_global.loc[index, 'Inflow Country'] in NA:
        in_global.loc[index, 'region'] = 'NA'
    elif in_global.loc[index, 'Inflow Country'] in ESAF:
        in_global.loc[index, 'region'] = 'ESAF'
    elif in_global.loc[index, 'Inflow Country'] in WCAF:
        in_global.loc[index, 'region'] = 'WCAF'
    else: pass
```


```python
# Identify and classify countries with null regions
null_reg = in_global[in_global.region.isna()]
null_reg
in_global.at[3, 'region'] = 'EAP'
in_global.at[9, 'region'] = 'LAC'
in_global.at[13, 'region'] = 'LAC'
in_global.at[21, 'region'] = 'LAC'
in_global.at[35, 'region'] = 'LAC'
in_global.at[38, 'region'] = 'WEU'
in_global.at[43, 'region'] = 'WCAF'
in_global.at[44, 'region'] = 'WCAF'
in_global.at[46, 'region'] = 'WCAF'
in_global.at[49, 'region'] = 'LAC'
in_global.at[51, 'region'] = 'WEU'
in_global.at[57, 'region'] = 'MENA'
in_global.at[62, 'region'] = 'ESAF'
in_global.at[64, 'region'] = 'WEU'
in_global.at[68, 'region'] = 'EAP'
in_global.at[70, 'region'] = 'WCAF'
in_global.at[77, 'region'] = 'EAP'
in_global.at[84, 'region'] = 'EAP'
in_global.at[89, 'region'] = 'MENA'
in_global.at[102, 'region'] = 'EAP'
in_global.at[103, 'region'] = 'EUCA'
in_global.at[105, 'region'] = 'EUCA'
in_global.at[106, 'region'] = 'EAP'
in_global.at[115, 'region'] = 'EAP'
in_global.at[126, 'region'] = 'EAP'
in_global.at[127, 'region'] = 'EUCA'
in_global.at[137, 'region'] = 'EAP'
in_global.at[142, 'region'] = 'EUCA'
in_global.at[169, 'region'] = 'LAC'
in_global.at[170, 'region'] = 'WEU'
in_global.at[178, 'region'] = 'LAC'
in_global.at[179, 'region'] = 'LAC'
in_global.at[180, 'region'] = 'LAC'
in_global.at[181, 'region'] = 'LAC'
in_global.at[188, 'region'] = 'ESAF'
in_global.at[207, 'region'] = 'LAC'
in_global.at[209, 'region'] = 'LAC'
in_global.at[210, 'region'] = 'MENA'
in_global.at[211, 'region'] = 'MENA'

in_global = in_global[in_global['region'].notna()]
```


```python
in_global.shape
in_global.dtypes
pd.to_numeric(in_global.columns.values[1:41])
in_global = in_global.set_index('Inflow Country')
```


```python
# Setting colors
ascol = 'cornflowerblue'
afcol = 'seagreen'
mencol = 'rosybrown'
nacol = '#C41E3A'
laccol = 'mediumpurple'
eucol = 'goldenrod'
```

# Top Receivers 2020


```python
top2020 = in_global.sort_values(2020, ascending=False)


plt.figure(figsize=(7,5))
plt.rc('font', size=14)   
top2020[2020][:10].plot(kind='bar', ylabel='USD Received (USD billions)', title='Top 10 Remittance Receivers', fontsize=16, color=colors)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend()

pd.DataFrame(top2020[2020]).head(15)

```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2725113329.py:9: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])





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
      <th>2020</th>
    </tr>
    <tr>
      <th>Inflow Country</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>India</th>
      <td>83149.172934</td>
    </tr>
    <tr>
      <th>China</th>
      <td>59506.673349</td>
    </tr>
    <tr>
      <th>Mexico</th>
      <td>42878.274907</td>
    </tr>
    <tr>
      <th>Philippines</th>
      <td>34913.342999</td>
    </tr>
    <tr>
      <th>Egypt, Arab Rep.</th>
      <td>29602.900000</td>
    </tr>
    <tr>
      <th>Pakistan</th>
      <td>26108.000000</td>
    </tr>
    <tr>
      <th>France</th>
      <td>25141.879667</td>
    </tr>
    <tr>
      <th>Bangladesh</th>
      <td>21749.701161</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>17898.798739</td>
    </tr>
    <tr>
      <th>Nigeria</th>
      <td>17207.547306</td>
    </tr>
    <tr>
      <th>Vietnam</th>
      <td>17200.000000</td>
    </tr>
    <tr>
      <th>Ukraine</th>
      <td>15213.000000</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>12693.508977</td>
    </tr>
    <tr>
      <th>Guatemala</th>
      <td>11405.439200</td>
    </tr>
    <tr>
      <th>Russian Federation</th>
      <td>9914.970000</td>
    </tr>
  </tbody>
</table>
</div>




    
![png](output_34_2.png)
    



```python
top2010 = in_global.sort_values(2010, ascending=False)


plt.figure(figsize=(7,5))
plt.rc('font', size=14)
colors10 = ['salmon','blue','yellow','magenta','blueviolet','green','crimson','mediumspringgreen','black','goldenrod']

top2010[2010][:10].plot(kind='bar', ylabel='USD Received (USD billions)', title='Top 10 Remittance Receivers', fontsize=16, color=colors10)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend()

pd.DataFrame(top2010[2010]).head(15)
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1223951428.py:11: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])





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
      <th>2010</th>
    </tr>
    <tr>
      <th>Inflow Country</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>India</th>
      <td>53479.960083</td>
    </tr>
    <tr>
      <th>China</th>
      <td>52459.645879</td>
    </tr>
    <tr>
      <th>Mexico</th>
      <td>22080.259154</td>
    </tr>
    <tr>
      <th>Philippines</th>
      <td>21556.633836</td>
    </tr>
    <tr>
      <th>France</th>
      <td>19898.258274</td>
    </tr>
    <tr>
      <th>Nigeria</th>
      <td>19744.755063</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>12788.812790</td>
    </tr>
    <tr>
      <th>Egypt, Arab Rep.</th>
      <td>12453.100000</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>10993.669270</td>
    </tr>
    <tr>
      <th>Bangladesh</th>
      <td>10850.211617</td>
    </tr>
    <tr>
      <th>Pakistan</th>
      <td>9690.000000</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>8707.390657</td>
    </tr>
    <tr>
      <th>Vietnam</th>
      <td>8260.000000</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>7975.133246</td>
    </tr>
    <tr>
      <th>Poland</th>
      <td>7712.000000</td>
    </tr>
  </tbody>
</table>
</div>




    
![png](output_35_2.png)
    


## Total Remittances Received by Continent


```python
cont = in_global.groupby('continentcode').sum('total_rem').sort_values('total_rem', ascending=False)
contt = pd.DataFrame(cont['total_rem'])
contt['Trillions Received (USD)'] = round((contt['total_rem'] / 1000000),3)
contt = contt.drop('total_rem',axis=1)
contt
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
      <th>Trillions Received (USD)</th>
    </tr>
    <tr>
      <th>continentcode</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AS</th>
      <td>5.082</td>
    </tr>
    <tr>
      <th>EU</th>
      <td>3.245</td>
    </tr>
    <tr>
      <th>NA</th>
      <td>1.374</td>
    </tr>
    <tr>
      <th>AF</th>
      <td>1.294</td>
    </tr>
    <tr>
      <th>SA</th>
      <td>0.357</td>
    </tr>
    <tr>
      <th>OC</th>
      <td>0.119</td>
    </tr>
    <tr>
      <th>CB</th>
      <td>0.003</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure()
plt.rc('font', size=14)    

cont.total_rem.plot(kind='bar', xlabel='Continent', ylabel='Trillions (USD)', legend=False, fontsize=12, color=[eucol,ascol,nacol,afcol,ascol,laccol,laccol], figsize=(10,6))
plt.title('Total Remittances Received by Continent', fontsize=18, y=1.09)

plt.ticklabel_format(style='plain', axis='y')
plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000000])
plt.gca().spines[['top','right']].set_visible(False) 
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/4122970546.py:8: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000000])



    
![png](output_38_1.png)
    


## Total Remittances Received by Region
- Eastern Eu & Central Asia (ECA) | East Asia & Pacific (EAP) | South Asia (SAS) |
- Western Eu (WEU) | Latin Am & Caribbean (LAC) | Middle East & North Af (MENA) | North Am (NA) |
- Eastern & Southern Africa (ESAF) | West & Central Af (WCAF)
#### Source: UNICEF regional classifications (https://data.unicef.org/regionalclassifications/)


```python
regions = in_global.groupby('region').sum('total_rem').sort_values('total_rem', ascending=False)
regionss = pd.DataFrame(regions['total_rem'])
regionss['Trillions Received (USD)'] = round((regionss['total_rem'] / 1000000),3)
regionss = regionss.drop('total_rem',axis=1)
regionss
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
      <th>Trillions Received (USD)</th>
    </tr>
    <tr>
      <th>region</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>WEU</th>
      <td>2.583</td>
    </tr>
    <tr>
      <th>EAP</th>
      <td>2.381</td>
    </tr>
    <tr>
      <th>SAS</th>
      <td>1.989</td>
    </tr>
    <tr>
      <th>LAC</th>
      <td>1.554</td>
    </tr>
    <tr>
      <th>MENA</th>
      <td>1.124</td>
    </tr>
    <tr>
      <th>EUCA</th>
      <td>0.985</td>
    </tr>
    <tr>
      <th>WCAF</th>
      <td>0.497</td>
    </tr>
    <tr>
      <th>ESAF</th>
      <td>0.183</td>
    </tr>
    <tr>
      <th>NA</th>
      <td>0.180</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14) 

regionss.plot(kind='bar', xlabel='Region', ylabel='Trillions Received (USD)', fontsize=12, color=['b','k','g','m','r','c','y'], legend=False)
plt.title('Total Remittances Received by Region', fontsize=18, y=1.09)
plt.gca().spines[['top', 'right']].set_visible(False)


plt.close()
# the contt & regionss version of data are cleaner but below figures allow easier color customization
```


    <Figure size 504x360 with 0 Axes>



```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(14, 6), sharey=True)
fig.tight_layout()

cont.total_rem.sort_values(ascending=False).plot(kind='bar', ax=axes[0], title='Total Remittances Received by Continent', xlabel='Continent', ylabel='Remittances Received (USD trillions)', fontsize=12, color=[ascol,eucol,nacol,afcol,laccol,ascol,laccol])
regions.total_rem.sort_values(ascending=False).plot(kind='bar', ax=axes[1], title='Total Remittances Received by Region', xlabel='Region', ylabel='Remittances Received (USD trillions)', fontsize=12, color=[eucol,ascol,ascol,laccol,mencol, eucol,afcol,afcol,nacol])

plt.ticklabel_format(style='plain', axis='y')
plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2445342661.py:8: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000000])



    
![png](output_42_1.png)
    



```python
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(15, 6), sharey=True)
fig.tight_layout()

cont.total_rem.sort_values(ascending=False).plot(kind='bar', ax=axes[0,0], title='Total Remittances Received by Continent', xlabel='Continent', ylabel='Remittances Received (USD billions)', fontsize=12)
contt.plot(kind='bar', xlabel='Continent', ylabel='Trillions (USD)', ax=axes[1,0], legend=False, fontsize=12, color='black')

regions.total_rem.sort_values(ascending=False).plot(kind='bar', ax=axes[0,1], title='Total Remittances Received by Region', xlabel='Region', ylabel='Remittances Received (USD trillions)', fontsize=12, color=['b','k','g','m','r','c','y'])
regionss.plot(kind='bar', xlabel='Region', ylabel='Trillions Received (USD)', ax=axes[1,1], fontsize=12, color=['b','k','g','m','r','c','y'], legend=False)

fig.align_ylabels()

plt.close()
# contt/regionss code is cleaner but cont/regions allowed easier color customization
```

## Remittances Received over Time


```python
regionss = regions.drop('remit_gdp', axis=1).drop('total_rem', axis=1)
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(9):
    regionss.iloc[i].plot(title='Remittances Received over Time', xlabel='Year', ylabel='Annual Remittances (USD billions)')

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best',fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2452573266.py:9: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_46_1.png)
    


### Ukraine probe


```python
inrem0.drop(['remit_gdp', 'total_rem', 'pct_gdp'], axis=1).iloc[200].plot()
inrem0.xs('Ukraine')[2020]
plt.close('all')    # close fig
```

# Asia Analysis


```python
asia = in_global.loc[in_global.continentcode == 'AS']
asia = asia.sort_values('total_rem', ascending=False)
ascoll = ['#000080','#0F52BA','#1F51FF','#4169E1','#6082B6','#4682B4','#87CEEB','#ADD8E6','#A7C7E7','#CCCCFF']
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)   
asia.total_rem[:10].plot(kind='bar', color=ascoll, title='Total Remittances Received', ylabel='USD (billions)', fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2054047277.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_51_1.png)
    


## Trends over Time


```python
asiaa = asia.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (Asia)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    asiaa.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/3015819980.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_53_1.png)
    


## East Asia & the Pacific Analysis


```python
eap = in_global.loc[in_global.region == 'EAP']
eap = eap.sort_values('total_rem', ascending=False)
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14) 
eap.total_rem[:10].plot(kind='bar', title='Total Remittances Received (EAP)', ylabel='Remittances Received (USD billions)', fontsize=12, color=ascoll)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/3134394110.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_56_1.png)
    


### EAP Trends over Time


```python
eapp = eap.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

# Formatting
plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (EAP)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    eapp.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/4284130395.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_58_1.png)
    


## South Asia Analysis


```python
sas = in_global.loc[in_global.region == 'SAS']
sas = sas.sort_values('total_rem', ascending=False)
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14) 
sas.total_rem[:10].plot(kind='bar', title='Total Remittances Received (SAS)', ylabel='Remittances Received (USD billions)', fontsize=12, color=ascoll)

plt.gca().spines[['top', 'right']].set_visible(False)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1969632671.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_61_1.png)
    


### SAS Trends over time


```python
sass = sas.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (SAS)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(len(SAS)):
    sass.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1244387317.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_63_1.png)
    


## Middle East & North Africa Analysis


```python
mena = in_global.loc[in_global.region == 'MENA']
mena = mena.sort_values('total_rem', ascending=False)
mencoll = ['#770737','#9F2B68','#DE3163','#FF10F0','#DA70D6','#FF69B4','#E37383','#F8C8DC','#F3CFC6','#F2D2BD']
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)   
mena.total_rem[:10].plot(kind='bar', title='Total Remittances Received (MENA)', ylabel='Remittances Received (USD billions)', color=mencoll, fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1781216465.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_66_1.png)
    


### MENA Trends over Time


```python
menaa = mena.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

# Formatting
plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (MENA)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    menaa.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/4280755982.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_68_1.png)
    


# Europe Analysis

## Western Europe  Analysis


```python
weu = in_global.loc[in_global.region == 'WEU']
weu = weu.sort_values('total_rem', ascending=False)
eucoll = ['#CD7F32','#CC5500','#F28C28','#E3963E','#FFBF00','#DAA520','#FFC000','#FFEA00','#FAC898','#FFE5B4']
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)   
weu.total_rem[:10].plot(kind='bar', title='Total Remittances Received (WEU)', ylabel='USD billions', color=eucoll, fontsize=12)
plt.gca().spines[['top', 'right']].set_visible(False)  

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1203878996.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_72_1.png)
    



```python
weuu = weu.rename(columns={'2021e':2021}).drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)
# Formatting
plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (WEU)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    weuu.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2950670687.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_73_1.png)
    


## Eastern Europe & Central Asia Analysis


```python
euca = in_global.loc[in_global.region == 'EUCA']
euca = euca.sort_values('total_rem', ascending=False)
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)   
euca.total_rem[:10].plot(kind='bar', title='Total Remittances Received (EUCA)', ylabel='Remittances Received (USD billions)', color=eucoll, fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/977072418.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_76_1.png)
    


### EUCA Trends over time


```python
eucaa = euca.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (EUCA)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    eucaa.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/730051698.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_78_1.png)
    



```python
plt.close('all')
# overlap between senders and receivers
# what are the top migrant groups in SEDING countries
```

## Latin America & Caribbean


```python
lac = in_global.loc[in_global.region == 'LAC']
lac = lac.sort_values('total_rem', ascending=False)
laccoll = ['#02000A','#120632','#2E165B','#532D84','#7E4EAC','#AF77D5','#CF9FFF','#E0B0FF','#da8ee7','#e8bcf0','#BDB5D5']
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)   
lac.total_rem[:11].plot(kind='bar', color=laccoll, title='Total Remittances Received (LAC)', ylabel='Remittances Received (USD billions)', fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2339113439.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_82_1.png)
    


### LAC Trends over time


```python
lacc = lac.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (LAC)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    lacc.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1632443053.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_84_1.png)
    


## Africa Analysis


```python
africa = in_global.loc[in_global.continentcode == 'AF']
africa = africa.sort_values('total_rem', ascending=False)
afcoll = ['#355E3B','#00A36C','#2AAA8A','#2e8b57','#228b22','#32cd32','#b2ec5d','#c5e384','#AFE1AF','#e9ffdb']
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)   
africa.total_rem[:10].plot(kind='bar', color=afcoll, title='Total Remittances Received (Africa)', ylabel='Remittances Received (USD billions)', fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/3966738851.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_87_1.png)
    


### Africa Trends over time


```python
africaa = africa.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (Africa)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    africaa.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2584971811.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_89_1.png)
    


## West & Central Africa Analysis


```python
wcaf = in_global.loc[in_global.region == 'WCAF']
wcaf = wcaf.sort_values('total_rem', ascending=False)
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)
wcaf.total_rem[:10].plot(kind='bar', title='Total Remittances Received (WCAF)', ylabel='Remittances Received (USD billions)', color=afcoll, fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/127004185.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_92_1.png)
    


### WCAF Trends over time


```python
wcaff = wcaf.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (WCAF)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    wcaff.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='best', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/797875498.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_94_1.png)
    


## East & Southern Africa Analysis


```python
esaf = in_global.loc[in_global.region == 'ESAF']
esaf = esaf.sort_values('total_rem', ascending=False)
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)
esaf.total_rem[:10].plot(kind='bar', title='Total Remittances Received (ESAF)', ylabel='Remittances Received (USD billions)', color=afcoll, fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2233040147.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_97_1.png)
    


### ESAF Trends over time


```python
esaff = esaf.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (ESAF)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(10):
    esaff.iloc[i].plot(fontsize=12)

plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='upper left', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1754149688.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_99_1.png)
    


# NA Analysis


```python
naa = in_global.loc[in_global.region == 'NA']
naa = naa.sort_values('total_rem', ascending=False)
nacoll = ['#C41E3A', '#FA5F55']
```


```python
plt.figure(figsize=(7,5))
plt.rc('font', size=14)
naa.total_rem[:10].plot(kind='bar', title='Total Remittances Received (NA)', ylabel='Remittances Received (USD billions)', color=nacoll, fontsize=12)

plt.gca().spines[['top', 'right']].set_visible(False)  
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/563567195.py:6: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_102_1.png)
    


## NA Trends over Time


```python
naa = naa.drop(['pct_gdp','remit_gdp','total_rem','continentcode','capital','population_x','currencycode','languages','geonameid','continent','region'], axis=1)

plt.figure(figsize=(7,5))
plt.rc('font', size=14)    
plt.axes(title='Trends over time (NA)', xlabel='Year', ylabel='Annual Remittances Received (USD billions)')
plt.gca().spines[['top', 'right']].set_visible(False)    
plt.ticklabel_format(style='plain', axis='y')

for i in range(len(NA)):
    naa.iloc[i].plot()

plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.legend(loc='upper left', fontsize=10)
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1753334485.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.1f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_104_1.png)
    



```python
plt.close('all')
```

# GLOBAL WORLDVIEW


```python
import geopandas as gpd
import mapclassify
import plotly.graph_objs as go 
world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))
world = world.rename(columns={'name':'country'})
countries = countries.rename({'name':'country'}, axis=1)
orig_countries = in_global.reset_index().rename({'Inflow Country':'country'}, axis=1)
```

    /Users/Jane/opt/anaconda3/lib/python3.9/site-packages/geopandas/_compat.py:111: UserWarning: The Shapely GEOS version (3.10.2-CAPI-1.16.0) is incompatible with the GEOS version PyGEOS was compiled with (3.10.1-CAPI-1.16.0). Conversions between both will be slow.
      warnings.warn(



```python
foo = pd.merge(countries, world, on='country', how='right')
# merging countries with world to obtain geometry column from world
```


```python
# Renaming to make foo country names in merge match original list to maintain necessary geometries
foo.at[4, 'country'] = 'United States'
foo.at[11, 'country'] = 'Congo, Dem. Rep.'
foo.at[17, 'country'] = 'Dominican Republic'
foo.at[18, 'country'] = 'Russian Federation'
foo.at[19, 'country'] = 'Bahamas, The'
foo.at[40, 'country'] = 'Venezuela, RB'
foo.at[60, 'country'] = "Cote d'Ivoire"
foo.at[66, 'country'] = 'Central African Republic'
foo.at[69, 'country'] = 'Equatorial Guinea'
foo.at[73, 'country'] = 'Eswatini'
foo.at[80, 'country'] = 'Gambia, The'
orig_countries.at[88, 'country'] = 'Iran'
orig_countries.at[99, 'country'] = 'South Korea'
orig_countries.at[102, 'country'] = 'Kyrgyzstan'
orig_countries.at[206, 'country'] = 'Yemen'
foo.at[108, 'country'] = 'Syrian Arab Republic'
foo.at[149, 'country'] = 'Brunei Darussalam'
foo.at[152, 'country'] = 'Slovak Republic'
foo.at[153, 'country'] = 'Czech Republic'
foo.at[163, 'country'] = 'Egypt, Arab Rep.'
foo.at[167, 'country'] = 'Somalia'
foo.at[170, 'country'] = 'Bosnia and Herzegovina'
foo.at[171, 'country'] = 'North Macedonia'
foo.at[176, 'country'] = 'South Sudan'
foo.at[160, 'country'] = 'Cyprus'
```


```python
new_world = pd.merge(foo, orig_countries, on='country', how='left')
new_world = gpd.GeoDataFrame(new_world, geometry='geometry')    # convert pandas df to geodataframe for plotting
```


```python
new_world[new_world.geometry.isna()]    # all items now have geometries
new_world[new_world.total_rem < 1]
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
      <th>geonameid_x</th>
      <th>country</th>
      <th>iso</th>
      <th>iso3</th>
      <th>isonumeric</th>
      <th>fips</th>
      <th>continentcode_x</th>
      <th>capital_x</th>
      <th>areakm2</th>
      <th>population</th>
      <th>...</th>
      <th>remit_gdp</th>
      <th>total_rem</th>
      <th>continentcode_y</th>
      <th>capital_y</th>
      <th>population_x</th>
      <th>currencycode_y</th>
      <th>languages_y</th>
      <th>geonameid_y</th>
      <th>region</th>
      <th>continent_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19</th>
      <td>3572887</td>
      <td>Bahamas, The</td>
      <td>BS</td>
      <td>BHS</td>
      <td>44</td>
      <td>BF</td>
      <td>NA</td>
      <td>Nassau</td>
      <td>13940</td>
      <td>301790</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>CB</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>LAC</td>
      <td>Caribbean</td>
    </tr>
    <tr>
      <th>47</th>
      <td>3562981</td>
      <td>Cuba</td>
      <td>CU</td>
      <td>CUB</td>
      <td>192</td>
      <td>CU</td>
      <td>NA</td>
      <td>Havana</td>
      <td>110860</td>
      <td>11423000</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>NA</td>
      <td>Havana</td>
      <td>11423000</td>
      <td>CUP</td>
      <td>es-CU</td>
      <td>3562981</td>
      <td>LAC</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>66</th>
      <td>NaN</td>
      <td>Central African Republic</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.509873</td>
      <td>AF</td>
      <td>Bangui</td>
      <td>4844927</td>
      <td>XAF</td>
      <td>fr-CF,sg,ln,kg</td>
      <td>239880</td>
      <td>WCAF</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>84</th>
      <td>290557</td>
      <td>United Arab Emirates</td>
      <td>AE</td>
      <td>ARE</td>
      <td>784</td>
      <td>AE</td>
      <td>AS</td>
      <td>Abu Dhabi</td>
      <td>82880</td>
      <td>4975593</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>AS</td>
      <td>Abu Dhabi</td>
      <td>4975593</td>
      <td>AED</td>
      <td>ar-AE,fa,en,hi,ur</td>
      <td>290557</td>
      <td>MENA</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>149</th>
      <td>1820814</td>
      <td>Brunei Darussalam</td>
      <td>BN</td>
      <td>BRN</td>
      <td>96</td>
      <td>BX</td>
      <td>AS</td>
      <td>Bandar Seri Begawan</td>
      <td>5770</td>
      <td>395027</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>AS</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EAP</td>
      <td>Asia</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 75 columns</p>
</div>



# Global Worldview


```python
new_world.plot(column='total_rem', cmap='magma_r', figsize=(25,25), 
               legend=True, legend_kwds={'label': 'USD trillions', 'shrink': 0.4},
               edgecolor='grey', missing_kwds={'label': 'No Data', 'color':'dimgrey'})
# not optimized bc Jenks optimization creates bins that hide the slight variation between countries (ie. ~all Africa+LAC same color)
plt.title('Total Remittances Received (trillions)', fontsize=22)
plt.axis('off')

new_world.plot(column='total_rem', cmap='YlOrRd', scheme='jenkscaspall', 
               legend=True, legend_kwds={'title': 'USD trillions'},
               figsize=(25,25), edgecolor='grey', missing_kwds={'label': 'No Data', 'color':'dimgrey'})
plt.title('Total Remittances Received (normalized)', fontsize=25)
plt.axis('off')
plt.show()
```


    
![png](output_113_0.png)
    



    
![png](output_113_1.png)
    


The Jenks optimization method (natural breaks classification) is a data clustering method designed to determine the best arrangement of values into different classes. This is done by seeking to minimize each class's average deviation from the class mean, while maximizing each class's deviation from the means of the other classes (ie. the method reduces variance within classes and maximizes the variance between classes)

## NA close-up


```python
na = new_world[new_world["region"] == "NA"]
na = gpd.GeoDataFrame(na, geometry='geometry')
na = na.set_index('country').sort_values('total_rem', ascending=False)
na['billions'] = na.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(15, 6))
fig.tight_layout()


na.plot(column='billions', cmap='PuBuGn', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (NA)', fontsize=20)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

na.total_rem[:11].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='#204B53', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=20)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1763784384.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_117_1.png)
    


## LAC close-up


```python
lacc = new_world[new_world["region"] == "LAC"]
lacc = gpd.GeoDataFrame(lacc, geometry='geometry')
lacc['billions'] = lacc.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(15, 6))
fig.tight_layout()


lacc.plot(column='billions', cmap='Purples', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (LAC)', fontsize=20)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

lac.total_rem[:11].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='mediumpurple', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=20)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1664422355.py:12: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_120_1.png)
    


## WEU close-up


```python
weu = new_world[new_world["region"] == "WEU"]
weu = gpd.GeoDataFrame(weu, geometry='geometry')
weu['billions'] = weu.total_rem/1000
weu = weu.set_index('country').sort_values('total_rem', ascending=False)
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(15, 6))
fig.tight_layout()

weu.plot(column='billions', cmap='YlOrBr', legend=True, ax=axes[0], figsize=(10,5))
axes[0].set_title('Total Remittances Received (WEU)', fontsize=20)
axes[0].set_xlim(-27, 35)
axes[0].set_ylim(34, 82)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

weu.total_rem[:11].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='goldenrod', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=20)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/918542011.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_123_1.png)
    


## EUCA close-up


```python
euca = new_world[new_world["region"] == "EUCA"]
euca = gpd.GeoDataFrame(euca, geometry='geometry')
euca = euca.set_index('country').sort_values('total_rem', ascending=False)
euca['billions'] = euca.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(14, 6))
fig.tight_layout()

euca.plot(column='billions', cmap='Oranges', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (EUCA)', fontsize=24)
axes[0].set_xlim(0, 200)
axes[0].set_ylim(20, 100)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

euca.total_rem[:8].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='darkorange', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=24)   
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/219950185.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_126_1.png)
    


## MENA close-up


```python
mena = new_world[new_world["region"] == "MENA"]
mena = gpd.GeoDataFrame(mena, geometry='geometry')
mena = mena.set_index('country').sort_values('total_rem', ascending=False)
mena['billions'] = mena.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(14, 6))
fig.tight_layout()

mena.plot(column='billions', cmap='PuRd', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (MENA)', fontsize=24)
axes[0].set_xlim(-30, 80)
axes[0].set_ylim(0, 55)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

mena.total_rem[:8].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='rosybrown', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=24)   
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1423569622.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_129_1.png)
    


## WCAF close-up


```python
wcaf = new_world[new_world["region"] == "WCAF"]
wcaf = gpd.GeoDataFrame(wcaf, geometry='geometry')
wcaf = wcaf.set_index('country').sort_values('total_rem', ascending=False)
wcaf['billions'] = wcaf.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(15, 7))
fig.tight_layout()

wcaf.plot(column='billions', cmap='YlGn', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (WCAF)', fontsize=20)
axes[0].set_xlim(-25,40)
axes[0].set_ylim(-30, 40)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

wcaf.total_rem[:11].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='seagreen', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=20)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/2658026874.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_132_1.png)
    


## ESAF close-up


```python
esaf = new_world[new_world["region"] == "ESAF"]
esaf = gpd.GeoDataFrame(esaf, geometry='geometry')
esaf = esaf.set_index('country').sort_values('total_rem', ascending=False)
esaf['billions'] = esaf.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(16, 7))
fig.tight_layout()

esaf.plot(column='billions', cmap='YlGn', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (ESAF)', fontsize=20)
axes[0].set_xlim(-10,70)
axes[0].set_ylim(-60, 45)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

esaf.total_rem[:11].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='seagreen', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=20)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1526238383.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_135_1.png)
    


## EAP close-up


```python
eap = new_world[new_world["region"] == "EAP"]
eap = gpd.GeoDataFrame(eap, geometry='geometry')
eap = eap.set_index('country').sort_values('total_rem', ascending=False)
eap['billions'] = eap.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(14, 6))
fig.tight_layout()

eap.plot(column='billions', cmap='Blues', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (EAP)', fontsize=20)
axes[0].set_xlim(70,180)
axes[0].set_ylim(-50, 60)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

eap.total_rem[:11].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='cornflowerblue', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=20)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/3844058500.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_138_1.png)
    


## SAS close-up


```python
sas = new_world[new_world["region"] == "SAS"]
sas = gpd.GeoDataFrame(sas, geometry='geometry')
sas = sas.set_index('country').sort_values('total_rem', ascending=False)
sas['billions'] = sas.total_rem/1000
```


```python
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(14, 6))
fig.tight_layout()

sas.plot(column='billions', cmap='Blues', legend=True, ax=axes[0])
axes[0].set_title('Total Remittances Received (SAS)', fontsize=20)
axes[0].set_xlim(50,106)
axes[0].set_ylim(-5, 50)
axes[0].get_xaxis().set_visible(False)
axes[0].get_yaxis().set_visible(False)

sas.total_rem[:11].plot(kind='bar', ax=axes[1], ylabel='USD billions', color='cornflowerblue', fontsize=18)
plt.title('Total Remittances Received (USD billions)', fontsize=20)
plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])
plt.show()
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/561525936.py:13: UserWarning: FixedFormatter should only be used together with FixedLocator
      plt.gca().set_yticklabels(['{:,.0f}'.format(x) for x in (plt.gca().get_yticks())/1000])



    
![png](output_141_1.png)
    



```python
# Bubble map w/ remit. as proportional bubble sizes
centroids = new_world.copy()
centroids.geometry = new_world.centroid

ax = new_world.plot(facecolor='w', edgecolor='k', figsize=(20,20))
centroids.plot(markersize=new_world['total_rem']/200, ax=ax)
# centroid size reflects magnitude of remit received
plt.close('all')
```

    /var/folders/s4/dp397f9j3zs5ymr83ltkv2m80000gn/T/ipykernel_89780/1248198644.py:3: UserWarning: Geometry is in a geographic CRS. Results from 'centroid' are likely incorrect. Use 'GeoSeries.to_crs()' to re-project geometries to a projected CRS before this operation.
    
      centroids.geometry = new_world.centroid



```python

```
