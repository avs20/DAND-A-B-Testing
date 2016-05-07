## A/B Testing
### Project Report by Ashutosh Singh
-------------------------------------

#### Experiment
In this experiment, Udacity tested a change where if the student clicked
"start free trial", they were asked how much time they had available to
devote to the course. If the student indicated 5 or more hours per week,
they would be taken through the checkout process as usual. If they
indicated fewer than 5 hours per week, a message would appear
indicating that Udacity courses usually require a greater time
commitment for successful completion, and suggesting that the student
might like to access the course materials for free. At this point, the
student would have the option to continue enrolling in the free trial, or
access the course materials for free instead.

#### Metric Selection

**Number of Cookies** -  *INVARIANT* This metric will not change with the experiment as the
number of users visiting Udacity will not change as they have been not yet part
of the experiment.

**Number of user-ids** - *NONE* This will not be an invariant metric because the
number of enrolled users may depend on the rendered page and we may see different
values in the groups. This metric can be an evaluation metric but it is just a
number and Gross Conversion does a better job at counting the number of users and
also the affect of the *5 hour commitment question*.

**Number of click** - *INVARIANT* Same argument as the number of cookies. The
experiment has still not started so this metric will be invariant.

**Click-through-probability** - *INVARIANT* The user has still not seen the
experiment so this will not be different in the control and experiment groups.

**Gross conversion** - *EVALUATION* This is a metric we would like to evaluate.
It depends on how the page has rendered after clicking the START FREE TRIAL button.
We would like to know how showing a form with commitment questions changes the
enrollment. Based on the hypothesis this metric will be *lower* as the user likely
to drop after seeing the question will be filtered.

**Retention** - *EVALUATION* Same as in case of gross conversion. We would like to
find out if the users who see the *5 hours commitment* question have more or less
rate of remaining enrolled. This will become higher according to hypothesis as
the those who have enrolled would be less likely to drop and those who would have
dropped are already filtered.

**Net Conversion** - *EVALUATION* This metric is the ratio of Retention and
Gross-Conversion. It gives us the big picture idea of how many users clicked
the START FREE TRIAL button and how many remained. This metric should increase
Retention will increase and Gross conversion will decrease and the ratio will
increase.


#### Measuring Variability


##### Measuring Standard Deviation

|Evaluation Metric| Standard Deviation|
|------------------|------------------|
|Gross Conversion |   0.020230      |
|Retention        |	  0.05494		|
|Net Conversion |     0.0156   |



For Gross Conversion and Net Conversion the unit of analysis is same i.e., cookie.
Since the unit of diversion is also cookie hence the analytical estimate will
match the empirical standard deviation from the experiment.

For Net Retention the unit of diversion (cookie that clicked on the Start Free
Trial button) and the unit of analysis (the user-id of the person enrolled) are
 different. Hence the analytical estimate will be different from empirical
 standard deviation for Retention.


#### Sizing

##### Choosing Number of Samples given Power

