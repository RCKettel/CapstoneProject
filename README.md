![VideoGameImage](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/video-game-controllers.jpg)

# Projecting Future Videogame Sales
Final Project for Flatiron school

## Contents

[Notebooks](https://github.com/RCKettel/CapstoneProject/tree/main/Notebooks)
Contains EDA and Final Notebooks

[Data](https://github.com/RCKettel/CapstoneProject/tree/main/Data)
Contains data files used in the notebooks

[Projects](https://github.com/RCKettel/CapstoneProject/tree/main/Projects)
Contains slides of the presentation 

[Resources](https://github.com/RCKettel/CapstoneProject/tree/main/Resources)
Contains data citations and images used in the slideshow

[Src](https://github.com/RCKettel/CapstoneProject/tree/main/Src)
Contains source code for any manufactured functions used in the notebok

## Business Understanding
The [Project Data](https://data.world/julienf/video-games-global-sales-in-volume-1983-2017) contains over 16,500 records of the sales of individual videogames in each major market from 1980 through 2020 including North America, Europe, and Japan ranked by the total global sales for that game.  The data for the games is common to each market and additionally contians the title, platform, genre, and publisher for each.  Since the data only had a few features on which to predict, more features needed to be engineered from the existing data and an API was used to collect data from the Internet Games Database website. This data was used to further engineer features for the models predictive capabilities. 

## Data Understanding
The [Sglobale Dataset](https://data.world/julienf/video-games-global-sales-in-volume-1983-2017) contains over 16,500 records of sales for individual videogames in each major market from 1980 through 2020 including North America, Europe, and Japan ranked by the total global sales for that game.  The data for the games are common to each market and contain the title, platform, genre, and publisher of each.  Since multicollinearity was an issue with this data, more data was collected using an API request from [IGDB](pi-docs.igdb.com/#about), the code to which can be found in the [IgdbApiNotebook](https://github.com/RCKettel/CapstoneProject/blob/main/Notebooks/IgdbApiNotebook.ipynb).  This data contains numerous rows that have information about some of the games that are included in the Sglobale dataframe.  The rows contain contain codes for representations of the data in each column.

![YearlyEarnings](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/GameSalesYear.png)

## Data Collection
To collect data from [IGDB](https://api-docs.igdb.com/#about) create a [twitch account](https://dev.twitch.tv/login) If the instructions are followed at the account creation site for Twitch.tv there shouldn't be a major problem.  Once the client ID and client secret have been collected an access token will be needed to collect the data from IGDB. The request URL is found under the authentification section of the instructions on the IGDB website the above link should lead to and the client ID and client secret can be filled in to make a successful request.  The Apicalypse Python wrapper was used with the client ID, client secret, and the request URL to return a byte array with the results of the request. The data collected was for the games in the sglobal dataset so the names of the games were used to identify which game data should be returned.

## The First Model
This model, a linear regression, was run to identify how well a regression would fit to the features using a basic supervised model without any regularization. The results clearly show the model does not perform well with the features as they are. The low r2 score of .16 in tandem with a high MAE of .71 in the results of the training data show a low distrbution about the mean and low accuracy in the predictions of the model. In addition, the even lower r2 and much higher MAE in the validation scores show the model does not generalize well to new data proving underfitness and a possible need for regularization.

![linregplt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/LinRgRegPlt.png)
![linregrsdplt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/LinRgRsdPlt.png)

## The Second Model
Ridge Regression was chosen to adjust the coefficients without lowereing them to zero in order to lower the variance thereby raising the scores from the validation data.  This did not prevent the model from being underfit. The training data in this model gave results that were nearly identical to those in the linear regression model the difference being a negligible increase in the r2 score.  The greatest difference for this model was in the scores from the test data.  The r2 score at .15 and the MAE at .76 are a dramatic change in comparison to the original scores returned by the linear regression model. However, the reg plot has shown the difficulty the model had in predicting on a dependent variable, by visualizing more easily where the data is better predicted at lower values than at higher values and how the reliability of the predictions were somewhat untrustworthy. Meanwhile, the residuals plot demonstrated the necessity to move away from a more basic linear regression where it had shown the heteroskedasticity of the data.  When the data was chosen, it was predicted the lower number of features would affect the predictions of the data.  For this reason, more data was collected.

![ResidPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/ResidualsofSecondModel.png)
![Regplt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/ActVsProjSlsscndMod.png)

## The final model
Compared to the second model the homoskedasticity of this model is far more evident. This data shows a greater distribution about the mean as demonstrated in the residuals graph and the reg plot. Given all of this, the accuracy has increased in this model over the original as can be seen in how the larger predictions fall along the projected values in both graphs demonstrating a better ability to predict on the dependent variables.

![ResidPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/BstRsdls.png)
![RegPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/BstPrjSls.png)

## Future Improvement
Using feature engineering and hypertuning will help improve the current model.  More and different models should be considered and improved upon to find of other models such as a KNearest Neighbors regressor or using boosting could improve the MAE score or the accuracy.  If the models don't show as much improvement a desired a final step would be to find more data and engineer more features using that data. Then begin working with the models again to see if there is any improvement in the models that showed the most promise.
