# Data Engineer: DQLab x KOMDIGI

## EDA (Exploratory Data Analysis)
- pandas library:
  > - `pd.read_csv, pd.read_json, pd.read_parquet, pd.read_sql_query and etc` : read data
  > - `<dataframe>.dtypes` : checking data type
- Profiling Data
- Data Cleansing:
  > - `<dataframe>.shape()` : shape data (bentuk data)
  > - `<dataframe>.drop_duplicates(inplace=True)` : remove duplicates data
  > - `<dataframe>.isnull().any()` : checking missing value (boolean)

#### Case Study: Data Profiling
```py
import pandas as pd
import numpy as np
import io
import pandas_profiling

# Baca dataset uncleaned_raw.csv
uncleaned_raw = pd.read_csv('https://storage.googleapis.com/dqlab-dataset/uncleaned_raw.csv')

#inspeksi dataframe uncleaned_raw
print('Lima data teratas:') 
print(uncleaned_raw.head())

#Check kolom yang mengandung missing value
print('\nKolom dengan missing value:') 
print(uncleaned_raw.isnull().any())

#Persentase missing value
length_qty = len(uncleaned_raw['Quantity'])
count_qty = uncleaned_raw['Quantity'].count()

#mengurangi length dengan count
number_of_missing_values_qty = length_qty - count_qty

#mengubah ke bentuk float
float_of_missing_values_qty = float(number_of_missing_values_qty / length_qty) 

#mengubah ke dalam bentuk persen
pct_of_missing_values_qty = '{0:.1f}%'.format(float_of_missing_values_qty * 100) 

#print hasil percent dari missing value
print('Persentase missing value kolom Quantity:', pct_of_missing_values_qty)

#Mengisi missing value tersebut dengan mean dari kolom tersebut
uncleaned_raw['Quantity'] = uncleaned_raw['Quantity'].fillna(uncleaned_raw['Quantity'].mean())
```                                                             
#### Lambda Function
  > - def name_function(x):
  >  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&emsp;return x*100
  > - `lambda x: (algorithm) | example: lambda x: x*100`: anonymous function

#### Treatment Missing Value
- Missing Value:
  > - `mv = <dataframe>.isna().sum()`: checking missing value (NaN dan .sum())
- Example Treatment Missing Value:  
  > ##### Treatment 1  
  >  
  > ```python
  > import pandas as pd
  > df = pd.read_csv("https://storage.googleapis.com/dqlab-dataset/datacovid19.csv")
  > print("Ukuran awal df: %d baris, %d kolom." % df.shape)
  > # Drop kolom yang seluruhnya missing value dan cetak ukurannya
  > df = df.dropna(axis=1, how="all")
  > print("Ukuran df setelah buang kolom dengan seluruh data missing: %d baris, %d kolom." % df.shape)
  ># Drop baris jika ada satu saja data yang missing dan cetak ukurannya
  > df = df.dropna(axis=0, how="any")
  > print("Ukuran df setelah dibuang baris yang memiliki sekurangnya 1 missing value: %d baris, %d kolom." % df.shape)
  > ```
  > ##### Treatment 2 : Change Value
  > ```py
  > import pandas as pd
  > df = pd.read_csv("https://storage.googleapis.com/dqlab-dataset/datacovid19.csv")
  > print("Unique value awal:\n", df["province_state"].unique())
  >df["province_state"] = df["province_state"].fillna("unknown")
  > print("Unique value setelah fillna:\n", df["province_state"].unique())