To calculate the number of samples required for each setup. I used the
[Evan Miller's calcutor](http://www.evanmiller.org/ab-testing/sample-size.html).
The values are calculated in the table below. alpha = 0.05 and beta = 0.2 is
chosen.i9h

| Metric                | Baseline Conversion Rate | Dmin   | Page views | Total Page Views  |
| ------                | ----------- | -----  | ---------- | ----------------- |
| Gross Conversion Rate | 0.20625     | 0.01   | 25,835     | 645,875           |
| Retention             | 0.53        | 0.01   | 39,115     | 4,741,212         |
| Net Conversion        | 0.109135    | 0.0075 | 27413	     | 685,325          |

Total Number of pageviews Required (max of all) = 4,741,212


##### Duration vs. Exposure

The statistical significance level is chosen to *0.05*

**Calculating Duration**

Keeping retention rate as evaluation metric will make the experiment go
much longer(4.7 million page views will take approx. 4 months on full
site traffic). Hence I am dropping the retention rate as evaluation
metric and use only Gross Conversion Rate and Net Conversion. This makes
the total number of page views to **685,325**.

**Exposure**

The exposure of the experiment is based on the risk involved. Since for the
experiment only a small reminder is shown about the time commitment. There will
be no physical harm to the users. Also since no sensitive information is being
collected therefore a 100% exposure is safe.

For the number of page views per day (40000) and a 100% exposure, it would take
us around 18 days for the experiment.

I chose not to use the Bonferroni Correction because the two metrics Gross Conversion
and Net Conversion are highly correlated.

##### Experiment Analysis

###### Sanity Checks

For each metric which is chosen as invariant metric I perform the sanity
checks. Following table shows the process and values for this

####### Number of Cookies

|    Data | Values    |
|----------|----------|
| Control Group | 345543 |
| Experiment Group | 344660 |
|Standard Deviation | 0.0006018|
|Margin of Error| 0.0011796 |
|lower bound | 0.4988|
|upper bound | 0.5012 |
|observed value | 0.5006|

***The observed value is within the 95 %CI  hence this invariant
metric passes the sanity check.***


###### Number of clicks on "Start Free Trial"


|    Data | Values    |
| ----------|----------|
| Control Group | 28378 |
| Experiment Group | 28325 |
|Standard Deviation | 0.0021|
|Margin of Error| 0.0041 |
|lower bound | 0.4959|
|upper bound | 0.5041|
|observed value | 0.5005|

***The observed value is within the 95 %CI  hence this invariant
metric passes the sanity check.***


##### Click-through-probability on "start free trial"

|    Data | Values    |
|----------|----------|
|Control Value | 0.0821258 |
|Standard Deviation | *sqrt(0.5 * (1-0.0821258) / (344660))* = **0.000468**|
|Margin of Error| *1.96 *0.000468* = **0.00092** |
|lower bound | *0.0821258 - 0.00092* = **0.0812**|
|upper bound | *0.0821258 + 0.00092* = **0.0830** |
|observed value | 0.0821258 (given)|

***The observed value is within the 95 %CI  hence this invariant
metric passes the sanity check.***

----------------------------------------------------------------


#### Effect Size Tests

Since we are using Gross Conversion and Net conversion as the evaluation metrics
following are the confidence intervals for them.

|Metric | Lower bound |  Upper Bound | Statistical significance | Practical significance |  
|-------|-------------|--------------| -------------------------|-------------------------|
|Gross Conversion | -0.0291 | -0.0120|  Yes | Yes |
|Net Conversion   | -0.0016 | 0.0019  | No | No |

Statistical significance is determined if the confidence interval does not contain
0 and Practical significance is determined if the interval does not include
*d-min* of 0.01 as decided in experiment.

#### Sign Tests

I used the graphpad calculator for the Sign test (link in References).

1. **Gross Conversion**

   |Calculation |  Value |
   |------------|---------|
   |# of successes | 4    |
   |# of Trials    |23    |
   |Probability    | 0.5  |
   |p-value ( 2-tailed ) | 0.0026 |

 Since the p-value is less than the alpha value o 0.05, hence the difference is
 statistically significant .

2. **Net conversion**

 |Calculation |  Value |
 |------------|---------|
 |# of successes | 10    |
 |# of Trials    |23    |
 |Probability    | 0.5  |
 |p-value ( 2-tailed ) | 0.6776 |

 The p-value for Net conversion is greater than the alpha value of 0.05, hence
 this difference is not statistically significant.

#### Summary

 I have decided to not use Boneferroni Correction because our decision is based
 upon the **both** Gross Conversion and Net Conversion metrics. The hypothesis
 requires that both the effects be considered and we cannot go ahead with one
 metric alone. Hence Bonferroni correction will not be appropriate here.


### Recommendation

The hypothesis of the experiment was

*... that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time—**without significantly reducing the number of students to continue past the free trial and eventually complete the course**. If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.*

The main points were

1. Reducing the number of frustrated students as they didn't have enough time
2. Without reducing the number of students to continue past the free trial.

Based on the hypothesis it was predicted that the Gross Conversion Rate will go
down which occured in the statistically and the practically significant way.

For Net Conversion rate and the second point above we find that the experiment
was unable to keep the numbers of student continue past the free trail unaffected.
Infact based upon the confidence interval for the Net conversion it is possible
that the *5 hours commitment* might have increased the number of students who
leave free trial.

Based on the above observations and our experiments goal. I would recommend to **
not launch** this experiment.


### Follow up Experiment


The goal of the follow up experiment is to reduce the frustration of the free
trial students. Why are students frustrated?

1. They didn't understand the course materials.
2. They slack off after some time as in new year's resolution
3. Unlike the college based education where we can see our companions move
forward daily there is no companion in online education.
4. They can't devote enough time for the Nanodegree.

Based on above points I propose the following experiment

*Give users notifications/space to interact more during the trial period like using
forums, online chat channel, etc. A section on the course page dedicated to directly
interact with users on the same course. A link to slack channel will be great.
Or if the user is taking more time to solve a problem then pop up a notification
on the side to interact with others. *

My hypothesis is that there may be many reasons for the frustration and as
discussed above many times no part of companionship will make a student aloof.
When a human being interacts with others often then a social feeling
 emerges and makes one a part of community.
Interaction with other students will make the user more frank to be communicating
with others and a group/cohort bonding may emerge.

**Unit of diversion :** *user ids who have enrolled in the free trial*. Since the
experiment will start after the enrollment and the user has logged in, we
can easily divert them to either the control and experiment group.

Invariant Metrics :

* *Number of user ids to complete checkout and enroll in free trial* :
Since this experiment will activate on user login
hence the number of user ids enrolled will be unaffected by this experiment.

Evaluation Metrics :

* *Retention Rate* : Retention rate will be the best metric for this experiment
as this can quantify the number of users who checkout and kept enrolled.

The Retention rate as evaluation metric will make the experiment last longer.


#### References

1. [Graphpad Sign Test calcutor](http://graphpad.com/quickcalcs/binomial2/)
2. [What's wrong with Bonferroni correction](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC1112991/)
3. [Statistical Analysis and A/B Testing](http://20bits.com/article/statistical-analysis-and-ab-testing)
