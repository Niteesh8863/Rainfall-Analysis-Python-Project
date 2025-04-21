# Rainfall-Analysis-Python-Project
Rainfall Analysis of Indian Meteorological Subdivisions (1901–2015) based on python project

'''
"""
Rainfall Analysis of Indian Meteorological Subdivisions (1901–2015)
====================================================================

Dataset Source:
https://www.data.gov.in/resource/area-weighted-monthly-seasonal-and-annual-rainfall-mm-36-meteorological-subdivisions-1901


"""

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Set style for plots
sns.set(style='whitegrid')

# ================================
# Load Dataset
# ================================
print("Loading dataset...")
df = pd.read_excel(r"C:\Users\nitee\OneDrive\Desktop\python project\rainfall_area-wt_sd_1901-2015.xlsx")

# ================================
# Dataset Overview
# ================================
print("\n--- Dataset Preview (First 5 Rows) ---")
print(df.head())

print("\n--- Dataset Info ---")
df.info()

print("\n--- Dataset Shape ---")
print(f"Total records: {df.shape[0]}, Total columns: {df.shape[1]}")

print("\n--- Summary Statistics ---")
print(df.describe(include='all'))

# ================================
# Define month columns
# ================================
months = ['JAN', 'FEB', 'MAR', 'APR', 'MAY', 'JUN',
          'JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC']

# ================================
# 1. Bar Plot - Annual Rainfall per Subdivision
# ================================
plt.figure(figsize=(14, 8))
sns.barplot(x='SUBDIVISION', y='ANNUAL', data=df)
plt.xticks(rotation=90)
plt.title('Annual Rainfall for All Subdivisions')
plt.xlabel('Subdivision')
plt.ylabel('Annual Rainfall (mm)')
plt.tight_layout()
plt.show()


# ================================
# 2. Pie Chart - Top 10 Subdivisions with Highest Annual Rainfall
# ================================
top_subdivisions = df.nlargest(10, 'ANNUAL')[['SUBDIVISION', 'ANNUAL']]
plt.figure(figsize=(8, 8))
plt.pie(top_subdivisions['ANNUAL'], labels=top_subdivisions['SUBDIVISION'],
        autopct='%1.1f%%', startangle=140)
plt.title('Top 10 Subdivisions with Highest Annual Rainfall')
plt.tight_layout()
plt.show()

# ================================
# 3. Histogram - Distribution of Annual Rainfall
# ================================
plt.figure(figsize=(10, 6))
sns.histplot(df['ANNUAL'], kde=True, bins=20)
plt.title('Distribution of Annual Rainfall Across All Subdivisions')
plt.xlabel('Annual Rainfall (mm)')
plt.ylabel('Frequency')
plt.tight_layout()
plt.show()

# ================================
# 4. Boxplot - Annual Rainfall by Subdivision
# ================================
plt.figure(figsize=(12, 8))
sns.boxplot(x='SUBDIVISION', y='ANNUAL', data=df)
plt.xticks(rotation=90)
plt.title('Boxplot of Annual Rainfall for All Subdivisions')
plt.xlabel('Subdivision')
plt.ylabel('Annual Rainfall (mm)')
plt.tight_layout()
plt.show()

# ================================
# 5. Line Plot - Annual Rainfall Trend for a Subdivision
# ================================
subdivision = 'ANDAMAN & NICOBAR ISLANDS'
df_sub = df[df['SUBDIVISION'] == subdivision]
plt.figure(figsize=(12, 6))
sns.lineplot(data=df_sub, x='YEAR', y='ANNUAL', marker='o', label=subdivision)
plt.title(f'Annual Rainfall Trend for {subdivision}')
plt.xlabel('Year')
plt.ylabel('Annual Rainfall (mm)')
plt.tight_layout()
plt.show()

# ================================
# 6. Grouped Bar Plot - Annual vs Seasonal Rainfall
# ================================
df_melted = df.melt(id_vars=['SUBDIVISION'],
                    value_vars=['ANNUAL', 'Jan-Feb', 'Mar-May', 'Jun-Sep', 'Oct-Dec'],
                    var_name='Season', value_name='Rainfall')
plt.figure(figsize=(14, 8))
sns.barplot(x='SUBDIVISION', y='Rainfall', hue='Season', data=df_melted)
plt.xticks(rotation=90)
plt.title('Comparison of Annual vs Seasonal Rainfall for Each Subdivision')
plt.xlabel('Subdivision')
plt.ylabel('Rainfall (mm)')
plt.legend(title='Season')
plt.tight_layout()
plt.show()

# ================================
# 7. Bar Plot - Top 5 Subdivisions by Average Annual Rainfall
# ================================
top_5 = df.groupby('SUBDIVISION')['ANNUAL'].mean().sort_values(ascending=False).head(5)
plt.figure(figsize=(12, 8))
top_5.plot(kind='bar', color='skyblue')
plt.title('Top 5 Subdivisions with the Highest Average Annual Rainfall')
plt.xlabel('Subdivision')
plt.ylabel('Average Annual Rainfall (mm)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# ================================
# 8. Scatter Plot - Rainfall Anomalies (Below 500 mm)
# ================================
df_anomalies = df[df['ANNUAL'] < 500]
plt.figure(figsize=(12, 6))
sns.scatterplot(x='YEAR', y='ANNUAL', data=df_anomalies,
                hue='SUBDIVISION', palette='Set2', marker='o')
plt.title('Rainfall Anomalies: Years with Annual Rainfall Below 500 mm')
plt.xlabel('Year')
plt.ylabel('Annual Rainfall (mm)')
plt.legend(title='Subdivision', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()
'''
