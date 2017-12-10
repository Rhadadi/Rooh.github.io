---
layout: post
title: Pandas and Panel Data Application!
published: true
---

In this post, I am going through a lecture note I found on Quantecon page.

Source: [Quantecon](https://lectures.quantecon.org/py/pandas_panel.html)

```python
import pandas as pd
pd.set_option('display.max_columns', 6)
# Reduce decimal points to 2

pd.options.display.float_format = '{:,.2f}'.format

realwage = pd.read_csv(
    'https://github.com/QuantEcon/QuantEcon.lectures.code/raw/master/pandas_panel/realwage.csv'
)
```


```python
realwage.head()  # Show first 5 rows
```

<script src="https://gist.github.com/Rhadadi/eefdb3651c75225f84ae6f83bc9c49ac.js"></script>

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Time</th>
      <th>Country</th>
      <th>Series</th>
      <th>Pay period</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2006-01-01</td>
      <td>Ireland</td>
      <td>In 2015 constant prices at 2015 USD PPPs</td>
      <td>Annual</td>
      <td>17,132.44</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2007-01-01</td>
      <td>Ireland</td>
      <td>In 2015 constant prices at 2015 USD PPPs</td>
      <td>Annual</td>
      <td>18,100.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2008-01-01</td>
      <td>Ireland</td>
      <td>In 2015 constant prices at 2015 USD PPPs</td>
      <td>Annual</td>
      <td>17,747.41</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2009-01-01</td>
      <td>Ireland</td>
      <td>In 2015 constant prices at 2015 USD PPPs</td>
      <td>Annual</td>
      <td>18,580.14</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2010-01-01</td>
      <td>Ireland</td>
      <td>In 2015 constant prices at 2015 USD PPPs</td>
      <td>Annual</td>
      <td>18,755.83</td>
    </tr>
  </tbody>
</table>
</div>



## pivot_table


```python
realwage = realwage.pivot_table(
    values='value', index='Time', columns=['Country', 'Series', 'Pay period'])
realwage.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Country</th>
      <th colspan="3" halign="left">Australia</th>
      <th>...</th>
      <th colspan="3" halign="left">United States</th>
    </tr>
    <tr>
      <th>Series</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD PPPs</th>
      <th>In 2015 constant prices at 2015 USD exchange rates</th>
      <th>...</th>
      <th>In 2015 constant prices at 2015 USD PPPs</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th>Pay period</th>
      <th>Annual</th>
      <th>Hourly</th>
      <th>Annual</th>
      <th>...</th>
      <th>Hourly</th>
      <th>Annual</th>
      <th>Hourly</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>20,410.65</td>
      <td>10.33</td>
      <td>23,826.64</td>
      <td>...</td>
      <td>6.05</td>
      <td>12,594.40</td>
      <td>6.05</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>21,087.57</td>
      <td>10.67</td>
      <td>24,616.84</td>
      <td>...</td>
      <td>6.24</td>
      <td>12,974.40</td>
      <td>6.24</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>20,718.24</td>
      <td>10.48</td>
      <td>24,185.70</td>
      <td>...</td>
      <td>6.78</td>
      <td>14,097.56</td>
      <td>6.78</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>20,984.77</td>
      <td>10.62</td>
      <td>24,496.84</td>
      <td>...</td>
      <td>7.58</td>
      <td>15,756.42</td>
      <td>7.58</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>20,879.33</td>
      <td>10.57</td>
      <td>24,373.76</td>
      <td>...</td>
      <td>7.88</td>
      <td>16,391.31</td>
      <td>7.88</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 128 columns</p>
</div>



## to_datetime


```python
realwage.index = pd.to_datetime(realwage.index)
realwage.index
```




    DatetimeIndex(['2006-01-01', '2007-01-01', '2008-01-01', '2009-01-01',
                   '2010-01-01', '2011-01-01', '2012-01-01', '2013-01-01',
                   '2014-01-01', '2015-01-01', '2016-01-01'],
                  dtype='datetime64[ns]', name='Time', freq=None)



## stack


```python
realwage.stack(level='Country')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Series</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD PPPs</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th></th>
      <th>Pay period</th>
      <th>Annual</th>
      <th>Hourly</th>
      <th>Annual</th>
      <th>Hourly</th>
    </tr>
    <tr>
      <th>Time</th>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2006-01-01</th>
      <th>Australia</th>
      <td>20,410.65</td>
      <td>10.33</td>
      <td>23,826.64</td>
      <td>12.06</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>21,042.28</td>
      <td>10.09</td>
      <td>20,228.74</td>
      <td>9.70</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>3,310.51</td>
      <td>1.41</td>
      <td>2,032.87</td>
      <td>0.87</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>13,649.69</td>
      <td>6.56</td>
      <td>14,335.12</td>
      <td>6.89</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>5,201.65</td>
      <td>2.22</td>
      <td>3,333.76</td>
      <td>1.42</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">2016-01-01</th>
      <th>Slovenia</th>
      <td>14,520.80</td>
      <td>6.96</td>
      <td>10,533.06</td>
      <td>5.05</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>12,317.41</td>
      <td>5.06</td>
      <td>10,191.91</td>
      <td>4.19</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>12,074.76</td>
      <td>5.79</td>
      <td>6,741.96</td>
      <td>3.23</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>17,568.33</td>
      <td>8.44</td>
      <td>21,352.73</td>
      <td>10.26</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>14,892.12</td>
      <td>7.16</td>
      <td>14,892.12</td>
      <td>7.16</td>
    </tr>
  </tbody>
</table>
<p>335 rows × 4 columns</p>
</div>




```python
realwage['2015'].stack(level='Country')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Series</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD PPPs</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th></th>
      <th>Pay period</th>
      <th>Annual</th>
      <th>Hourly</th>
      <th>Annual</th>
      <th>Hourly</th>
    </tr>
    <tr>
      <th>Time</th>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="11" valign="top">2015-01-01</th>
      <th>Australia</th>
      <td>21,715.53</td>
      <td>10.99</td>
      <td>25,349.90</td>
      <td>12.83</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>21,588.12</td>
      <td>10.35</td>
      <td>20,753.48</td>
      <td>9.95</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>4,628.63</td>
      <td>2.00</td>
      <td>2,842.28</td>
      <td>1.21</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>16,536.83</td>
      <td>7.95</td>
      <td>17,367.24</td>
      <td>8.35</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>6,633.56</td>
      <td>2.80</td>
      <td>4,251.49</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Slovenia</th>
      <td>14,512.81</td>
      <td>6.96</td>
      <td>10,527.26</td>
      <td>5.05</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>12,170.47</td>
      <td>5.00</td>
      <td>10,070.33</td>
      <td>4.14</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>10,062.42</td>
      <td>4.82</td>
      <td>5,618.36</td>
      <td>2.69</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>17,125.45</td>
      <td>8.23</td>
      <td>20,814.46</td>
      <td>10.01</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>15,080.00</td>
      <td>7.25</td>
      <td>15,080.00</td>
      <td>7.25</td>
    </tr>
  </tbody>
</table>
<p>32 rows × 4 columns</p>
</div>




```python
realwage_c = realwage['2015'].stack(level=[1, 2]).transpose()  # no time index
realwage_c
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Time</th>
      <th colspan="4" halign="left">2015-01-01</th>
    </tr>
    <tr>
      <th>Series</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD PPPs</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th>Pay period</th>
      <th>Annual</th>
      <th>Hourly</th>
      <th>Annual</th>
      <th>Hourly</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Australia</th>
      <td>21,715.53</td>
      <td>10.99</td>
      <td>25,349.90</td>
      <td>12.83</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>21,588.12</td>
      <td>10.35</td>
      <td>20,753.48</td>
      <td>9.95</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>4,628.63</td>
      <td>2.00</td>
      <td>2,842.28</td>
      <td>1.21</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>16,536.83</td>
      <td>7.95</td>
      <td>17,367.24</td>
      <td>8.35</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>6,633.56</td>
      <td>2.80</td>
      <td>4,251.49</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Slovenia</th>
      <td>14,512.81</td>
      <td>6.96</td>
      <td>10,527.26</td>
      <td>5.05</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>12,170.47</td>
      <td>5.00</td>
      <td>10,070.33</td>
      <td>4.14</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>10,062.42</td>
      <td>4.82</td>
      <td>5,618.36</td>
      <td>2.69</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>17,125.45</td>
      <td>8.23</td>
      <td>20,814.46</td>
      <td>10.01</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>15,080.00</td>
      <td>7.25</td>
      <td>15,080.00</td>
      <td>7.25</td>
    </tr>
  </tbody>
</table>
<p>32 rows × 4 columns</p>
</div>



## .xs


```python
realwage_f = realwage.xs(
    ('Hourly', 'In 2015 constant prices at 2015 USD exchange rates'),
    level=('Pay period', 'Series'),
    axis=1)
realwage.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Country</th>
      <th colspan="3" halign="left">Australia</th>
      <th>...</th>
      <th colspan="3" halign="left">United States</th>
    </tr>
    <tr>
      <th>Series</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD PPPs</th>
      <th>In 2015 constant prices at 2015 USD exchange rates</th>
      <th>...</th>
      <th>In 2015 constant prices at 2015 USD PPPs</th>
      <th colspan="2" halign="left">In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th>Pay period</th>
      <th>Annual</th>
      <th>Hourly</th>
      <th>Annual</th>
      <th>...</th>
      <th>Hourly</th>
      <th>Annual</th>
      <th>Hourly</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>20,410.65</td>
      <td>10.33</td>
      <td>23,826.64</td>
      <td>...</td>
      <td>6.05</td>
      <td>12,594.40</td>
      <td>6.05</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>21,087.57</td>
      <td>10.67</td>
      <td>24,616.84</td>
      <td>...</td>
      <td>6.24</td>
      <td>12,974.40</td>
      <td>6.24</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>20,718.24</td>
      <td>10.48</td>
      <td>24,185.70</td>
      <td>...</td>
      <td>6.78</td>
      <td>14,097.56</td>
      <td>6.78</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>20,984.77</td>
      <td>10.62</td>
      <td>24,496.84</td>
      <td>...</td>
      <td>7.58</td>
      <td>15,756.42</td>
      <td>7.58</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>20,879.33</td>
      <td>10.57</td>
      <td>24,373.76</td>
      <td>...</td>
      <td>7.88</td>
      <td>16,391.31</td>
      <td>7.88</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 128 columns</p>
</div>




```python
realwage_f.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Country</th>
      <th>Australia</th>
      <th>Belgium</th>
      <th>Brazil</th>
      <th>...</th>
      <th>Turkey</th>
      <th>United Kingdom</th>
      <th>United States</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>12.06</td>
      <td>9.70</td>
      <td>0.87</td>
      <td>...</td>
      <td>2.27</td>
      <td>9.81</td>
      <td>6.05</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>12.46</td>
      <td>9.82</td>
      <td>0.92</td>
      <td>...</td>
      <td>2.26</td>
      <td>10.07</td>
      <td>6.24</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>12.24</td>
      <td>9.87</td>
      <td>0.96</td>
      <td>...</td>
      <td>2.22</td>
      <td>10.04</td>
      <td>6.78</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>12.40</td>
      <td>10.21</td>
      <td>1.03</td>
      <td>...</td>
      <td>2.28</td>
      <td>10.15</td>
      <td>7.58</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>12.34</td>
      <td>10.05</td>
      <td>1.08</td>
      <td>...</td>
      <td>2.30</td>
      <td>9.96</td>
      <td>7.88</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>




```python
realwage.xs(('Annual', 'Brazil'), level=[2, 0], axis=1)  # () not []
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Series</th>
      <th>In 2015 constant prices at 2015 USD PPPs</th>
      <th>In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th>Time</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2006-01-01</th>
      <td>3,310.51</td>
      <td>2,032.87</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>3,525.45</td>
      <td>2,164.86</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>3,664.39</td>
      <td>2,250.18</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>3,934.77</td>
      <td>2,416.21</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>4,145.69</td>
      <td>2,545.73</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2012-01-01</th>
      <td>4,498.38</td>
      <td>2,762.30</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>4,616.93</td>
      <td>2,835.10</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>4,636.71</td>
      <td>2,847.25</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>4,628.63</td>
      <td>2,842.28</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>4,753.60</td>
      <td>2,919.02</td>
    </tr>
  </tbody>
</table>
<p>11 rows × 2 columns</p>
</div>




```python
realwage.xs(('Annual', 'Brazil'), level=[2, 0], axis=1)  # () not []
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Series</th>
      <th>In 2015 constant prices at 2015 USD PPPs</th>
      <th>In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th>Time</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2006-01-01</th>
      <td>3,310.51</td>
      <td>2,032.87</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>3,525.45</td>
      <td>2,164.86</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>3,664.39</td>
      <td>2,250.18</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>3,934.77</td>
      <td>2,416.21</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>4,145.69</td>
      <td>2,545.73</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2012-01-01</th>
      <td>4,498.38</td>
      <td>2,762.30</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>4,616.93</td>
      <td>2,835.10</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>4,636.71</td>
      <td>2,847.25</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>4,628.63</td>
      <td>2,842.28</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>4,753.60</td>
      <td>2,919.02</td>
    </tr>
  </tbody>
</table>
<p>11 rows × 2 columns</p>
</div>




```python
realwage_c.xs('Annual', level='Pay period', axis=1)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Time</th>
      <th colspan="2" halign="left">2015-01-01</th>
    </tr>
    <tr>
      <th>Series</th>
      <th>In 2015 constant prices at 2015 USD PPPs</th>
      <th>In 2015 constant prices at 2015 USD exchange rates</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Australia</th>
      <td>21,715.53</td>
      <td>25,349.90</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>21,588.12</td>
      <td>20,753.48</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>4,628.63</td>
      <td>2,842.28</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>16,536.83</td>
      <td>17,367.24</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>6,633.56</td>
      <td>4,251.49</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Slovenia</th>
      <td>14,512.81</td>
      <td>10,527.26</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>12,170.47</td>
      <td>10,070.33</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>10,062.42</td>
      <td>5,618.36</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>17,125.45</td>
      <td>20,814.46</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>15,080.00</td>
      <td>15,080.00</td>
    </tr>
  </tbody>
</table>
<p>32 rows × 2 columns</p>
</div>




```python
worlddata = pd.read_csv(
    'https://github.com/QuantEcon/QuantEcon.lectures.code/raw/master/pandas_panel/countries.csv',
    sep=';')
worlddata.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country (en)</th>
      <th>Country (de)</th>
      <th>Country (local)</th>
      <th>...</th>
      <th>Deathrate</th>
      <th>Life expectancy</th>
      <th>Url</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>Afghanistan</td>
      <td>Afganistan/Afqanestan</td>
      <td>...</td>
      <td>13.70</td>
      <td>51.30</td>
      <td>https://www.laenderdaten.info/Asien/Afghanista...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Egypt</td>
      <td>Ägypten</td>
      <td>Misr</td>
      <td>...</td>
      <td>4.70</td>
      <td>72.70</td>
      <td>https://www.laenderdaten.info/Afrika/Aegypten/...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Åland Islands</td>
      <td>Ålandinseln</td>
      <td>Åland</td>
      <td>...</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>https://www.laenderdaten.info/Europa/Aland/ind...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>Albanien</td>
      <td>Shqipëria</td>
      <td>...</td>
      <td>6.70</td>
      <td>78.30</td>
      <td>https://www.laenderdaten.info/Europa/Albanien/...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Algeria</td>
      <td>Algerien</td>
      <td>Al-Jaza’ir/Algérie</td>
      <td>...</td>
      <td>4.30</td>
      <td>76.80</td>
      <td>https://www.laenderdaten.info/Afrika/Algerien/...</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 17 columns</p>
</div>




```python
worlddata = worlddata[['Country (en)', 'Continent']]
```


```python
worlddata.head(2)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country (en)</th>
      <th>Continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Egypt</td>
      <td>Africa</td>
    </tr>
  </tbody>
</table>
</div>




```python
worlddata = worlddata.rename(
    columns={'Country (en)': 'Country',
             'Continent': 'Continent'})
worlddata
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>Continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Egypt</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Åland Islands</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Algeria</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>243</th>
      <td>Wallis and Futuna</td>
      <td>Oceania</td>
    </tr>
    <tr>
      <th>244</th>
      <td>Christmas Island</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>245</th>
      <td>Western Sahara</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>246</th>
      <td>Central African Republic</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>247</th>
      <td>Cyprus</td>
      <td>Asia</td>
    </tr>
  </tbody>
</table>
<p>248 rows × 2 columns</p>
</div>




```python
realwage_f.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Country</th>
      <th>Australia</th>
      <th>Belgium</th>
      <th>Brazil</th>
      <th>...</th>
      <th>Turkey</th>
      <th>United Kingdom</th>
      <th>United States</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>12.06</td>
      <td>9.70</td>
      <td>0.87</td>
      <td>...</td>
      <td>2.27</td>
      <td>9.81</td>
      <td>6.05</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>12.46</td>
      <td>9.82</td>
      <td>0.92</td>
      <td>...</td>
      <td>2.26</td>
      <td>10.07</td>
      <td>6.24</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>12.24</td>
      <td>9.87</td>
      <td>0.96</td>
      <td>...</td>
      <td>2.22</td>
      <td>10.04</td>
      <td>6.78</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>12.40</td>
      <td>10.21</td>
      <td>1.03</td>
      <td>...</td>
      <td>2.28</td>
      <td>10.15</td>
      <td>7.58</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>12.34</td>
      <td>10.05</td>
      <td>1.08</td>
      <td>...</td>
      <td>2.30</td>
      <td>9.96</td>
      <td>7.88</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>




```python
realwage_f.transpose().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Time</th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2014-01-01 00:00:00</th>
      <th>2015-01-01 00:00:00</th>
      <th>2016-01-01 00:00:00</th>
    </tr>
    <tr>
      <th>Country</th>
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
      <th>Australia</th>
      <td>12.06</td>
      <td>12.46</td>
      <td>12.24</td>
      <td>...</td>
      <td>12.67</td>
      <td>12.83</td>
      <td>12.98</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>9.70</td>
      <td>9.82</td>
      <td>9.87</td>
      <td>...</td>
      <td>10.01</td>
      <td>9.95</td>
      <td>9.76</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>0.87</td>
      <td>0.92</td>
      <td>0.96</td>
      <td>...</td>
      <td>1.21</td>
      <td>1.21</td>
      <td>1.24</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>6.89</td>
      <td>6.96</td>
      <td>7.24</td>
      <td>...</td>
      <td>8.22</td>
      <td>8.35</td>
      <td>8.48</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>1.42</td>
      <td>1.45</td>
      <td>1.44</td>
      <td>...</td>
      <td>1.76</td>
      <td>1.81</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 11 columns</p>
</div>




```python
merged = pd.merge(
    realwage_f.transpose(),
    worlddata,
    how='left',
    left_index=True,
    right_on='Country')
merged.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2016-01-01 00:00:00</th>
      <th>Country</th>
      <th>Continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>12.06</td>
      <td>12.46</td>
      <td>12.24</td>
      <td>...</td>
      <td>12.98</td>
      <td>Australia</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>23</th>
      <td>9.70</td>
      <td>9.82</td>
      <td>9.87</td>
      <td>...</td>
      <td>9.76</td>
      <td>Belgium</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>32</th>
      <td>0.87</td>
      <td>0.92</td>
      <td>0.96</td>
      <td>...</td>
      <td>1.24</td>
      <td>Brazil</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>100</th>
      <td>6.89</td>
      <td>6.96</td>
      <td>7.24</td>
      <td>...</td>
      <td>8.48</td>
      <td>Canada</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>38</th>
      <td>1.42</td>
      <td>1.45</td>
      <td>1.44</td>
      <td>...</td>
      <td>1.91</td>
      <td>Chile</td>
      <td>South America</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 13 columns</p>
</div>




```python
merged[merged.Continent.isnull()]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2016-01-01 00:00:00</th>
      <th>Country</th>
      <th>Continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>247</th>
      <td>3.42</td>
      <td>3.74</td>
      <td>3.87</td>
      <td>...</td>
      <td>5.28</td>
      <td>Korea</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>247</th>
      <td>0.23</td>
      <td>0.45</td>
      <td>0.39</td>
      <td>...</td>
      <td>0.55</td>
      <td>Russian Federation</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>247</th>
      <td>1.50</td>
      <td>1.64</td>
      <td>1.71</td>
      <td>...</td>
      <td>2.08</td>
      <td>Slovak Republic</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 13 columns</p>
</div>



## fillna


```python
missing_continents = {
    'Korea': 'Asia',
    'Russian Federation': 'Europe',
    'Slovak Republic': 'Europe'
}

merged.Continent = merged['Continent'].fillna(
    merged.Country.map(missing_continents))

merged
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2016-01-01 00:00:00</th>
      <th>Country</th>
      <th>Continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>12.06</td>
      <td>12.46</td>
      <td>12.24</td>
      <td>...</td>
      <td>12.98</td>
      <td>Australia</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>23</th>
      <td>9.70</td>
      <td>9.82</td>
      <td>9.87</td>
      <td>...</td>
      <td>9.76</td>
      <td>Belgium</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>32</th>
      <td>0.87</td>
      <td>0.92</td>
      <td>0.96</td>
      <td>...</td>
      <td>1.24</td>
      <td>Brazil</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>100</th>
      <td>6.89</td>
      <td>6.96</td>
      <td>7.24</td>
      <td>...</td>
      <td>8.48</td>
      <td>Canada</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>38</th>
      <td>1.42</td>
      <td>1.45</td>
      <td>1.44</td>
      <td>...</td>
      <td>1.91</td>
      <td>Chile</td>
      <td>South America</td>
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
      <th>198</th>
      <td>3.92</td>
      <td>3.88</td>
      <td>3.96</td>
      <td>...</td>
      <td>5.05</td>
      <td>Slovenia</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>200</th>
      <td>3.99</td>
      <td>4.10</td>
      <td>4.14</td>
      <td>...</td>
      <td>4.19</td>
      <td>Spain</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>227</th>
      <td>2.27</td>
      <td>2.26</td>
      <td>2.22</td>
      <td>...</td>
      <td>3.23</td>
      <td>Turkey</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>241</th>
      <td>9.81</td>
      <td>10.07</td>
      <td>10.04</td>
      <td>...</td>
      <td>10.26</td>
      <td>United Kingdom</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>240</th>
      <td>6.05</td>
      <td>6.24</td>
      <td>6.78</td>
      <td>...</td>
      <td>7.16</td>
      <td>United States</td>
      <td>North America</td>
    </tr>
  </tbody>
</table>
<p>32 rows × 13 columns</p>
</div>




```python
merged[merged.Country == "Korea"]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2016-01-01 00:00:00</th>
      <th>Country</th>
      <th>Continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>247</th>
      <td>3.42</td>
      <td>3.74</td>
      <td>3.87</td>
      <td>...</td>
      <td>5.28</td>
      <td>Korea</td>
      <td>Asia</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 13 columns</p>
</div>



```merged.Country.map(missing_continents)``` creates an array of NaN for non missing continent and values for missing

`fillna` receives an array and replace the missings with the values from the input array

## to_replace


```python
list_country = ['Central America', 'North America', 'South America']
for country in list_country:
    merged.Continent.replace(
        to_replace=country, value='Americas', inplace=True)
```


```python
merged.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2016-01-01 00:00:00</th>
      <th>Country</th>
      <th>Continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <td>12.06</td>
      <td>12.46</td>
      <td>12.24</td>
      <td>...</td>
      <td>12.98</td>
      <td>Australia</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>23</th>
      <td>9.70</td>
      <td>9.82</td>
      <td>9.87</td>
      <td>...</td>
      <td>9.76</td>
      <td>Belgium</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>32</th>
      <td>0.87</td>
      <td>0.92</td>
      <td>0.96</td>
      <td>...</td>
      <td>1.24</td>
      <td>Brazil</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>100</th>
      <td>6.89</td>
      <td>6.96</td>
      <td>7.24</td>
      <td>...</td>
      <td>8.48</td>
      <td>Canada</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>38</th>
      <td>1.42</td>
      <td>1.45</td>
      <td>1.44</td>
      <td>...</td>
      <td>1.91</td>
      <td>Chile</td>
      <td>Americas</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 13 columns</p>
</div>



## set_index


```python
merged = merged.set_index(['Continent', 'Country']).sort_index()
merged.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2014-01-01 00:00:00</th>
      <th>2015-01-01 00:00:00</th>
      <th>2016-01-01 00:00:00</th>
    </tr>
    <tr>
      <th>Continent</th>
      <th>Country</th>
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
      <th rowspan="5" valign="top">Americas</th>
      <th>Brazil</th>
      <td>0.87</td>
      <td>0.92</td>
      <td>0.96</td>
      <td>...</td>
      <td>1.21</td>
      <td>1.21</td>
      <td>1.24</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>6.89</td>
      <td>6.96</td>
      <td>7.24</td>
      <td>...</td>
      <td>8.22</td>
      <td>8.35</td>
      <td>8.48</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>1.42</td>
      <td>1.45</td>
      <td>1.44</td>
      <td>...</td>
      <td>1.76</td>
      <td>1.81</td>
      <td>1.91</td>
    </tr>
    <tr>
      <th>Colombia</th>
      <td>1.01</td>
      <td>1.02</td>
      <td>1.01</td>
      <td>...</td>
      <td>1.13</td>
      <td>1.13</td>
      <td>1.12</td>
    </tr>
    <tr>
      <th>Costa Rica</th>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>...</td>
      <td>2.41</td>
      <td>2.56</td>
      <td>2.63</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 11 columns</p>
</div>




```python
merged.columns = pd.to_datetime(merged.columns)
merged.columns = merged.columns.rename('Time')
merged
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Time</th>
      <th>2006-01-01 00:00:00</th>
      <th>2007-01-01 00:00:00</th>
      <th>2008-01-01 00:00:00</th>
      <th>...</th>
      <th>2014-01-01 00:00:00</th>
      <th>2015-01-01 00:00:00</th>
      <th>2016-01-01 00:00:00</th>
    </tr>
    <tr>
      <th>Continent</th>
      <th>Country</th>
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
      <th rowspan="5" valign="top">Americas</th>
      <th>Brazil</th>
      <td>0.87</td>
      <td>0.92</td>
      <td>0.96</td>
      <td>...</td>
      <td>1.21</td>
      <td>1.21</td>
      <td>1.24</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>6.89</td>
      <td>6.96</td>
      <td>7.24</td>
      <td>...</td>
      <td>8.22</td>
      <td>8.35</td>
      <td>8.48</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>1.42</td>
      <td>1.45</td>
      <td>1.44</td>
      <td>...</td>
      <td>1.76</td>
      <td>1.81</td>
      <td>1.91</td>
    </tr>
    <tr>
      <th>Colombia</th>
      <td>1.01</td>
      <td>1.02</td>
      <td>1.01</td>
      <td>...</td>
      <td>1.13</td>
      <td>1.13</td>
      <td>1.12</td>
    </tr>
    <tr>
      <th>Costa Rica</th>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>...</td>
      <td>2.41</td>
      <td>2.56</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>...</th>
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
      <th rowspan="5" valign="top">Europe</th>
      <th>Russian Federation</th>
      <td>0.23</td>
      <td>0.45</td>
      <td>0.39</td>
      <td>...</td>
      <td>0.61</td>
      <td>0.56</td>
      <td>0.55</td>
    </tr>
    <tr>
      <th>Slovak Republic</th>
      <td>1.50</td>
      <td>1.64</td>
      <td>1.71</td>
      <td>...</td>
      <td>2.08</td>
      <td>2.08</td>
      <td>2.08</td>
    </tr>
    <tr>
      <th>Slovenia</th>
      <td>3.92</td>
      <td>3.88</td>
      <td>3.96</td>
      <td>...</td>
      <td>5.01</td>
      <td>5.05</td>
      <td>5.05</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>3.99</td>
      <td>4.10</td>
      <td>4.14</td>
      <td>...</td>
      <td>4.10</td>
      <td>4.14</td>
      <td>4.19</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>9.81</td>
      <td>10.07</td>
      <td>10.04</td>
      <td>...</td>
      <td>9.72</td>
      <td>10.01</td>
      <td>10.26</td>
    </tr>
  </tbody>
</table>
<p>32 rows × 11 columns</p>
</div>




```python
merged = merged.transpose()
merged.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Continent</th>
      <th colspan="3" halign="left">Americas</th>
      <th>...</th>
      <th colspan="3" halign="left">Europe</th>
    </tr>
    <tr>
      <th>Country</th>
      <th>Brazil</th>
      <th>Canada</th>
      <th>Chile</th>
      <th>...</th>
      <th>Slovenia</th>
      <th>Spain</th>
      <th>United Kingdom</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>0.87</td>
      <td>6.89</td>
      <td>1.42</td>
      <td>...</td>
      <td>3.92</td>
      <td>3.99</td>
      <td>9.81</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>0.92</td>
      <td>6.96</td>
      <td>1.45</td>
      <td>...</td>
      <td>3.88</td>
      <td>4.10</td>
      <td>10.07</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>0.96</td>
      <td>7.24</td>
      <td>1.44</td>
      <td>...</td>
      <td>3.96</td>
      <td>4.14</td>
      <td>10.04</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>1.03</td>
      <td>7.67</td>
      <td>1.52</td>
      <td>...</td>
      <td>4.08</td>
      <td>4.32</td>
      <td>10.15</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>1.08</td>
      <td>7.94</td>
      <td>1.56</td>
      <td>...</td>
      <td>4.81</td>
      <td>4.30</td>
      <td>9.96</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>



## index.get_level_values


```python
import matplotlib.pyplot as plt
import matplotlib
matplotlib.style.use('seaborn')
%matplotlib inline

merged.mean().sort_values(ascending=False).plot(
    kind='bar', title="Average real minimum wage 2006 - 2016")

# Set country labels
country_labels = merged.mean().sort_values(
    ascending=False).index.get_level_values('Country').tolist()
plt.xticks(range(0, len(country_labels)), country_labels)
plt.xlabel('Country')

plt.show()
```


![png](output_37_0.png)


## columns.get_level_values


```python
merged.columns.get_level_values('Continent').tolist()
```




    ['Americas',
     'Americas',
     'Americas',
     'Americas',
     'Americas',
     'Americas',
     'Americas',
     'Asia',
     'Asia',
     'Asia',
     'Asia',
     'Australia',
     'Australia',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe',
     'Europe']




```python
merged.mean(axis=1).plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1184282e8>




![png](output_40_1.png)



```python
merged.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Continent</th>
      <th colspan="3" halign="left">Americas</th>
      <th>...</th>
      <th colspan="3" halign="left">Europe</th>
    </tr>
    <tr>
      <th>Country</th>
      <th>Brazil</th>
      <th>Canada</th>
      <th>Chile</th>
      <th>...</th>
      <th>Slovenia</th>
      <th>Spain</th>
      <th>United Kingdom</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>0.87</td>
      <td>6.89</td>
      <td>1.42</td>
      <td>...</td>
      <td>3.92</td>
      <td>3.99</td>
      <td>9.81</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>0.92</td>
      <td>6.96</td>
      <td>1.45</td>
      <td>...</td>
      <td>3.88</td>
      <td>4.10</td>
      <td>10.07</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>0.96</td>
      <td>7.24</td>
      <td>1.44</td>
      <td>...</td>
      <td>3.96</td>
      <td>4.14</td>
      <td>10.04</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>1.03</td>
      <td>7.67</td>
      <td>1.52</td>
      <td>...</td>
      <td>4.08</td>
      <td>4.32</td>
      <td>10.15</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>1.08</td>
      <td>7.94</td>
      <td>1.56</td>
      <td>...</td>
      <td>4.81</td>
      <td>4.30</td>
      <td>9.96</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 32 columns</p>
</div>




```python
merged.mean(level='Country', axis=1)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Country</th>
      <th>Australia</th>
      <th>Belgium</th>
      <th>Brazil</th>
      <th>...</th>
      <th>Turkey</th>
      <th>United Kingdom</th>
      <th>United States</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>12.06</td>
      <td>9.70</td>
      <td>0.87</td>
      <td>...</td>
      <td>2.27</td>
      <td>9.81</td>
      <td>6.05</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>12.46</td>
      <td>9.82</td>
      <td>0.92</td>
      <td>...</td>
      <td>2.26</td>
      <td>10.07</td>
      <td>6.24</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>12.24</td>
      <td>9.87</td>
      <td>0.96</td>
      <td>...</td>
      <td>2.22</td>
      <td>10.04</td>
      <td>6.78</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>12.40</td>
      <td>10.21</td>
      <td>1.03</td>
      <td>...</td>
      <td>2.28</td>
      <td>10.15</td>
      <td>7.58</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>12.34</td>
      <td>10.05</td>
      <td>1.08</td>
      <td>...</td>
      <td>2.30</td>
      <td>9.96</td>
      <td>7.88</td>
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
      <th>2012-01-01</th>
      <td>12.60</td>
      <td>9.95</td>
      <td>1.18</td>
      <td>...</td>
      <td>2.43</td>
      <td>9.72</td>
      <td>7.48</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>12.64</td>
      <td>10.04</td>
      <td>1.21</td>
      <td>...</td>
      <td>2.48</td>
      <td>9.65</td>
      <td>7.38</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>12.67</td>
      <td>10.01</td>
      <td>1.21</td>
      <td>...</td>
      <td>2.51</td>
      <td>9.72</td>
      <td>7.26</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>12.83</td>
      <td>9.95</td>
      <td>1.21</td>
      <td>...</td>
      <td>2.69</td>
      <td>10.01</td>
      <td>7.25</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>12.98</td>
      <td>9.76</td>
      <td>1.24</td>
      <td>...</td>
      <td>3.23</td>
      <td>10.26</td>
      <td>7.16</td>
    </tr>
  </tbody>
</table>
<p>11 rows × 32 columns</p>
</div>




```python
merged.mean(level='Continent', axis=1).plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11a24a198>




![png](output_43_1.png)



```python
merged.drop('Americas', level=0, axis=1)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Continent</th>
      <th colspan="3" halign="left">Asia</th>
      <th>...</th>
      <th colspan="3" halign="left">Europe</th>
    </tr>
    <tr>
      <th>Country</th>
      <th>Israel</th>
      <th>Japan</th>
      <th>Korea</th>
      <th>...</th>
      <th>Slovenia</th>
      <th>Spain</th>
      <th>United Kingdom</th>
    </tr>
    <tr>
      <th>Time</th>
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
      <th>2006-01-01</th>
      <td>5.77</td>
      <td>5.69</td>
      <td>3.42</td>
      <td>...</td>
      <td>3.92</td>
      <td>3.99</td>
      <td>9.81</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>6.03</td>
      <td>5.75</td>
      <td>3.74</td>
      <td>...</td>
      <td>3.88</td>
      <td>4.10</td>
      <td>10.07</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>5.92</td>
      <td>5.79</td>
      <td>3.87</td>
      <td>...</td>
      <td>3.96</td>
      <td>4.14</td>
      <td>10.04</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>5.84</td>
      <td>5.99</td>
      <td>4.00</td>
      <td>...</td>
      <td>4.08</td>
      <td>4.32</td>
      <td>10.15</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>5.68</td>
      <td>6.14</td>
      <td>3.99</td>
      <td>...</td>
      <td>4.81</td>
      <td>4.30</td>
      <td>9.96</td>
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
      <th>2012-01-01</th>
      <td>5.82</td>
      <td>6.35</td>
      <td>4.18</td>
      <td>...</td>
      <td>4.94</td>
      <td>4.12</td>
      <td>9.72</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>5.94</td>
      <td>6.44</td>
      <td>4.38</td>
      <td>...</td>
      <td>4.98</td>
      <td>4.09</td>
      <td>9.65</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>5.91</td>
      <td>6.39</td>
      <td>4.64</td>
      <td>...</td>
      <td>5.01</td>
      <td>4.10</td>
      <td>9.72</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>6.31</td>
      <td>6.48</td>
      <td>4.93</td>
      <td>...</td>
      <td>5.05</td>
      <td>4.14</td>
      <td>10.01</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>6.59</td>
      <td>6.65</td>
      <td>5.28</td>
      <td>...</td>
      <td>5.05</td>
      <td>4.19</td>
      <td>10.26</td>
    </tr>
  </tbody>
</table>
<p>11 rows × 25 columns</p>
</div>




```python
merged.stack().describe()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Continent</th>
      <th>Americas</th>
      <th>Asia</th>
      <th>Australia</th>
      <th>Europe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>69.00</td>
      <td>44.00</td>
      <td>22.00</td>
      <td>200.00</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3.19</td>
      <td>4.70</td>
      <td>11.03</td>
      <td>5.15</td>
    </tr>
    <tr>
      <th>std</th>
      <td>3.02</td>
      <td>1.56</td>
      <td>1.58</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.52</td>
      <td>2.22</td>
      <td>8.44</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.03</td>
      <td>3.37</td>
      <td>9.56</td>
      <td>2.02</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.44</td>
      <td>5.48</td>
      <td>11.27</td>
      <td>3.54</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.96</td>
      <td>5.95</td>
      <td>12.45</td>
      <td>9.70</td>
    </tr>
    <tr>
      <th>max</th>
      <td>8.48</td>
      <td>6.65</td>
      <td>12.98</td>
      <td>12.39</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped = merged.groupby(level='Continent', axis=1)
grouped
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x119fccb70>




```python
grouped.size()
```




    Continent
    Americas      7
    Asia          4
    Australia     2
    Europe       19
    dtype: int64



## groups.keys


```python
grouped.groups.keys()
```




    dict_keys(['Australia', 'Asia', 'Europe', 'Americas'])




```python
grouped.get_group('Asia')['2015'].unstack()
```




    Continent  Country  Time      
    Asia       Israel   2015-01-01   6.31
               Japan    2015-01-01   6.48
               Korea    2015-01-01   4.93
               Turkey   2015-01-01   2.69
    dtype: float64



## grouped.get_group


```python
import seaborn as sns

continents = grouped.groups.keys()

for continent in continents:
    sns.kdeplot(grouped.get_group(continent)[
                '2015'].unstack(), label=continent, shade=True)

plt.title('Real minimum wages in 2015')
plt.xlabel('US dollars')
plt.show()
```


![png](output_52_0.png)


## Example 1


```python
employ = pd.read_csv("https://lectures.quantecon.org/_downloads/employ.csv")
```


```python
employ.set_index(pd.to_datetime(employ.DATE), inplace=True)
```


```python
employ.drop(['Unnamed: 0', 'DATE'], axis=1, inplace=True)
```


```python
employ.dropna(how='all', inplace=True)
employ.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GEO</th>
      <th>AGE</th>
      <th>UNIT</th>
      <th>SEX</th>
      <th>INDIC_EM</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>DATE</th>
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
      <th>2007-01-01</th>
      <td>European Union (28 countries)</td>
      <td>From 15 to 24 years</td>
      <td>Thousand persons</td>
      <td>Total</td>
      <td>Active population</td>
      <td>26,839.00</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>European Union (28 countries)</td>
      <td>From 15 to 24 years</td>
      <td>Thousand persons</td>
      <td>Total</td>
      <td>Total employment (resident population concept ...</td>
      <td>22,669.00</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>European Union (28 countries)</td>
      <td>From 15 to 24 years</td>
      <td>Thousand persons</td>
      <td>Males</td>
      <td>Active population</td>
      <td>14,665.00</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>European Union (28 countries)</td>
      <td>From 15 to 24 years</td>
      <td>Thousand persons</td>
      <td>Males</td>
      <td>Total employment (resident population concept ...</td>
      <td>12,430.00</td>
    </tr>
    <tr>
      <th>2007-01-01</th>
      <td>European Union (28 countries)</td>
      <td>From 15 to 24 years</td>
      <td>Thousand persons</td>
      <td>Females</td>
      <td>Active population</td>
      <td>12,173.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
employ = employ.pivot_table(index='DATE', columns=[
                            'AGE', 'GEO', 'SEX', 'UNIT'], values='Value')
employ
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>AGE</th>
      <th colspan="3" halign="left">From 15 to 24 years</th>
      <th>...</th>
      <th colspan="3" halign="left">From 55 to 64 years</th>
    </tr>
    <tr>
      <th>GEO</th>
      <th colspan="3" halign="left">Austria</th>
      <th>...</th>
      <th colspan="3" halign="left">United Kingdom</th>
    </tr>
    <tr>
      <th>SEX</th>
      <th colspan="2" halign="left">Females</th>
      <th>Males</th>
      <th>...</th>
      <th>Males</th>
      <th colspan="2" halign="left">Total</th>
    </tr>
    <tr>
      <th>UNIT</th>
      <th>Percentage of total population</th>
      <th>Thousand persons</th>
      <th>Percentage of total population</th>
      <th>...</th>
      <th>Thousand persons</th>
      <th>Percentage of total population</th>
      <th>Thousand persons</th>
    </tr>
    <tr>
      <th>DATE</th>
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
      <th>2007-01-01</th>
      <td>53.30</td>
      <td>264.50</td>
      <td>59.95</td>
      <td>...</td>
      <td>2,390.00</td>
      <td>58.35</td>
      <td>4,199.50</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>53.75</td>
      <td>267.00</td>
      <td>60.25</td>
      <td>...</td>
      <td>2,443.00</td>
      <td>58.90</td>
      <td>4,272.00</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>53.35</td>
      <td>265.00</td>
      <td>59.35</td>
      <td>...</td>
      <td>2,444.00</td>
      <td>58.90</td>
      <td>4,294.00</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>51.45</td>
      <td>254.50</td>
      <td>59.60</td>
      <td>...</td>
      <td>2,417.00</td>
      <td>58.60</td>
      <td>4,290.00</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>52.30</td>
      <td>258.00</td>
      <td>60.80</td>
      <td>...</td>
      <td>2,392.00</td>
      <td>58.20</td>
      <td>4,273.50</td>
    </tr>
    <tr>
      <th>2012-01-01</th>
      <td>52.85</td>
      <td>260.00</td>
      <td>60.10</td>
      <td>...</td>
      <td>2,407.50</td>
      <td>59.60</td>
      <td>4,330.00</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>52.55</td>
      <td>257.50</td>
      <td>59.35</td>
      <td>...</td>
      <td>2,448.00</td>
      <td>61.30</td>
      <td>4,446.50</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>52.65</td>
      <td>257.00</td>
      <td>57.50</td>
      <td>...</td>
      <td>2,488.50</td>
      <td>62.25</td>
      <td>4,551.00</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>51.40</td>
      <td>249.50</td>
      <td>57.35</td>
      <td>...</td>
      <td>2,545.50</td>
      <td>63.30</td>
      <td>4,689.00</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>51.80</td>
      <td>250.00</td>
      <td>56.55</td>
      <td>...</td>
      <td>2,633.00</td>
      <td>64.60</td>
      <td>4,873.50</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 720 columns</p>
</div>




```python
employ.xs('Males', level=2, axis=1)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>AGE</th>
      <th colspan="3" halign="left">From 15 to 24 years</th>
      <th>...</th>
      <th colspan="3" halign="left">From 55 to 64 years</th>
    </tr>
    <tr>
      <th>GEO</th>
      <th colspan="2" halign="left">Austria</th>
      <th>Belgium</th>
      <th>...</th>
      <th>Turkey</th>
      <th colspan="2" halign="left">United Kingdom</th>
    </tr>
    <tr>
      <th>UNIT</th>
      <th>Percentage of total population</th>
      <th>Thousand persons</th>
      <th>Percentage of total population</th>
      <th>...</th>
      <th>Thousand persons</th>
      <th>Percentage of total population</th>
      <th>Thousand persons</th>
    </tr>
    <tr>
      <th>DATE</th>
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
      <th>2007-01-01</th>
      <td>59.95</td>
      <td>293.50</td>
      <td>33.00</td>
      <td>...</td>
      <td>944.50</td>
      <td>67.55</td>
      <td>2,390.00</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>60.25</td>
      <td>297.00</td>
      <td>32.85</td>
      <td>...</td>
      <td>1,005.00</td>
      <td>68.50</td>
      <td>2,443.00</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>59.35</td>
      <td>291.00</td>
      <td>31.15</td>
      <td>...</td>
      <td>1,066.50</td>
      <td>68.20</td>
      <td>2,444.00</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>59.60</td>
      <td>291.50</td>
      <td>31.25</td>
      <td>...</td>
      <td>1,155.00</td>
      <td>67.15</td>
      <td>2,417.00</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>60.80</td>
      <td>296.00</td>
      <td>30.90</td>
      <td>...</td>
      <td>1,283.00</td>
      <td>66.25</td>
      <td>2,392.00</td>
    </tr>
    <tr>
      <th>2012-01-01</th>
      <td>60.10</td>
      <td>294.50</td>
      <td>31.40</td>
      <td>...</td>
      <td>1,370.50</td>
      <td>67.45</td>
      <td>2,407.50</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>59.35</td>
      <td>291.00</td>
      <td>29.50</td>
      <td>...</td>
      <td>1,402.00</td>
      <td>68.70</td>
      <td>2,448.00</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>57.50</td>
      <td>280.50</td>
      <td>28.40</td>
      <td>...</td>
      <td>1,497.50</td>
      <td>69.35</td>
      <td>2,488.50</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>57.35</td>
      <td>280.50</td>
      <td>28.90</td>
      <td>...</td>
      <td>1,580.00</td>
      <td>70.05</td>
      <td>2,545.50</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>56.55</td>
      <td>283.00</td>
      <td>27.35</td>
      <td>...</td>
      <td>1,738.50</td>
      <td>71.10</td>
      <td>2,633.00</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 240 columns</p>
</div>




```python
for col in employ.columns.names:
    print(col, employ.columns.get_level_values(col).unique())
```

    AGE Index(['From 15 to 24 years', 'From 25 to 54 years', 'From 55 to 64 years'], dtype='object', name='AGE')
    GEO Index(['Austria', 'Belgium', 'Bulgaria', 'Croatia', 'Cyprus', 'Czech Republic',
           'Denmark', 'Estonia', 'Euro area (17 countries)',
           'Euro area (18 countries)', 'Euro area (19 countries)',
           'European Union (15 countries)', 'European Union (27 countries)',
           'European Union (28 countries)', 'Finland',
           'Former Yugoslav Republic of Macedonia, the', 'France',
           'France (metropolitan)',
           'Germany (until 1990 former territory of the FRG)', 'Greece', 'Hungary',
           'Iceland', 'Ireland', 'Italy', 'Latvia', 'Lithuania', 'Luxembourg',
           'Malta', 'Netherlands', 'Norway', 'Poland', 'Portugal', 'Romania',
           'Slovakia', 'Slovenia', 'Spain', 'Sweden', 'Switzerland', 'Turkey',
           'United Kingdom'],
          dtype='object', name='GEO')
    SEX Index(['Females', 'Males', 'Total'], dtype='object', name='SEX')
    UNIT Index(['Percentage of total population', 'Thousand persons'], dtype='object', name='UNIT')
    


```python
employ.columns = employ.columns.swaplevel(0, 1)
employ = employ.sort_index(axis=1)
employ
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>GEO</th>
      <th colspan="3" halign="left">Austria</th>
      <th>...</th>
      <th colspan="3" halign="left">United Kingdom</th>
    </tr>
    <tr>
      <th>AGE</th>
      <th colspan="3" halign="left">From 15 to 24 years</th>
      <th>...</th>
      <th colspan="3" halign="left">From 55 to 64 years</th>
    </tr>
    <tr>
      <th>SEX</th>
      <th colspan="2" halign="left">Females</th>
      <th>Males</th>
      <th>...</th>
      <th>Males</th>
      <th colspan="2" halign="left">Total</th>
    </tr>
    <tr>
      <th>UNIT</th>
      <th>Percentage of total population</th>
      <th>Thousand persons</th>
      <th>Percentage of total population</th>
      <th>...</th>
      <th>Thousand persons</th>
      <th>Percentage of total population</th>
      <th>Thousand persons</th>
    </tr>
    <tr>
      <th>DATE</th>
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
      <th>2007-01-01</th>
      <td>53.30</td>
      <td>264.50</td>
      <td>59.95</td>
      <td>...</td>
      <td>2,390.00</td>
      <td>58.35</td>
      <td>4,199.50</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>53.75</td>
      <td>267.00</td>
      <td>60.25</td>
      <td>...</td>
      <td>2,443.00</td>
      <td>58.90</td>
      <td>4,272.00</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>53.35</td>
      <td>265.00</td>
      <td>59.35</td>
      <td>...</td>
      <td>2,444.00</td>
      <td>58.90</td>
      <td>4,294.00</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>51.45</td>
      <td>254.50</td>
      <td>59.60</td>
      <td>...</td>
      <td>2,417.00</td>
      <td>58.60</td>
      <td>4,290.00</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>52.30</td>
      <td>258.00</td>
      <td>60.80</td>
      <td>...</td>
      <td>2,392.00</td>
      <td>58.20</td>
      <td>4,273.50</td>
    </tr>
    <tr>
      <th>2012-01-01</th>
      <td>52.85</td>
      <td>260.00</td>
      <td>60.10</td>
      <td>...</td>
      <td>2,407.50</td>
      <td>59.60</td>
      <td>4,330.00</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>52.55</td>
      <td>257.50</td>
      <td>59.35</td>
      <td>...</td>
      <td>2,448.00</td>
      <td>61.30</td>
      <td>4,446.50</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>52.65</td>
      <td>257.00</td>
      <td>57.50</td>
      <td>...</td>
      <td>2,488.50</td>
      <td>62.25</td>
      <td>4,551.00</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>51.40</td>
      <td>249.50</td>
      <td>57.35</td>
      <td>...</td>
      <td>2,545.50</td>
      <td>63.30</td>
      <td>4,689.00</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>51.80</td>
      <td>250.00</td>
      <td>56.55</td>
      <td>...</td>
      <td>2,633.00</td>
      <td>64.60</td>
      <td>4,873.50</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 720 columns</p>
</div>




```python
geo_list = employ.columns.get_level_values('GEO').unique().tolist()
countries = [x for x in geo_list if not x.startswith('Euro')]
employ = employ[countries]
employ.columns.get_level_values('GEO').unique()
```




    Index(['Austria', 'Belgium', 'Bulgaria', 'Croatia', 'Cyprus', 'Czech Republic',
           'Denmark', 'Estonia', 'Finland',
           'Former Yugoslav Republic of Macedonia, the', 'France',
           'France (metropolitan)',
           'Germany (until 1990 former territory of the FRG)', 'Greece', 'Hungary',
           'Iceland', 'Ireland', 'Italy', 'Latvia', 'Lithuania', 'Luxembourg',
           'Malta', 'Netherlands', 'Norway', 'Poland', 'Portugal', 'Romania',
           'Slovakia', 'Slovenia', 'Spain', 'Sweden', 'Switzerland', 'Turkey',
           'United Kingdom'],
          dtype='object', name='GEO')




```python
geog = employ.columns.get_level_values('GEO').unique().tolist()
geog2 = [i for i in geog if not i.startswith('Euro')]  # starts
```


```python
employ = employ[geog2]
```


```python
employ_f = employ.xs(('Percentage of total population'),
                     level=('UNIT'),
                     axis=1)
employ_f.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>GEO</th>
      <th colspan="3" halign="left">Austria</th>
      <th>...</th>
      <th colspan="3" halign="left">United Kingdom</th>
    </tr>
    <tr>
      <th>AGE</th>
      <th colspan="3" halign="left">From 15 to 24 years</th>
      <th>...</th>
      <th colspan="3" halign="left">From 55 to 64 years</th>
    </tr>
    <tr>
      <th>SEX</th>
      <th>Females</th>
      <th>Males</th>
      <th>Total</th>
      <th>...</th>
      <th>Females</th>
      <th>Males</th>
      <th>Total</th>
    </tr>
    <tr>
      <th>DATE</th>
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
      <th>2007-01-01</th>
      <td>53.30</td>
      <td>59.95</td>
      <td>56.60</td>
      <td>...</td>
      <td>49.35</td>
      <td>67.55</td>
      <td>58.35</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>53.75</td>
      <td>60.25</td>
      <td>56.95</td>
      <td>...</td>
      <td>49.60</td>
      <td>68.50</td>
      <td>58.90</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>53.35</td>
      <td>59.35</td>
      <td>56.30</td>
      <td>...</td>
      <td>49.90</td>
      <td>68.20</td>
      <td>58.90</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>51.45</td>
      <td>59.60</td>
      <td>55.55</td>
      <td>...</td>
      <td>50.30</td>
      <td>67.15</td>
      <td>58.60</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>52.30</td>
      <td>60.80</td>
      <td>56.55</td>
      <td>...</td>
      <td>50.40</td>
      <td>66.25</td>
      <td>58.20</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 306 columns</p>
</div>




```python
employ_f = employ_f.drop('Total', level='SEX', axis=1)
employ_f
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>GEO</th>
      <th colspan="3" halign="left">Austria</th>
      <th>...</th>
      <th colspan="3" halign="left">United Kingdom</th>
    </tr>
    <tr>
      <th>AGE</th>
      <th colspan="2" halign="left">From 15 to 24 years</th>
      <th>From 25 to 54 years</th>
      <th>...</th>
      <th>From 25 to 54 years</th>
      <th colspan="2" halign="left">From 55 to 64 years</th>
    </tr>
    <tr>
      <th>SEX</th>
      <th>Females</th>
      <th>Males</th>
      <th>Females</th>
      <th>...</th>
      <th>Males</th>
      <th>Females</th>
      <th>Males</th>
    </tr>
    <tr>
      <th>DATE</th>
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
      <th>2007-01-01</th>
      <td>53.30</td>
      <td>59.95</td>
      <td>78.60</td>
      <td>...</td>
      <td>89.90</td>
      <td>49.35</td>
      <td>67.55</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>53.75</td>
      <td>60.25</td>
      <td>79.35</td>
      <td>...</td>
      <td>89.65</td>
      <td>49.60</td>
      <td>68.50</td>
    </tr>
    <tr>
      <th>2009-01-01</th>
      <td>53.35</td>
      <td>59.35</td>
      <td>80.25</td>
      <td>...</td>
      <td>88.70</td>
      <td>49.90</td>
      <td>68.20</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>51.45</td>
      <td>59.60</td>
      <td>80.65</td>
      <td>...</td>
      <td>88.40</td>
      <td>50.30</td>
      <td>67.15</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>52.30</td>
      <td>60.80</td>
      <td>81.50</td>
      <td>...</td>
      <td>88.80</td>
      <td>50.40</td>
      <td>66.25</td>
    </tr>
    <tr>
      <th>2012-01-01</th>
      <td>52.85</td>
      <td>60.10</td>
      <td>82.20</td>
      <td>...</td>
      <td>89.30</td>
      <td>52.00</td>
      <td>67.45</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>52.55</td>
      <td>59.35</td>
      <td>82.50</td>
      <td>...</td>
      <td>89.35</td>
      <td>54.15</td>
      <td>68.70</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>52.65</td>
      <td>57.50</td>
      <td>82.40</td>
      <td>...</td>
      <td>90.10</td>
      <td>55.40</td>
      <td>69.35</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>51.40</td>
      <td>57.35</td>
      <td>82.35</td>
      <td>...</td>
      <td>90.10</td>
      <td>56.85</td>
      <td>70.05</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>51.80</td>
      <td>56.55</td>
      <td>82.75</td>
      <td>...</td>
      <td>90.60</td>
      <td>58.30</td>
      <td>71.10</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 204 columns</p>
</div>




```python
box = employ_f['2015'].unstack().reset_index()
box
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GEO</th>
      <th>AGE</th>
      <th>SEX</th>
      <th>DATE</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Austria</td>
      <td>From 15 to 24 years</td>
      <td>Females</td>
      <td>2015-01-01</td>
      <td>51.40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Austria</td>
      <td>From 15 to 24 years</td>
      <td>Males</td>
      <td>2015-01-01</td>
      <td>57.35</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Austria</td>
      <td>From 25 to 54 years</td>
      <td>Females</td>
      <td>2015-01-01</td>
      <td>82.35</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Austria</td>
      <td>From 25 to 54 years</td>
      <td>Males</td>
      <td>2015-01-01</td>
      <td>89.10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Austria</td>
      <td>From 55 to 64 years</td>
      <td>Females</td>
      <td>2015-01-01</td>
      <td>39.50</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>199</th>
      <td>United Kingdom</td>
      <td>From 15 to 24 years</td>
      <td>Males</td>
      <td>2015-01-01</td>
      <td>55.25</td>
    </tr>
    <tr>
      <th>200</th>
      <td>United Kingdom</td>
      <td>From 25 to 54 years</td>
      <td>Females</td>
      <td>2015-01-01</td>
      <td>78.25</td>
    </tr>
    <tr>
      <th>201</th>
      <td>United Kingdom</td>
      <td>From 25 to 54 years</td>
      <td>Males</td>
      <td>2015-01-01</td>
      <td>90.10</td>
    </tr>
    <tr>
      <th>202</th>
      <td>United Kingdom</td>
      <td>From 55 to 64 years</td>
      <td>Females</td>
      <td>2015-01-01</td>
      <td>56.85</td>
    </tr>
    <tr>
      <th>203</th>
      <td>United Kingdom</td>
      <td>From 55 to 64 years</td>
      <td>Males</td>
      <td>2015-01-01</td>
      <td>70.05</td>
    </tr>
  </tbody>
</table>
<p>204 rows × 5 columns</p>
</div>




```python
sns.boxplot(
    x="AGE", y=0, hue="SEX", data=box, palette=("husl"), showfliers=False)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11ae58b38>




![png](output_68_1.png)
