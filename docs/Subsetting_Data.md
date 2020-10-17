# Subsetting Data in Pandas


```python
import pandas as pd
```


```python
titanic = pd.read_csv('https://web.stanford.edu/class/cs102/datasets/Titanic.csv')
```


```python
 titanic.head()
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
      <th>last</th>
      <th>first</th>
      <th>gender</th>
      <th>age</th>
      <th>class</th>
      <th>fare</th>
      <th>embarked</th>
      <th>survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Braund</td>
      <td>Mr. Owen Harris</td>
      <td>M</td>
      <td>22.0</td>
      <td>3</td>
      <td>7.2500</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cumings</td>
      <td>Mrs. John Bradley (Florence Briggs Thayer)</td>
      <td>F</td>
      <td>38.0</td>
      <td>1</td>
      <td>71.2833</td>
      <td>Cherbourg</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Heikkinen</td>
      <td>Miss Laina</td>
      <td>F</td>
      <td>26.0</td>
      <td>3</td>
      <td>7.9250</td>
      <td>Southampton</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Futrelle</td>
      <td>Mrs. Jacques Heath (Lily May Peel)</td>
      <td>F</td>
      <td>35.0</td>
      <td>1</td>
      <td>53.1000</td>
      <td>Southampton</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Allen</td>
      <td>Mr. William Henry</td>
      <td>M</td>
      <td>35.0</td>
      <td>3</td>
      <td>8.0500</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>



##  Select Specific Columns

To select a single column, use square brackets [] with the column name of the column of interest.


```python
ages = titanic["age"]
```


```python
ages.head()
```




    0    22.0
    1    38.0
    2    26.0
    3    35.0
    4    35.0
    Name: age, dtype: float64




```python
age_sex = titanic[["age", "gender"]]
```


```python
age_sex.head()
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
      <th>age</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22.0</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35.0</td>
      <td>F</td>
    </tr>
    <tr>
      <th>4</th>
      <td>35.0</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>



## Understand the dataframe


```python
type(titanic[["age", "gender"]])
```




    pandas.core.frame.DataFrame




```python
titanic[["age", "gender"]].shape
```




    (891, 2)



## Select Specific Rows



```python
above_35 = titanic[titanic["age"] > 35]
```


```python
above_35.head()
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
      <th>last</th>
      <th>first</th>
      <th>gender</th>
      <th>age</th>
      <th>class</th>
      <th>fare</th>
      <th>embarked</th>
      <th>survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cumings</td>
      <td>Mrs. John Bradley (Florence Briggs Thayer)</td>
      <td>F</td>
      <td>38.0</td>
      <td>1</td>
      <td>71.2833</td>
      <td>Cherbourg</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>6</th>
      <td>McCarthy</td>
      <td>Mr. Timothy J</td>
      <td>M</td>
      <td>54.0</td>
      <td>1</td>
      <td>51.8625</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Bonnell</td>
      <td>Miss Elizabeth</td>
      <td>F</td>
      <td>58.0</td>
      <td>1</td>
      <td>26.5500</td>
      <td>Southampton</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Andersson</td>
      <td>Mr. Anders Johan</td>
      <td>M</td>
      <td>39.0</td>
      <td>3</td>
      <td>31.2750</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Hewlett</td>
      <td>Mrs. (Mary D Kingcome)</td>
      <td>F</td>
      <td>55.0</td>
      <td>2</td>
      <td>16.0000</td>
      <td>Southampton</td>
      <td>yes</td>
    </tr>
  </tbody>
</table>
</div>




```python
class_23 = titanic[titanic["class"].isin([2, 3])]
```


```python
class_23.head()
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
      <th>last</th>
      <th>first</th>
      <th>gender</th>
      <th>age</th>
      <th>class</th>
      <th>fare</th>
      <th>embarked</th>
      <th>survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Braund</td>
      <td>Mr. Owen Harris</td>
      <td>M</td>
      <td>22.0</td>
      <td>3</td>
      <td>7.2500</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Heikkinen</td>
      <td>Miss Laina</td>
      <td>F</td>
      <td>26.0</td>
      <td>3</td>
      <td>7.9250</td>
      <td>Southampton</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Allen</td>
      <td>Mr. William Henry</td>
      <td>M</td>
      <td>35.0</td>
      <td>3</td>
      <td>8.0500</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Moran</td>
      <td>Mr. James</td>
      <td>M</td>
      <td>NaN</td>
      <td>3</td>
      <td>8.4583</td>
      <td>Queenstown</td>
      <td>no</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Palsson</td>
      <td>Master Gosta Leonard</td>
      <td>M</td>
      <td>2.0</td>
      <td>3</td>
      <td>21.0750</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>



