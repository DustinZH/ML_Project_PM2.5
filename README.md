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

Second, we find there are lots of invalid rows, which have '-' or NaN. Before we do Machine Learning, we need to clean the data. So we write a data clean function to help us clean and standardize data.

Now we can get all the valid data set, it has 93790 rows, 1 column output,and 10 column attributes.

Finally, we want to make more attributes.So what we have done is to add 2-order and 3-order attributes to our data set. now it have 30 attributes.

---------------------------
## Final Step: Linear regression/LASSO/Neural Network
More detail in PM2.5 Multi-method Regression.ipynb
Final Result:

| Model        | Normalized RSS | 
| :---         |     :---:      |
| Simple first-order linear regression   | 0.542290     |
| Third-order linear regression     | 0.417474       |
| Third-order linear regression with LASSO L1 Regularization     | 0.417535       |
| Neural Network with 10 hidden-units     | 0.404074       |
| Neural Network with 20 hidden-units     | 0.391214       |
| Neural Network with 40 hidden-units     | 0.393047       |
| Neural Network with 80 hidden-units     | 0.406128       |
