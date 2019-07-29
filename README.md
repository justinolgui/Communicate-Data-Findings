# Udacity - Communicate Data Findings 
## by Justin Olgui


## Dataset: Loan Data from Prosper

# Preliminary Wrangling

This dataset contains data from over 100,000 prosper loans.
Each row contains information about a specific loan that was funded through the Prosper marketplace.

#### Who is prosper?
Prosper is a San Francisco based company in the peer-to-peer lending marketplace in the United States. Since 2005, Prosper has facilitated more than $15 billion in loans to more than 930,000 people.

#### What is peer2peer lending?
For those who are not familiar, Prosper does not actually lend money, they essentially provide a marketplace for lenders and borrowers to meet, think online dating for loans. As a prospective borrower, you would go through the process of filling out an application, why do you want money, how much do you make, are you employed and so on. They will then assign you a Prosperscore and put your loan up on their marketplace at which point lenders who are looking for higher rate investment returns can choose to fund a portion, or the entirety of your loan. Some of the information on our borrower includes but is not limited to APR, Employment status, credit rating, term, occupation, etc.

### What is the structure of your dataset?

This dataset contains 113937 loans with 81 different variables.
Our column definitions can be found in "Prosper Loan Data - Columns Definitions.csv"
What are the main features of interest in your dataset?

Through our exploration i'm wanting to answer some of the following questions I have:

- Who are the borrowers? (financial health, income levels, debt ratios, etc.)
- Why are they borrowing money?
- How much are they paying in interest?
- Are these metrics changing over time?

My objective is to better understand what are the most significant factors in obtaining reduced rates and are those factors changing over time?

What features in the dataset do you think will help support your investigation into your features of interest?

This dataset is filled with a ton of personal information on our borrowers. Some of the standard finance metrics are quite helpful on their own. (DebtToIncomeRatio, CreditGrade, StatedMonthlyIncome, RevolvingCreditBalance, BorrowerAPR, etc.) However by combining these variables I think we should be able to gather some interesting insights and better understanding our borrowers.

Of the features you investigated, were there any unusual distributions? Did you perform any operations on the data to tidy, adjust, or change the form of the data? If so, why did you do this?

There were some outliers in some of the columns that i had to remove I also added some new columns:

- Added a Quarters column to group Listing dates by Quarter
- Added a new Credit Score column that is the mean of the Upper and Lower Credit Score range columns
- Converted the ListingCategory col to a category datatype
- Changed numerical value to the category they were given with the definition provided
- Removed all monthly income above 15,000
- Removed DTI above 1
- Removed RevolvingCreditBalance above 85,000
- Removed Credit Scores below 500
- Removed Monthly Loan payments above 699

#### Variable Defintions

Taken from our Prosper Loan Data - Columns Definitions.csv that was provided with the dataset I will now define the individual variables i have selected for my analysis:

__CreditScoreMean:__ This column is the mean of CreditScoreRangeLower and CreditScoreRangeUpper.<br>

__ProsperScore:__ A custom risk score built using historical Prosper data. The score ranges from 1-10, with 10 being the best, or lowest risk score.  Applicable for loans originated after July 2009.<br>

__Term:__ The length of the loan expressed in months.<br>

__MonthlyLoanPayment:__ The scheduled monthly loan payment.<br>

__StatedMonthlyIncome:__ The monthly income the borrower stated at the time the listing was created.<br>

__BorrowerAPR:__ The Borrower's Annual Percentage Rate (APR) for the loan.<br>

__DebtToIncomeRatio:__ The debt to income ratio of the borrower at the time the credit profile was pulled. This value is Null if the debt to income ratio is not available. This value is capped at 10.01 (any debt to income ratio larger than 1000% will be returned as 1001%).<br>

__RevolvingCreditBalance:__ Dollars of revolving credit at the time the credit profile was pulled.<br>

__BorrowerState:__ The two letter abbreviation of the state of the address of the borrower at the time the Listing was created.<br>

__ListingCategory:__ Determines the category of loan that the borrower needs money for.<br>


## Summary of Findings

#### Loan Origination by Quarter
The first thing that jumps out to me is that at Q3 of 2008 prosper loans essentially fell off a cliff. The timing is peculiar because this is when the economic crisis of 2008 came to light, this was no coincidence. Prosper was clearly hit hard by this economic downturn. Since then Prosper has experienced some serious growth. Aside from the Q4 2012 and the Q1 2013 prosper loans have increased quarter over quarter since 2010 at what appears to be a parabolic rate. Let's now inspect the credit worthiness of our borrowers.