The above is equivalent to filtering by rows for which the class is either 2 or 3 and combining the two statements with an | (or) operator


```python
class_23 = titanic[(titanic["class"] == 2) | (titanic["class"] == 3)]
```

I want to work with passenger data for which the age is known.


```python
age_no_na = titanic[titanic["age"].notna()]
```


```python
age_no_na.head()
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
      <th>last</th>
      <th>first</th>
      <th>gender</th>
      <th>age</th>
      <th>class</th>
      <th>fare</th>
      <th>embarked</th>
      <th>survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Braund</td>
      <td>Mr. Owen Harris</td>
      <td>M</td>
      <td>22.0</td>
      <td>3</td>
      <td>7.2500</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cumings</td>
      <td>Mrs. John Bradley (Florence Briggs Thayer)</td>
      <td>F</td>
      <td>38.0</td>
      <td>1</td>
      <td>71.2833</td>
      <td>Cherbourg</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Heikkinen</td>
      <td>Miss Laina</td>
      <td>F</td>
      <td>26.0</td>
      <td>3</td>
      <td>7.9250</td>
      <td>Southampton</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Futrelle</td>
      <td>Mrs. Jacques Heath (Lily May Peel)</td>
      <td>F</td>
      <td>35.0</td>
      <td>1</td>
      <td>53.1000</td>
      <td>Southampton</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Allen</td>
      <td>Mr. William Henry</td>
      <td>M</td>
      <td>35.0</td>
      <td>3</td>
      <td>8.0500</td>
      <td>Southampton</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>



#### How do I select specific rows and columns from a DataFrame?

I’m interested in the names of the passengers older than 35 years.


```python
adult_names = titanic.loc[titanic["age"] > 35, "last"]
```


```python
adult_names.head()
```




    1       Cumings
    6      McCarthy
    11      Bonnell
    13    Andersson
    15      Hewlett
    Name: last, dtype: object



I’m interested in rows 10 till 25 and columns 3 to 5.


```python
titanic.iloc[9:25, 2:5]
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
      <th>gender</th>
      <th>age</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>F</td>
      <td>14.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>F</td>
      <td>4.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>11</th>
      <td>F</td>
      <td>58.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>M</td>
      <td>20.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>13</th>
      <td>M</td>
      <td>39.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>F</td>
      <td>14.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>15</th>
      <td>F</td>
      <td>55.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>16</th>
      <td>M</td>
      <td>2.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>17</th>
      <td>M</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>18</th>
      <td>F</td>
      <td>31.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>19</th>
      <td>F</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>20</th>
      <td>M</td>
      <td>35.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>21</th>
      <td>M</td>
      <td>34.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>22</th>
      <td>F</td>
      <td>15.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>23</th>
      <td>M</td>
      <td>28.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>F</td>
      <td>8.0</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



When selecting subsets of data, square brackets [] are used.

Inside these brackets, you can use a single column/row label, a list of column/row labels, a slice of labels, a conditional expression or a colon.

Select specific rows and/or columns using loc when using the row and column names

Select specific rows and/or columns using iloc when using the positions in the table

You can assign new values to a selection based on loc/iloc.


```python
# comparson between two columns
#df.query('value_1 < value_2')
```
