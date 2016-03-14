## A/B Testing 
### Project Report by Ashutosh Singh
-------------------------------------

#### Experiment
In the experiment, Udacity tested a change where if the student clicked
"start free trial", they were asked how much time they had available to
devote to the course. If the student indicated 5 or more hours per week,
they would be taken through the checkout process as usual. If they
indicated fewer than 5 hours per week, a message would appear
indicating that Udacity courses usually require a greater time
commitment for successful completion, and suggesting that the student
might like to access the course materials for free. At this point, the
student would have the option to continue enrolling in the free trial, or
access the course materials for free instead.




#### Measuring Variability


##### Measuring Standard Deviation

|Evaluation Metric| Standard Deviation|
|------------------|------------------|
|Gross Conversion |   0.020230      |
|Retention        |	  0.05494		|
|Net Conversion |     0.0156   |

For Gross Conversion and Net Conversion the unit of diversion is same i.e.,
cookie and also the unit of analysis is the person clicking on the 
"Start Free Trial" button. They are highly correlated but we cannot be sure that
they are same for some cases where a person has checked the course on the 
personal computer but lated used the mobile device to click on the course. But 
these cases may be seldom and hence it can assumed that the analytical standard
deviation and the empirical standard deviation will be close.

For Net Retention the unit of diversion (cookie that clicked on the Start Free
Trial button) and the unit of analysis (the user-id of the person enrolled) are 
not exactly equal. Hence we need to collect more data for the empirical analysis.


#### Sizing

##### Choosing Number of Samples given Power

To calculate the number of samples required for each setup. I used the
[Evan Miller's calcutor](http://www.evanmiller.org/ab-testing/sample-size.html).
The values are calculated in the table below. alpha = 0.05 and beta = 0.2 is 
chosen.i9h 

|Metric|Probability|Dmin|Page views| Total Page Views|
|------|-----------|-----|----------|-----------------|
|Gross Conversion Rate | 0.20625 | 0.01 | 25,835 | 645,875  |
|Retention | 0.53 | 0.01 | 39,115 | 4,741,212 |
|Net Conversion | 0.109135| 0.0075 | 27413	|685,325 |

Total Number of pageviews Required (max of all) = 4,741,212


##### Duration vs. Exposure

I decided to not use the Bonferroni Correction **Insert reason here for why 
Bonferroni is not good for Correlated values** The statisctial significance
level is chosen to *0.05* 

**Calculating Duration**