#### Borrowers Credit Score<br>
The majority of borrowers having a credit score between 650 and 750. Our mode falls around the 670 mark. According to Experian which is one of the credit report agencies in the US: "a credit score of 700 or above is generally considered good. A score of 800 or above on the same range is considered to be excellent. Most credit scores fall between 600 and 750." We actually have very few in the 600-650 range. I think it's fair to say that our borrowers are slightly above average. Credit score has long been considered the gold standard in determining a borrower's credit worthiness. Let's see how this compares to the relatively new prosper score.

#### Loan ProsperScore<br>
This prosperscore is quite interesting, our mode is a 4 which is quite low. This indicates that most loans are considered to be high risk. This is telling us a very different story from our credit rating.

#### Loan Term<br>
Prosper loans are given in 12, 36 and 60 month terms. It's clear that the majority of our borrowers are opting for a 36 month term.

#### Monthly Loan Payments<br>
The majority of prosper loans monthly payments are below 400, with the highest frequency falling between 150-200. Depending on what other debts a borrower may have these payment amount seem to be quite sustainable and shouldn't have too much of an impact on a borrower's ability to repay. To better understand the impact these payments might have it seems reasonable to next understand the income levels of our borrowers.

#### Distribution of Borrower's Income<br>
It appears as though most of our borrowers have a monthly income of roughly 5,000. This distribution is right skewed with some long tails. Kind of interesting that some of our borrowers have a monthly income over 10K and are choosing to turn towards the P2P lending market. This is self reported income though so who knows how accurate this is. Considering most of the monthly loan payments are around 300 this shouldn't put too much stress on our borrowers. However without knowing what other expenses a borrower has it's hard to make this claim with any certainty. Next I'd like to explore APR to see how much interest our borrowers are paying.

#### Distribution of APR<br>
Our distribution here is almost normally distributed, however it does have a slight right skew. With a large amount of loans in the 0.35 - 0.375 range. The mode is between 0.2 - 0.25, our borrowers must be pretty desperate to accept these loans. These rates are worse than pretty much every credit card there is on the market. A loan with an APR above 0.35 is pretty much usury.

#### Distribution of Borrower's Debt to Income Ratio<br>
This distribution is once again right skewed like the last few we have explored. This is quite surprising to be honest. Based on standard finance metrics the majority of these people seem to be in pretty good financial health. Typically if you have a DTI below 0.36 it's considered to be quite good. The mode of our distribution is below 0.2, I'm quite curious to know why these people are turning to the P2P markets. Could this be the result of strict lending criteria, a lack of financial literacy or is the typical loan approval process just too onerous for our borrowers? Next let's explore how much are these borrowers carrying in revolving balances.

#### Distribution of Revolving Credit Balance<br>
Once again, yet another heavily right skewed distribution. It appears as though most of our borrowers have less than 5,000 in revolving credit balances. This data is counterintuitive, our borrowers seem to be in a pretty good financial situation, and pretty well safeguarded against a financial disaster.

#### Loans by State (Top 20)
It appears as though the majority of our borrowers hail from California, Texas, New York and Florida. This seems to coincide with the fact that these are some of the most densely populated states in the US.

#### Distribution of Loan Categories<br>
This chart just further confuses me, debt consolidation is more than 5 times the count of the next category. Unfortunately the next two are NA and Other which doesn't really provide us with much value. This chart in isolation looks good because you have people actively taking steps to improve their financial situation. On the other hand with a mean APR of nearly 22% you have to wonder what types of loans could they possibly be consolidating that would have a rate higher than that.


## Discuss the distributions of your variables of interest. Were there any unusual points? Did you need to perform any transformations?<br>

I found the exploration quite insightful, as I started my analysis I was quite confused as sone of the data points seem to be telling completely different stories. Once I got to the APR distribution I started to believe that these borrowers must be in severe financial trouble. However most of the other data showed otherwise, they had slightly above average credit scores, very good debt to income ratios and minimal revolving credit balances. They also seem quite financially responsible as they are being proactive in trying to improve their financial situations by opting to consolidate their debt. However with a mean APR of 21.8% these borrowers must have taken on some really bad loans in the past.


## Bivariate Exploration

