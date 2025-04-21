# elevate_labs_intership_task1
import csv
file_path = r"C:\Users\praba\Downloads\sales_data_sample.csv"
# using import csv library to import the file(sales_data_sample.csv) using file path

import pandas as pd
df = pd.read_csv(file_path, encoding='latin1') 
# Load the CSV file into a DataFrame using pandas
# 'latin1' encoding handles special characters that may break UTF-8

print (df.head)
# show the first 5 rows of your DataFrame in a clean, table-like format helping in unoking column names and processing data further

print(df[df.isnull().any(axis=1)])
# prints all rows in the DataFrame that contain at least one missing (NaN) value.

print(df.isnull().sum())
# shows the total number of missing (NaN) values

df['ORDERDATE'] = pd.to_datetime(df['ORDERDATE'], format='%m/%d/%Y %H:%M')
df['ORDERDATE'] = df['ORDERDATE'].dt.strftime('%d-%m-%Y')
# Parse the full format correctly
# Then convert to dd-mm-yyyy as a string

import numpy as np
columns_to_clean = ['ADDRESSLINE2', 'STATE', 'POSTALCODE', 'TERRITORY']
df[columns_to_clean] = df[columns_to_clean].replace(r'^\s*$', np.nan, regex=True)

# Regex pattern that matches strings that are empty or contain only whitespace then Replaces those bad entries

df['ADDRESSLINE2'] = df['ADDRESSLINE2'].fillna(df['ADDRESSLINE1'])  # Copy from ADDRESSLINE1
df['STATE'] = df['STATE'].fillna('NA')
df['POSTALCODE'] = df['POSTALCODE'].fillna('00000')
df['TERRITORY'] = df['TERRITORY'].fillna('NA')
# Fills the misssing value with the respective asked in above code


output_path = r"C:\Users\praba\Downloads\sales_data_cleaned.csv"
df.to_csv(output_path, index=False)
print(" Cleaning complete. File saved as 'sales_data_cleaned.csv'")
# Save the cleaned DataFrame to a new CSV file named sales_data_cleaned.csv

print(df[columns_to_clean].isnull().sum())
# checking the specific coloumn if the still have any null value

print(df.isnull().sum())
# checking entire in table for null value




