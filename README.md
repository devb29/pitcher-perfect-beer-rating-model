## **“Pitcher Perfect” - Beer Rating Model**

Served by Devra Alper



#### **Abstract**
This goal of this project was to create a model, “Pitcher Perfect,” that predicts beer ratings on [ratebeer.com](http://ratebeer.com). Data was scraped from the site’s [“Most Recent” ratings page](https://www.ratebeer.com/beer-ratings/) using Beautiful Soup and Selenium. After data was cleaned and exploratory data analysis was performed, modeling was completed using root mean squared error (RMSE) as an evaluation metric. This model could help breweries determine what features they should focus on when brewing a new beer. Ensuring a positive review on ratebeer.com could improve visibility on the site, which may increase sales and revenue.

#### **Design**
List comprehension was used to collect 100 URLs of the most recently rated beers. Then, each page was iterated over using Beautiful Soup to scrape the link for each beer on the page. Selenium was used to visit each beer detail page to scrape field data. 1485 pages were scraped for the following information: brewery, location of brewery, name of beer, "overall" and "style" scores, rating, number of ratings and reviews, ABV, calories, style of beer, description, type of glass the beer is served in, date it was added to the site, and its URL for reference during data cleaning. Overall and style scores were dropped as they were calculated by ratebeer.com using the target variable, rating. The columns used for calculations, rows with missing data, and information only used for reference while data cleaning were then dropped. Through visualizations and then confirmed with a Pearson’s correlation of 1.0, it was determined that ratebeer.com calculated calories from ABV; thus, one of the features (calories) was removed from the dataset.

Modeling began with all features included in a linear regression model. The model was overfitting and thus lasso cross-validation was used for feature selection. The selected features were used on another lasso model and finally another linear regression model to predict beer ratings.


#### **Data**
The original dataset used for modeling contains 1260 ratings (target) and 57 features. Features include: location of brewery, number of ratings and reviews, ABV, style of beer and type of glass it’s served in, and days since the beer was added to the site. Feature selection was used via lasso cross-validation, which resulted in 33 features in the final model.

#### **Algorithms**
*Feature Engineering*
1. The style of beer from each page was too specific and resulted in too many features. Instead, Beautiful Soup was used to scrape [this page](https://www.ratebeer.com/beerstyles/), which lists each style's general style. General style was used to create dummy variables.
2. The original location data listed the city, state/region, and country the beer was brewed in. Location was filtered by country only, then dummy variables were created.
3. Dummy variables were also created to indicate what type of glass the beer was served in.
4. A new column was created with the days since the beer has been on the site. This was calculated by subtracting the date the data was scraped from the date the beer was added to the site.

*Models*
Four models were tested: (1) linear regression with all features included, (2) lasso cross-validation with included feature selection, (3) lasso with only the selected features, and (4) linear regression with the selected features.

*Model Evaluation and Selection*
Data was split into train and test sets; 80% train and 20% test. Linear regression with all features included was overfitting on the training data. Training data was then split further to create a validation set for lasso cross-validation modeling; 80% train and 20% validation. This model served a dual purpose, which was both feature selection and model training. The model was not ideal, but it selected important features that were used to test another lasso regression and linear regression. While the linear regression model was overfitting slightly, the RMSE was better than the lasso regression’s RMSE. Ultimately, the scraped data used for modeling was limited and affects the accuracy of model predictions.

**Final Model**: Linear regression with feature selection determined by lasso cross-validation

Test R²: 0.35 <br>
RMSE: 0.30 <br>
RME: 0.24

**Tools**
* Beautiful Soup and Selenium for web scraping
* Numpy and Pandas for data manipulation
* Scikit-learn for modeling
* Matplotlib and Seaborn for plotting