#### Correlation Matrix<br>
The strongest correlation in our dataset is BorrowerAPR and ProsperScore which have a negative correlation of -66.8 so as ProsperScore increases APR should decrease. BorrowerAPR and CreditScoreMean is the next strongest relationship at -49.9 same idea, CreditScoreMean increases as interest rates decrease. After that the next strongest correlation is CreditScoreMean and ProsperScore which also makes sense since they are essentially different tools trying to achieve the same purpose, quantify the risk of the loan. I chose to mask the top half of the correlation matrix as it is essentially a mirror of the bottom half. I found that with all that extra information that essentially provides no extra value it can be more difficult to interpret the plot as it can be hard to focus at least for me.

#### Pairplot<br>
So when I initially attempted a seaborn pairplot i ran my entire dataset. This took forever and due to the sheer volume of data points it was quite difficult to notice any patterns. As such I decided to switch it up and run a sample of 500 rows instead.
Borrower APR and Prosper Score demonstrate the clearest trend of all our plots, Credit Score and Borrower APR also seem to be linked. Debt to Income ratio and Prosper score also seem to be negatively correlated. We'll first have a look at our categorical levels

#### Borrower APR by State
The majority of the states seem to be quite similar in terms of Median APR however there is quite a difference when we look at the extremes. Maine (ME) has the lowest APR at 0.157 while Alabama has the highest median APR at 0.235, that's a 7.1% difference. Let's now have a look at income by state.

#### Monthly income by State
We can see quite a difference between the median incomes in this plot. North Dakota is our lowest with a median income of 2,666. DC is our highest with a median income of 6,000. DC has the highest median income and the 3rd lowest median APR. Those politicians are working some magic. Something else that is interesting to note Maine has the lowest median APR and also has the 3rd lowest median income at 3,250. Let's see if category has any influence on our APR.

#### BorrowerAPR by Listing Category
So there seems to be a considerable amount of difference in our median APR depending on the purpose of your loan. Personal loan is the lowest at 0.176 and Cosmetic Procedure is the highest at .272 nearly 10 percentage points higher. What strikes me as odd though is that a lot of these categories seem to fit under the personal loan category. Could it be advantageous to be vague when submitting your loan application? We may never know. We'll now explore our numerical variables.

#### BorrowerAPR vs CreditScoreMean<br>
By adding alpha to our plot the relationship starts to become much more clear. There is a negative correlation between credit score and APR. In other words as your credit score increases, your interest rate decreases. This of course is what we would expect. This is a reflection of the inherent risk in lending money, as a borrower demonstrates less risky tendencies, lenders are willing to give the borrower preferred rates. The box plot helps to make this trend visualization a bit more clear.

#### BorrowerAPR vs ProsperScore<br>
This plot shows us a very similar picture to our credit score plot, which of course is to be expected. Higher prosper score equals lower rates. It's a bit hard to say this with any kind of certainty however the prosper score seems to have a much more defined trend. Whereas when you get into the 600-750 range of the credit score we have a much wider of behavior. Could the Prosper score be superior to the credit score? Let's explore that relationship and see if we can draw any conclusions

#### CreditScoreMean vs ProsperScore<br>
This seems like an odd result to me. Our correlation matrix does indicate that there is a 0.381 positive correlation between these variables. This is demonstrated by the fact that once we get above 800 we have very few points below 2. However there are some borrowers with a 650 credit score that have a prosper score above 10. I think the box plot does a better job of representing this relationship. Ranges 1 - 8 seem to have a much stronger relationship with credit score. 9-10 seem to include pretty much the entire range of credit scores with an increasing median. Range 11 seems to be quite odd, we have a higher minimum and also a lower maximum and median, quite odd!<br> 

From the prosper website: 
A custom risk score was built using historical Prosper data to assess the risk of Prosper borrower listings. The output to Prosper users is a Prosper score which ranges from 1 to 11, with 11 being the best, or lowest risk, score. The worst, or highest risk, score, is a 1. Unlike a credit bureau score, which is based on a much wider variety of loan performance, the Prosper score is specifically built on the Prosper borrower and applicant population. As such, the credit reporting agency score should, and does, rank order risk on the Prosper population, but is not as discriminating as the custom score.
<br>

Interesting how even though they use the credit score in their model, it's clearly designed to take other factors in consideration so that it's not as discriminatory. Next I'd like to see the relationship between borrower APR and DTI.

