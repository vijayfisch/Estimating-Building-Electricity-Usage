# Estimating Buildings Electricity Usage

Vijay Fisch
 
Tony Zhang
 
Rheona Mehta 

Trinity Yacoub


## INTRO:
Boston is a city facing the grave effects of climate change. Sitting on the ocean, we are at high risk of rising sea levels, stronger storms, and worsening infrastructure due to extreme heat and unusual weather events. We sought to determine the sustainability of Boston University buildings to understand how our university contributes to this crisis. With building emissions data provided by BU sustainability, our group created a predictive model for electricity usage by a building based on building height (meters), natural gas consumption (therms), and building gross area (square meters). 

## METHODOLOGY:
We were given two data tables (FY2021). The first table contained the columns “building code”, “E (kWh)”, “G (Therms)”, and “O (gallons).” The second table contained “building code”, “building type”, “address”, “gross square footage”, “height”, and “stories.” First, we dropped 5 rows with building codes containing letters that would make merging our tables difficult and make our predictive models difficult to run. Once the five rows were dropped, using the inner join merge function, we combined the two data sets into one with the building code column. Noticing that our height was in the imperial system rather than the metric system with quotation marks used for the notation of feet and inches (ie. 6 '4'' for 6 feet 4 inches), we used regular expression to remove any special characters ( ‘ , “ , etc.) and convert the data into meters. Since the gross area is also empirical, we had to convert those data points in metric as well. Then, we replaced null values in the E(kWh) and G(Therms) columns with 0 and converted all numbers into integers, since machine learning models don’t usually process null values. We also realized that the data points are in various different types (some floats, some integers, and some strings). To convert all data points into integers, we used pd.to_numeric with error = ‘coerce’. Before moving to testing the different machine learning algorithms, we dropped the unnecessary columns: “Street 1 Address”, “Stories”, “Street 1 Number”. We also decided to solely look at buildings in the Charles River Campus since other campuses have very few data points. 
        	Having cleaned the data, we began our models to analyze and predict. We used linear regression, K Nearest Neighbors, random forests and trees, and ADA boost. 

## RESULTS:
After our data cleaning, collecting and analyzing, we came to the conclusion that there is a relationship between E(kWh), G(Therms), and O(gallons). Our random forest feature’s importances analysis found that the most important feature for predicting electricity use was the gross area of a building. 
The first method we used was linear regression. We excluded the petroleum column from our analyses because it had too many null values for any strong prediction. To create a linear regression model, we created two functions: one that would create a scatter plot with a line of best fit and R2 value based on a building type (residential, academic, etc.), and testing variable, and one that would create a residual plot. Although we had strong R2 values, our residual graphs showed patterns and concentrated values, so we decided to try another model.


<img width="623" alt="Screenshot 2023-04-30 at 9 23 18 PM" src="https://user-images.githubusercontent.com/106829297/235387640-d51d103f-8919-40d4-a2be-e08fb47d9127.png">


The next model was K Nearest Neighbors. We were unable to use a classifier since our data was numerical and not categorical. Instead, we set training columns and used the regressor model, which resulted in a relatively low R2 value with high variability. In order to improve our results, we moved onto the next method.
        	Our third model was a decision tree regressor. From the regressor we received an R2 value range of 0.88-0.90 with lower variability. Because of the high R2 value we were happy with these results but tried additional methods in hopes of a better R2 value. We moved onto the random forest method, yielding a better R2 value of 0.94 with a fixed random state. With random forest we were able to use the feature importances program which showed that the gross footage of a building is the most important factor when estimating electricity usage.
        	To conclude our methods, we decided to use the ADA boost method because of its ability to improve itself upon each successive run. Ultimately, we reached an R2 value of 0.966 with high confidence. To convey our findings, we created a predictive function that could estimate a building's electricity by taking three arguments: “Gross”, “G(Therms)”, and “Height”, and display a scatter plot of each respective variable with the predicted data and print the R2 value. 
         
         
<img width="599" alt="Screenshot 2023-04-30 at 9 22 55 PM" src="https://user-images.githubusercontent.com/106829297/235387601-40525fa0-60ab-4682-a147-9f7109ec7e1b.png">


## CONCLUSION:
With worsening climate change affecting coastal communities like Boston, it is more important than ever to use our data-science methods to evaluate our buildings and improve sustainability while reducing emissions. By using machine learning models through python, we were able to create a predictive model that could help predict future building electricity usage, and also help predict data for buildings that have a lack of data collection for certain parameters. 
