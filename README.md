# Ex-09-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.


# CODE
# DEVELOPED BY : R BRINDHA
# REG NO : 212222230023
# Loading the dataset :
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("/content/Superstore (3).csv",encoding='unicode_escape')
df
```
# Removing unnecessary data variables :
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
```
# Detecting and removing outliers in current numeric data :
```
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
# data visualization :
# line plots :
```
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```
# HISTOGRAM :
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```
# count plot :
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```
# Barplot :
```
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
# KDE plot :
```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
# Point plot :
```
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
# Pie Chart :
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
#HeatMap
df4=df.copy() 
```
# encoding :
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])
Scaling :
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

```
# Heatmap :
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
# OUPUT
![1](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/98a73244-4e5f-47cf-98e9-eb918fca8bb7)
![2](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/1bb807c4-74ba-453a-b0b7-cd38cc9678e1)
![3](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/1d2a3db6-9668-44e6-960b-325498995930)
![4](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/8f5184d1-ddb3-497f-af20-76de1a1cd7dc)
![5](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/163d4b02-63c5-401e-86da-9ed404dd3856)
![6](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/1203abbb-2215-47dd-bd59-d74a2a1686a8)
![7](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/c2ad4ddb-eba5-466e-b5ce-3ac35977f7cb)
![8](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/98e3b214-a40a-41df-910c-328c8b7e9d89)
![9](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/da1cbfb7-e6ab-4e11-a92e-bfa645c8613c)
![10](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/d8d12b9e-314f-4e76-b2f5-7a3ad4f98811)
![11](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/1b64883d-d051-40b5-a979-5d199ed4dc55)
![12](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/06793c5f-f2a4-415e-ac32-3f963ba7307d)
![13](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/17c755e8-20d0-4753-8581-3973ce2060a4)
![14](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/4bc0d6e3-44c5-43b5-88ad-1af8244122dc)
![15](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/cef22bcf-17ba-4645-96b6-5be4424096df)
![16](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/a75c567c-db6a-4a64-9d46-1ef8f159c390)
![17](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/5cc27598-33fa-4662-a8b5-17bb2eb0e3d7)
![18](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/02b82249-1b02-46d1-9354-f8245f933360)
![19](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/75814c9a-c7a6-49f4-8ac0-2c60170265ca)
![20](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/16640ff6-a2f2-4d76-aabd-e6599247a86f)
![21](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/51f5e288-31bb-421f-8dbb-d5197f74c27f)
![22](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/82c015c7-a4c9-41b3-95e5-40e9d8529f8a)
![23](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/521a5de6-9a79-4bc4-9745-c9736ebe50ec)
![24](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/26208823-dac1-4704-9661-0f9119780e36)
![25](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/41be16c8-436b-40d4-9b21-5402e7eac971)
![26](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/24f199bf-818a-455b-a3d7-08b43e2cc7b5)
![27](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/83a87030-df3b-4b98-89ad-6b7a6dbd2a58)
![28](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/585dbd9d-9e91-4e05-974f-51ba51f22b17)
![29](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/1ef247f5-4ba9-451c-bc73-f722a296fa44)
![30](https://github.com/Brindha77/Ex-08-Data-Visualization_1/assets/118889143/504e5b1c-41d5-4f2e-be7a-3e7518ecc665)
# RESULT:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.