#### BorrowerAPR vs DebtToIncomeRatio<br>
This plot isn't overly exciting. While we can see a slight correlation (0.17) as we start to get into higher debt income ratios we start to notice that our APR starts to rise, however this is nothing to write home about. Let's explore APR vs Stated monthly income.

#### BorrowerAPR vs StatedMonthlyIncome<br>
This plot doesnt offer up too much either. We can see that the majority of our borrowers have an income around 4000 and their APR seems to be all over the place with the highest concentration falling around 0.2 <br>
Let's see the relationship between Income and Payments.

#### StatedMonthlyIncome vs MonthlyLoanPayment<br>
Once again nothing super exciting. We can see a slight correlation, as income rises as our monthly payment rises along with it. 
Up next income vs revolving credit balance.

#### StatedMonthlyIncome vs RevolvingCreditBalance (scatter)<br>
This scatterplot of Income vs Revolving Credit balance doesn't really show us anything interesting. We can see that most borrowers make less than 8000 a month, with the majority making around 4000 a month and having around 20000 in revolving credit. I think it's safe to assume that the majority of these borrowers are taking out loans to consolidate credit card debt.

#### StatedMonthlyIncome vs RevolvingCreditBalance (heatmap)<br>
Tried replotting this graph using heatmap and different bin sizes, this doesn't give us much more to look at. Unfortunately the past few graphs have kind of been a dead end. So let's take this in a different direction. When dealing with money lending interests rates are of huge importance (APR). Let's see how interest rates might be changing over time.

#### APR over time (Q)<br>
This chart has way too much going on. I'm going to change the frequency to year and see if that might give us a clearer picture.

#### APR over time (Y)<br>
By changing to year the trend becomes much more clear, we can see that our median interest rates rose until 2011 at which point it has started to trend downwards. The box plot gives us much more detail than our line plot in this instance. We can see that our all time high in interest rates came in 2010 as indicated by the whiskers however the median peak came a year later in 2012. Since then the median has continued to drop, another piece of information our box plot gives us is that in the past two years the body of our box plots has narrowed and since 2011 the overall range of interest rates has decreased as well this is good news for borrowers, lenders not so much. Could this be the result of less risky borrowers coming into the market?

#### Credit Scores over time<br>
This data doesn't seem to support the idea that we have higher quality borrowers coming onto the platform, credit score ranges were stable between 2009 and 2012, medians were stable between 2009 and 2013. In the past few years credit scores have actually decreased. Could Credit Score be a leading indicator? Unfortunately, I don't think we'll be able to answer that question. How have prosper scores changed over time? ProsperScores had a higher correlation to APR so maybe that can help us see a different perspective.

#### Prosper Scores over time<br>
This data is in line with the credit scores. We're actually seeing lower quality borrowers as time passes. Aside from 2014 it has been a downtrend with median decreasing and the lower quartile decreasing since 2009. As previously stated I'm inclined to believe that risk ratings are a leading indicator and then interest rates will then follow suit as higher levels of defaults are seen. Next I'd like to see have borrowing categories changed over time?


### Talk about some of the relationships you observed in this part of the investigation. How did the feature(s) of interest vary with other features in the dataset?

I found it very interesting that the prosperscore was the number one factor in determining a borrower's APR. This of course makes sense seeing as it is their platform, one of the major barriers to accessing financing through the banking system is of course the credit score. By diminishing the importance put on credit score and devloping an in house proprietary model I think this is great for accessibility as most people were taking on loans to consolidate debt. My biggest concern however is with how high APRs are through this platform, however if they are taking on lower interest rate loans then they are currently paying on a fixed payment schedule as opposed to revolving this is of course a win. Hopefully they are not just clearing up available space on the their cards to then spend again.

### Did you observe any interesting relationships between the other features (not the main feature(s) of interest)?

When I initially charted APR by Quarters I thought this a waste of time, the chart was all over the place and didn't give me any important information. However once I grouped the quarters into years there were some key trends that started to appear.
APR was decreasing over time which is great for borrowers, due to the negative correlation with Credit Score and Prosper Score my initial assumption was that we must be getting higher quality borrowers coming into the market. However it was the exact opposite, Credit Score and Prosper Score were both decreasing over time. This leads me to believe that APR must be a lagging indicator.


## Multivariate Exploration


#### BorrowerAPR vs ProsperScore vs Credit Score<br>
Here we can see that the best APRs (Below 0.1) are mostly borrowers with a Prosperscore above 10. There are also very few loans in that range for individuals who have credit ratings below 700. We'll add in Year for our individual plots and see how this changes our plots.

