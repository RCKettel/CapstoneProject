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
Since the introduction of the Nintendo Entertainment System in 1985 there has been a proliferation of new and more advanced gaming systems and videogames introduced to the global market.  Though many companies likely have methods and tools that would predict the success of new videogames, new tools could help game publishers determine the success of a game based on previous sales.  This may reduce the risk of a game that does not give a good return on investment and allow the company to invest thier resources in projects that would have a higher likelihood of success. 

## Data Understanding
The [Sglobale DataFrame](https://data.world/julienf/video-games-global-sales-in-volume-1983-2017) contains over 16,500 records of the sales of individual videogames in each major market from 1980 through 2020 including North America, Europe, and Japan ranked by the total global sales for that game.  The data for the games are common to each market and also contians the title, platform, genre, and publisher of each.  Since multicollinearity was an issue with this data, more data was collected using an API request from [IGDB](pi-docs.igdb.com/#about), the code to which can be found in the [IgdbApiNotebook](https://github.com/RCKettel/CapstoneProject/blob/main/Notebooks/IgdbApiNotebook.ipynb).  This data contains numerous rows that have information about some of the games that are included in the Sglobale dataframe.  The rows contain contain codes for representations of the data in each column.

![YearlyEarnings](https://github.com/RCKettel/CapstoneProject/blob/main/Resources/Images/GsalesScatter.png)

## Data Collection
To collect data from IGDB create a twitch account. If the instructions are follwed at the account creation site for Twitch.tv there shouldn't be a major problem. When filling in the application the OAuth url was set as "http://localhost" to let the system know the data will be run locally and choose analytics tool from the category menu. Once the application is accepted a client ID is assigned to you and you can ask for a client secret. Though this secret is used in the code to collect the data it should not be made public, as such once the code has been run it should be written down or saved to the computer and then deleted from the code.  Once the client ID and client secret have been collected an access token will be needed to collect the data from IGDB. The request URL is found under the authentification section of the insructions and the client ID and client secret can be filled in to make a successful request. A wrapper was created to deliver the data in a format comptible with python under wrappers, however, the readme file that shows how to run the data contains an issue that throws an error. The solution can be found in a discussion entitled 'Main Readme Example Does Not Work' uner the issues tab.  The data collected was for the games in the sglobal dataframe so the names of the games were used to identify which game data should be returned. This did not mean that the website would have data on all the games requested so a try/except was set up to allow the request to return None if there was no data so that the request would not throw an error if there were a NaN value. The final issue to consider when working with this API is the rate limit for requests is four per second. For this reason, a counter was set up to space out the information returned and told the machine to wait if it thought the rate would exceed the limit.


