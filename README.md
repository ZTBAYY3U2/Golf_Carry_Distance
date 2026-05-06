# Golf_Ball_Carry_Distance

## Goal
Build a Linear Regression model to take Launch monitor data and use these variables to predict carry distance. 

## Executive Summary.

The project aim was to see what factors are driving carry distance of a golf ball and if it was possible to predict ball carry distance using variables gathered from a launch monitor. A second objective was using these findings; can recommendations be made on what areas should be prioritised to increase ball carry distance. 
Using data obtained from an amateur golfer in a TopTracer Driving range, Alteryx was used to build a Linear Regression model to predict the total carry distance of a golf ball. The model resulted in a R2 value of 0.797 and Mean Absolute Error of 8.4 yards. 
The coefficients from the model indicated that for every 1m/s of additional ball speed, the carry distance would increase by 3.479 yards. Golfers wishing to increase their carry distance should focus on faster ball speed. 

## Data.
The data in this project was obtained from a driving range equipped with a Top Tracer launch monitor. The data collected consists of 196 observations, with data pertaining to the club used, the loft of the club, carry distance (yards), ball speed (m/s), launch angle (degrees) and Strike quality amongst others. Currently due to the small sample size, strike quality has not been used in the project, however, if more observations are added to the overall data, it is something that could be considered without shrinking the sample size. This sample of data also only relates to one amateur golfer, which may impede bias if providing general advice. 

