# Golf_Ball_Carry_Distance

## Goal
Build a Linear Regression model to take Launch monitor data and use these variables to predict carry distance. 

## Executive Summary

The project aim was to see what factors are driving carry distance of a golf ball and if it was possible to predict ball carry distance using variables gathered from a launch monitor. A second objective was using these findings; can recommendations be made on what areas should be prioritised to increase ball carry distance. 
Using data obtained from an amateur golfer in a TopTracer Driving range, Alteryx was used to build a Linear Regression model to predict the total carry distance of a golf ball. The model resulted in a R2 value of 0.797 and Mean Absolute Error of 8.4 yards. 
The coefficients from the model indicated that for every 1m/s of additional ball speed, the carry distance would increase by 3.479 yards. Golfers wishing to increase their carry distance should focus on faster ball speed. 

## Data
The data in this project was obtained from a driving range equipped with a Top Tracer launch monitor. The data collected consists of 196 observations, with data pertaining to the club used, the loft of the club, carry distance (yards), ball speed (m/s), launch angle (degrees) and Strike quality amongst others. Currently due to the small sample size, strike quality has not been used in the project, however, if more observations are added to the overall data, it is something that could be considered without shrinking the sample size. This sample of data also only relates to one amateur golfer, which may impede bias if providing general advice. 

## Scrutiny of data
The dataset is a small sample; however, it could have further observations added as time goes on. Research for similar publicly available datasets found minimal publicly available data. One found was a Kaggle dataset (https://www.kaggle.com/datasets/jamieb122/golf-swing-and-trajectory-data?select=golf_trajectory.csv) however the data here omitted to state if only one or multiple clubs were used and which clubs were used. 

## Tools
The tools used in this Project were Alteryx and Excel, these are readily available in the business. Alteryx allows for repeatability, clear and documented workflows, which also allow for easy debugging and model change. Excel was used for manual data entry due to the smaller sample size, should the project increase in observations other solutions may be a consideration such as snowflake SQL. 

## Engineering

Preparation for the dataset required manual intervention as the TopTracer app does not allow for exporting the data. The data needed to be manually input to excel. Whilst this could lead to human error, due to the smaller sample size, it was manageable. If multiple sessions were captured with more observations, a request to Top tracer may be required to extract the data. The data also contains the Club Number, which allows joining to further publicly available data on the specific clubs to obtain the stated loft from the manufacture ((https://ping.com/en-us/clubs/irons/g425) Ping have since removed the data from their website, but was correct at the time of the project) This allowed for further analysis later in the project. The joining of this data was done in excel using VLOOKUPs on club number in the main data and bringing in the loft of that club from the Ping data. As previously mentioned, strike quality was also recorded but not used in this project due to constraining the data further. Strike quality was recorded on site as it could not be recorded natively in the TopTracer data. This data was captured on Excel and each shot recorded. This was also Joined in excel and VLOOKUPs as part of the engineering stage. Data was then formatted in Excel to ensure consistency. As previously mentioned, using strike quality would help eliminate outliers in the data, however due to the small sample size, it was not used, this would be the preferred method of removing outliers as “Bad” shots could be removed from the data. 

## Data Visulisation
Initial EDA and Data visualisation pulled out the below visuals from the data. 

![EDA](Images/EDA/My%Data%averages%by%club.jpg)
``







