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
df_total = pd.read_csv("../dataSet/aqi_hourly_to_2016-02-04.csv")
df =  df_total.head(100000)
```
What's more, we find there are lots of invalid rows, which have '-' or NaN. Before we do Machine Learning, we need to clean the data. So we write a data clean function to help us clean and standardize data.