## Scrutiny of data.
The dataset is a small sample; however, it could have further observations added as time goes on. Research for similar publicly available datasets found minimal publicly available data. One found was a Kaggle dataset (https://www.kaggle.com/datasets/jamieb122/golf-swing-and-trajectory-data?select=golf_trajectory.csv) however the data here omitted to state if only one or multiple clubs were used and which clubs were used. 

## Tools.
The tools used in this Project were Alteryx and Excel, these are readily available in the business. Alteryx allows for repeatability, clear and documented workflows, which also allow for easy debugging and model change. Excel was used for manual data entry due to the smaller sample size, should the project increase in observations other solutions may be a consideration such as snowflake SQL. 

## Engineering.

Preparation for the dataset required manual intervention as the TopTracer app does not allow for exporting the data. The data needed to be manually input to excel. Whilst this could lead to human error, due to the smaller sample size, it was manageable. If multiple sessions were captured with more observations, a request to Top tracer may be required to extract the data. The data also contains the Club Number, which allows joining to further publicly available data on the specific clubs to obtain the stated loft from the manufacture ((https://ping.com/en-us/clubs/irons/g425) Ping have since removed the data from their website, but was correct at the time of the project) This allowed for further analysis later in the project. The joining of this data was done in excel using VLOOKUPs on club number in the main data and bringing in the loft of that club from the Ping data. As previously mentioned, strike quality was also recorded but not used in this project due to constraining the data further. Strike quality was recorded on site as it could not be recorded natively in the TopTracer data. This data was captured on Excel and each shot recorded. This was also Joined in excel and VLOOKUPs as part of the engineering stage. Data was then formatted in Excel to ensure consistency. As previously mentioned, using strike quality would help eliminate outliers in the data, however due to the small sample size, it was not used, this would be the preferred method of removing outliers as “Bad” shots could be removed from the data. 

## Data Visulisation.
Initial EDA and Data visualisation pulled out the below visuals from the data. 

![EDA](Images/EDA/My%20Data%20averages%20by%20club.jpg)
``
The above table shows the average carry, ball speed, launch angle and max carry for each club. The order is shortest club starting a W (Pitching Wedge) leading to the longest tested being a Three hybrid. We can see from the Average data that the shorter the Club, on average, it will travel less distance. In golf, the higher the club number the more lofted and shorter the club is, which typically leads to shorter shots. 

![EDA](Images/EDA/My%20Golf%20Average%20Carry%20By%20Handicap.jpg)
``
Comparing these averages to Amateur data above obtained from My golf Spy(https://mygolfspy.com/news-opinion/instruction/mid-iron-distance-chart-what-is-average-for-your-handicap/) it indicates this data would be indicative of a handicapped golfer between 15-10. For comparison a professional golfer according to the latest data released from Trackman (https://www.trackman.media/tour-averages) typically carries a 6 Iron 188 and a 8 Iron 164 yards as seen below. 

![EDA](Images/EDA/Trackman%20Tour%20Averages.jpg)

![EDA](Images/EDA/My%20Data%20-%20Ball%20speed%20vs%20carry%20distance%20scatterplot.pdf)

![EDA](Images/EDA/My%20Data%20-%20Club%20Loft%20vs%20Carry%20Distance%20Scatter.pdf)

Looking back at the source data, the above 2 scatterplots show the correlation between ball speed and carry distance and the relationship between club loft and carry distance. Carry distance has a positive relationship with Ball speed showing the faster the ball is travelling, the further it should travel. The Club loft shows the lower the club loft typically the ball will carry further. Which also correlates to the below left scatter plot which shows the higher the launch angle, the less distance it will carry. The below right scatter plot shows the relationship between launch angle and Club Loft again it proves the general trend that the lower the loft on the club, the lower the launch angle and the further the ball could travel. Whilst outliers do exist in the data, they do represent a true reflection of the data. Once again, if there were more observations in the data, strike quality could be used, which could decrease the outliers. For reference, mishits account for 28% of the dataset which is why they have been included.

![EDA](Images/EDA/Mishit%20stats.jpg)

![EDA](Images/EDA/My%20Data%20-%20Launch%20Angle%20vs%20carry%20distance%20scatterplot.pdf) 

![EDA](Images/EDA/My%20Data%20-%20Club%20Loft%20vs%20Launch%20Angle%20%20scatterplot.pdf) 

Using the Association Analysis tool in Alteryx, and specifically using the Pearson Correlation table it generates, it was identified that the highest three correlating variables with carry distance were, Ball Speed (0.78), Hang time (0.47) and Club Loft (-0.52). 

![EDA](Images/EDA/My%20Data%20%20-%20Correlation%20Table.jpg) 

## Data Analysis.

The model was built using Alteryx, the data was loaded, an auto field tool ran to ensure numbers are recognised as numbers, data was removed under the select tool, the data removed included Strike metric data, shot number, club number and directional data. A sample created using an 80 -20 split and then fed into various Linear regression tools to assess which model would be best to use. Linear regression was selected for this project as the dependant variable is continuous (carry Distance), reviewing (https://www.geeksforgeeks.org/machine-learning/ml-linear-regression/) also shows this to be a valid choice of tool. 

![Model](Images/Model/Model%20Alteryx%20Workflow.jpg) 

Three models were evaluated, one using all variables, one with the top three correlating variables and one using Ball speed and Launch angle. Upon evaluating the R2 from all models, using all variables had the highest R2 so was adopted for this project.
![Model](Images/Model/Model%20Comparison.jpg) 

The selected model’s adjusted R2 value was 0.797 with a MAPE of 0.069 again indicating the model can predict carry distance with strong confidence and thus reaffirming the decision to opt for this model. 

![Model](Images/Model/Model%20Results%20-%20My%20Data.jpg) 

The coefficients also indicated the following.
-	Ball speed, for every 1 additional Meter Per second of ball speed, total carry would increase by 3.79 yards.
-	Hang time, for every additional second of hang time the model estimated 10.5 additional yards of carry distance.

![EDA](Images/EDA/My%20Data%20-%20Coefficient%20table.jpg) 

Overall, the model shows that increasing ball speed, launch angle and Hangtime would mean the ball travels a further distance. Breaking this down further, it could be argued that hangtime is a product of ball speed and Launch angle, so increasing these alone could result in further carry distances. Should the project be repeated and observations increased, strike quality could also be introduced as an additional variable. 
The model overall performed well. Comparing the average from the original data vs the estimated averages. On average the model under predicted carry by 4 yards, which is consistent with the MAPE being 8.4 yards, with some clubs being predicted with more accuracy, such as the 9 Iron and W(Pitching Wedge) Some clubs such as the 6 Iron and 8 iron had higher variance and this may be down to the data itself and that each shot recorded may not have been a perfect strike. 

![Model](Images/Model/Model%20Predictions.jpg) 

Brožka, M., Gryc, T., Miřátský, P. and Zahálka, F., 2022. An assessment of the relationships between ball flight results, impact factors, and golf performance. Human Movement, 23(1), pp.1-9. concluded that “Ball flight distance depends on the quality of contact between the club and the ball (the smash factor) and the initial ball speed” Whilst in this dataset Smash Factor was not an observation, obtaining data from a launch monitor which does capture this data or captures club head speed, would be a suitable alternative to include. The Smash Factor is a calculation derived from Ball Speed / Club head Speed as mentioned by England golf. (https://englandigolf.co.uk/igolf-blog/blog-archive/smash-factor-in-golf/)

## Improvements.
If this project were to be repeated or continued, the data would be expanded upon to gather more observations as it is limited in its current form (198). It should be noted that in the data, strike quality was observed, however, it was not mentioned in the report as, due to the small number of observations it would further limit the study. If expanded, this could certainly be a variable that would alter the results as it could explain anomalies. Furthermore, to eliminate bias, obtaining data from various golfers of different skill levels would also improve global recommendations and help eliminate bias. This would also allow for more generic advice to be obtained from this project, rather than how this impacts one individual. 

## Overall Outcome. 
The model shows that the main factor that impacts carry distance is Ball Speed, however, it should be noted that due to the small sample size it would be difficult to fully extrapolate, however with what has been observed we can ascertain that, for every 1m/s of additional ball speed, the ball should travel a further 3.79 yards. From a coaching point of view from this sample size, a focus should be to increase ball speed, which would have a positive impact on improving distance. 



