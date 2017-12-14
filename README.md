# PM2.5 Prediction by Machine Learning
This is our Machine Learning project. We want to use Linear Regression/LASSO/Neural Network to predict PM2.5 in China.

---------------------------
## First Step: Data Collection 

At the beginning of our project, we need to find a huge property data Source and the data also need some attibutes, which can support us to do more fancy test in Machine Learning. Because a small data set always cases data overfit. Fortunately, we found 2 million rows dat of PM2.5 in Harvard CGA website. Now let's us to do the project ! 

Because GitHub's file size limit of 100MB, you can find the original pm2.5 data source here:
```sh
http://aqi.cga.harvard.edu/china/cumulative/
```

---------------------------
## Second Step: Data Extraction and Clean
After we get the data. First, we decide to only use One hundred thousand data, Because it's need long time to process two million data.
```sh
import pandas as pd
import numpy as np
df_total = pd.read_csv("../dataSet/aqi_hourly_to_2016-02-04.csv")
df =  df_total.head(100000)
```
Second, we find there are lots of invalid rows, which have '-' or NaN. Before we do Machine Learning, we need to clean the data. So we write a data clean function to help us clean and standardize data.
```sh
def data_clean(dfdata):
    data = np.array(dfdata[['pm25','pm10','o3','no2','so2','co','temperature','dewpoint','pressure','humidity','wind']])
    rows = data.shape[0]
    index = 0;
    while index < rows:
        for column in range(0,11):
            if data[index,column] == '-':
                data = np.delete(data,index,0)
                rows -= 1
                index -= 1
                break;
        index += 1
    data = data.astype('float')
    
    # remove rows which have NaN data
    rows = data.shape[0]
    check = np.isnan(data)
    index = 0;    
    while index < rows:
        for column in range(0,11):
            if check[index,column] == True:
                data = np.delete(data,index,0)
                check =  np.delete(check,index,0)
                rows -= 1
                index -= 1
                break;
        index += 1    
    return data

data = data_clean(df)  
```
Now we can get all the valid data set, it has 93790 rows, 1 column output,and 10 column attributes.
```sh
data.shape
```
Finally, we want to make more attributes.So what we have done is to add 2-order and 3-order attributes to our data set. now it have 30 attributes.
```sh
test = np.hstack((data,data*data))
data_2 = pd.DataFrame(test)
data_2.to_csv("/NYU/ML/ML_Project_PM2.5/dataSet/data_2.csv")
test2 = np.hstack((test,data*data*data))
data_3 = pd.DataFrame(test2)
data_3.to_csv("/NYU/ML/ML_Project_PM2.5/dataSet/data_3.csv")
```

---------------------------
## Third Step: Linear Regression 
