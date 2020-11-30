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
Since the introduction of the Nintendo Entertainment System in 1985 there has been a proliferation of new and more advanced gaming systems and videogames introduced to the global market. Though many companies likely have methods and tools to predict the success of new videogames, new and emerging tools may better position game publishers to determine the potential success of a game based on previous sales of video games with similar atributes. Putting predictive tools in the hands of video game manufacturers and marketers may reduce their risk of releasing a game that may not give a good return on investment and allows the company to invest thier resources in projects that would have a higher likelihood of success. 

## Data Understanding
The [Sglobale DataFrame](https://data.world/julienf/video-games-global-sales-in-volume-1983-2017) contains over 16,500 records of the sales of individual videogames in each major market from 1980 through 2020 including North America, Europe, and Japan ranked by the total global sales for that game.  The data for the games are common to each market and also contians the title, platform, genre, and publisher of each.  Since multicollinearity was an issue with this data, more data was collected using an API request from [IGDB](pi-docs.igdb.com/#about), the code to which can be found in the [IgdbApiNotebook](https://github.com/RCKettel/CapstoneProject/blob/main/Notebooks/IgdbApiNotebook.ipynb).  This data contains numerous rows that have information about some of the games that are included in the Sglobale dataframe.  The rows contain contain codes for representations of the data in each column.

![YearlyEarnings](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/GsalesScatter.png)

## Data Collection
To collect data from IGDB create a twitch account. If the instructions are follwed at the account creation site for Twitch.tv there shouldn't be a major problem. When filling in the application the OAuth url was set as "http://localhost" to let the system know the data will be run locally then choose analytics tool from the category menu. Once the application is accepted a client ID is assigned to you and you can ask for a client secret. Though this secret is used in the code to collect the data it should not be made public. As such once the code has been run it should be written down or saved to the computer and then deleted from the code. Once the client ID and client secret have been collected an access token will be needed to collect the data from IGDB. The request URL is found under the authentification section of the instructions and the client ID and client secret can be filled in to make a successful request. A wrapper was created to deliver the data in a format comptible with python under wrappers, however, the readme file that shows how to run the data contains an issue that throws an error. The solution can be found in a discussion entitled 'Main Readme Example Does Not Work' under the issues tab.  The data collected was for the games in the sglobal dataframe so the names of the games were used to identify which game data should be returned. This did not mean that the website would have data on all the games requested so a try/except was set up to allow the request to return None if there was no data so that the request would not throw an error if there were a NaN value. The final issue to consider when working with this API is that the rate limit for requests is four per second. For this reason, a counter was set up to space out the information returned which told the machine to wait if it thought the rate would exceed the limit.

## The First Model
This model, a linear regression, was run to identify how well a regression would fit to the features using a basic supervised model without any regularization. The results clearly show the model does not perform well with the features as they are. The low r2 score of .16 in tandem with a high MAE of .71 in the results of the training data show a low distrbution about the mean and low accuracy in the predictions of the model. In addition, the even lower r2 and much higher MAE in the validation scores show the model does not generalize well to new data proving underfitness and a possible need for regularization.

## The Second Model
Ridge Regression was chosen to adjust the coefficients without lowereing them to zero in order to lower the variance thereby raising the scores from the validation data.  This did not prevent the model from being underfit. The training data in this model gave results that were nearly identical to those in the linear regression model the difference being a negligible increase in the r2 score.  The greatest difference for this model was in the scores from the test data.  The r2 score at .15 and the MAE at .76 are a dramatic change in comparison to the original scores returned by the linear regression model. However, the reg plot has shown the difficulty the model had in predicting on a dependent variable, by visualizing more easily where the data is better predicted at lower values than at higher values and how the reliability of the predictions were somewhat untrustworthy. Meanwhile, the residuals plot demonstrated the necessity to move away from a more basic linear regression where it had shown the heteroskedasticity of the data.  When the data was chosen, it was predicted the lower number of features would affect the predictions of the data.  For this reason, more data was collected.

![ResidPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/ModOneRsdPlt2.png)
![Regplt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/ModOneRegPlt.png)

## The final model
Compared to the first model the homoskedasticity of this model is far more evident. This data shows a greater distribution about the mean as demonstrated in the residuals graph and the reg plot. Given all of this, the accuracy has increased in this model over the original as can be seen in how the larger predictions fall along the projected values in both graphs demonstrating a better ability to predict on the dependent variables.

![ResidPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/FnlMdlRsidPlt2.png)
![RegPlt](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/FnlMdlRegPlt.png)

## Future Improvement
Using feature engineering and hypertuning will help improve the current model.  More and different models should be considered and improved upon to find of other models such as a KNearest Neighbors regressor or using boosting could improve the MAE score or the accuracy.  If the models don't show as much improvement a would be desired a final step would be to find more data and engineer more features using that data. Then begin working with the models again to see if there is any improvement in the models that showed the most promise.
