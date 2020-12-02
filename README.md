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
Since the introduction of the Nintendo Entertainment System in 1985 there has been a proliferation of new and more advanced gaming systems and videogames introduced to the global market. Though many companies likely have methods and tools to predict the success of new games, new and emerging tools may better position publishers to determine the potential success of a game based on the characteristics of a videogame. Putting predictive tools in the hands of manufacturers and marketers may reduce their risk of releasing a game that may not give a good return on investment and allows the company to invest their resources in projects that would have a higher likelihood of success.

## Data Understanding
The [Sglobale Dataset](https://data.world/julienf/video-games-global-sales-in-volume-1983-2017) contains over 16,500 records of sales for individual video games in each major market from 1980 through 2020 including North America, Europe, and Japan ranked by the total global sales for that game. The dataset also contains the title, platform, genre, and publisher for each entry in the dataset.  More data was collected using an IGDP API request, the code to which can be found in the [IgdbApiNotebook](https://github.com/RCKettel/CapstoneProject/blob/main/Notebooks/IgdbApiNotebook.ipynb).  This data contains numerous rows that have information about some of the games that are included in the Sglobale dataframe.

![YearlyEarnings](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/SalesByYear.png)

## Data Collection
To collect data from [IGDB](https://api-docs.igdb.com/#about) create a [twitch account](https://dev.twitch.tv/login) If the instructions are followed at the account creation site for Twitch.tv there shouldn't be a major problem.  Once the client ID and client secret have been collected an access token will be needed to collect the data from IGDB. The request URL is found under the authentification section of the instructions on the IGDB website the above link should lead to, then the client ID and client secret can be written into the URL to make a successful request.  The Apicalypse Python wrapper was used with the client ID, client secret, and the request URL to return a byte array with the results of the request. The data collected was for the games in the sglobal dataset so the names of the games were used to identify which game data should be returned.

## The First Model
This model, a linear regression, was run to identify how well a regression would fit to the features using a basic supervised model without any regularization.  The results clearly show the model does not perform well with the features.  The low r2 score of .18 in tandem with a high MAE of .73  in the results of the training data show a low distrbution about the mean and low accuracy in the predictions of the model.  In addition, the even lower r2 of -2 and much higher MAE, twelve digits in length, in the validation scores show the model does not generalize well to new data proving underfitness and a possible need for regularization.

![linregplt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/LinRgRegPlt2.png)
![linregrsdplt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/LinRgRsdPlt2.png)

## The Second Model
Ridge Regression was chosen to adjust the coefficients without lowereing them to zero in order to raise the variance, thereby, raising the scores from the validation data. This did not prevent the model from being underfit. The training data in this model gave results that were slightly better compared to those in the linear regression model the difference being a .1 increase in the r2 score. The greatest difference for this model was in the scores from the test data. The r2 score at .19 and the MAE at .70 are a dramatic change in comparison to the original scores returned by the linear regression model. However, the reg plot has shown the difficulty the model had in predicting on a dependent variable, by visualizing more easily where the data was grouped more at lower values than at higher values.  This demonstrated how the reliability of the predictions were somewhat untrustworthy. Meanwhile, the residuals plot identified the necessity to move away from a more basic linear regression where it had shown the heteroskedasticity of the data. The low r2 score is likely attributed to the low number of features. For this reason more data was collected.

![ResidPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/RsdlsRdg.png)
![Regplt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/ActVsProjSlsRdg.png)

## The final model
A Random forest regressor was used for this model as it is better suited to finding more subtle patterns in the data than a ridge regression as is not as likely to overfit as a neural network.  This model shows the greatest improvement over the first model with a test r2 score of .32 and an MAE of .58.  Compared to the second model the homoskedasticity of this model was far more evident. This data had shown a greater distribution about the mean as demonstrated in the reg plot and the residuals plot has shown the data points grouped closer to the zero line.  The accuracy had increased in this model over the original as had been illustrated in how the larger predictions fall along the projected values in both graphs demonstrating a better ability to predict on the dependent variables.  Given all of this, this model could still be modified to improve its accuracy and MAE scores.

![ResidPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/ResidRFR.png)
![RegPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/LinregRFR2.png)

## Future Improvement
Using feature engineering and hypertuning will help improve the current model.  More and different models should be considered and improved upon such as a KNearest Neighbors regressor or using boosting could improve the MAE score or the accuracy.  If the models don't show as much improvement as desired a final step would be to find more data by scraping it from a website or making another API request. Then engineer more features such as what franchise the game belongs to rather than simply if it belongs to a franchise, if the game is multiplayer, or the games ESRB rating using that data.  This information might give a better understanding of whether the game would be played by a particular target audience, how popular it might be, or possibly how the sales might be restricted due to the target age group or genre.  Then begin working with the models again to see if there is any improvement in the models that showed the most promise.
