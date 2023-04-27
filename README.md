# Social-Media-page-Analysis-Using-GCP
# Project Description
This project aims to transform and visualize the Facebook page likes data for a better understanding of the trend over time. The project uses Apache Beam, pandas, scikit-learn, and matplotlib libraries for data transformation and visualization.

# Objectives:

To ingest Facebook page likes data and transform it for visualization.
To sort the data by date for plotting the trend of lifetime total likes over time.
To visualize the trend of lifetime total likes using a line plot.

# Scope:

The project will read the Facebook page likes data from a CSV file, convert the date column to datetime format, sort the data by date, and plot the trend of lifetime total likes over time. The project will use Apache Beam for data filtering, pandas for data transformation, and matplotlib for data visualization.

# Deliverables:

A Python script that ingests the Facebook page likes data, transforms it for visualization, and plots the trend of lifetime total likes over time.
A line plot that visualizes the trend of lifetime total likes over time.
A brief report on the data transformation and visualization process.

# Conclusion:

This project aims to transform and visualize the Facebook page likes data for a better understanding of the trend over time. The project will use Apache Beam for data filtering, pandas for data transformation, and matplotlib for data visualization. The project is expected to provide insights into the trend of lifetime total likes over time and enhance the understanding of Facebook page likes data.

THe below is the code used to do the project

!pip install apache-beam
!pip install pandas
!pip install scikit-learn
!pip install matplotlib

import apache_beam as beam
from flask import Flask, jsonify
import pandas as pd
import matplotlib.pyplot as plt

#make sure to upload TTL_PAGE.XLS TO GOOGLE COLLAB via drag n drop to the furthest left column on screen

df = pd.read_csv('TTL_PAGE.xls')

print("These are the header columns we looking to transform and process ")

print(df.columns)

# Get the number of columns in the Dataframe

num_columns = len(df.columns)

print("Number of columns:", num_columns)

pipe = beam.Pipeline()

def filter_data(element):

  if element[10]:
  
    return element
    
    with beam.Pipeline() as pipe1:
    
  ip = ( pipe
  
        |beam.io.ReadFromText("/content/TTL_PAGE.xls", skip_header_lines= True)
        
        |beam.Map(lambda x:x.split(","))
        
        |beam.Filter(filter_data)
        
        #|beam.Combiners.Count.Globally()
        
        |beam.Map(print)
        
)

pipe.run()

df = pd.read_csv('TTL_PAGE.xls')

# convert the 'Date' column to datetime
df['Date'] = pd.to_datetime(df['Date'])

# sort the dataframe by date
df.sort_values(by='Date', inplace=True)

# plot the trend of 'Lifetime Total Likes' over time

plt.plot(df['Date'], df['Lifetime Total Likes'])

plt.xlabel('Date')

plt.ylabel('Lifetime Total Likes')

plt.title('Trend of Lifetime Total Likes over time')

plt.show()