#### BorrowerAPR vs Credit Score vs Year<br>
Our Creditscore plot seems quite consistent with what we would expect, the best credit scores on the bottom and our rates increase we see lower scores. Something that is interesting is that in 2007-2008 we see some yellow colored plots which indicate lower credit scores. However after 2009 those yellow dots completely disappear. We also see much less points that have high credit scores. So less extreme borrowers. We start to see more "average" borrowers.

#### BorrowerAPR vs ProsperScore vs Year<br>
Our ProsperScore plot however tells a different story. In the first few years a high prosper score was less indicative of whether you would get a preferred rate. But in the last few years the distribution is much more gradual and follows a similar trend to our credit score plot. On the other hand we start to see a lot more borrowers with lower prosper scores in the last few years. This could be either the result of investors developing more and more confidence in the Prosperscore rating or that Prosper has changed their proprietary model that develops their score.


#### Talk about some of the relationships you observed in this part of the investigation. Were there features that strengthened each other in terms of looking at your feature(s) of interest?

Plotting Credit Score and Prosper Score with APR made a lot of sense as these values demonstrated the highest level of correlation with BorrowerAPR and with each other. It really demonstrated that although Credit Score definitely played a significant factor there were certain individuals with a "Good" Credit Score (700 range) that had exxecellent Prosper Scores (10+). This allows them access to preferred (lower) interest rates. Why is this significant you may ask? 56% of our population of borrowers (possibly more 17,000 loans have NA or Other listed for reason) have listed debt consolidation as their reason for borrowing. Credit Scores are a known barrier to the financially underserved, those who opted to never get a credit card will not have a credit score, also if you had missed payments on your cell phone bill in your late teenage years because no one had explained to you the importance of a credit score those derogatory items remain on your credit bureau for 7 years. Reducing your access to those lower interest rates, banks won't lend you money if you have a low credit score but they have no problem giving you a credit card with an APR over 20.

### Were there any interesting or surprising interactions between features?

When I added in time, some interesting trends started to emerge. On the Credit Score plot we saw that as time passed the population of borrowers with very low credit scores decreased, however so did the population of those with high credit scores. In 2008-2009 when the world was hit hard with the financial crisis Prosper was no exception, we saw new loans fall off a cliff in 2008Q4 and 2009Q1. No doubt Prosper had to rethink their business model and restore confidence in their investors. I searched online and found that today Prosper requires a minimum credit score of 640.

The Prosper Score vs Borrower APR over Time was of course a different story, like Credit Score we would expect our plot to gradually move from dark to light. As risk increases so should your rate of interest. In the first few years this wasn't the case. We saw dark points all over the range and very few light points. Prosper was relatively new and investors were spooked from the financial crisis and were opting to only choose loans with higher Prosper scores. As time passed though we have started to see out plot much more normally distributed and an appetite for higher risk loans reemerge. 





## Key Insights for Presentation

### APR
Before we introduce other variables I believe it's important to look at APR an isolation to understand what might be considered normal. APR is almost normally distributed, however it does have a slight right skew. With a large amount of loans in the 0.35 - 0.375 range. Our average borrower on Prosper is paying 21.96%


### Borrower APR by Category
If we think of APR as a proxy to sentiment of inherent risk as viewed by our investors, our box plot demonstrates personal loans to be the lest risky based on median 17.6%, Cosmetic Procedure seems to be the one that carries the highest risk with a median of 27.2%


## Risk Models Over Time

Credit Score and Prosper Score have the strongest negative correlation of all variables -49.9% for the former and -66.8% for the latter. Said another way as your score of either proprietary model increases as the expectancy that your APR will drop increases. Here are some key insights:

### Credit Score Impact on APR Over Time

- Best rates (below 10%) are reserved for the best Credit scores (800+)
- Post 2008 Prosper increased their credit score requirement, the yellow dots have disappeared
- 2011 onwards max APR has dropped from above 40% to slightly above 36%
- 2011 onwards number of borrowers with 800+ credit rating is trending downwards

### Prosper Score Impact on APR Over Time

- Best rates (below 10%) are reserved for the best Prosper Scores (10+)
- Appetite for risk has increased over time
- 2013 - 2014 Prosper Score follows a gradual transition from purple to yellow, investors seemed to have really adopted this risk rating
- 2011 onwards max APR has dropped from above 40% to slightly above 36%