Code

My code can be found&nbsp;here





Summary of Most Interesting Discoveries in the Bank Dataset:

The exploratory data analysis (EDA) of the bank dataset revealed several aspects about the attributes and their distributions.&nbsp; The data dictionary that accompanied the data was essential in or two situations to correctly interpret values.

Numeric attributes such as 'balance,' 'campaign,' 'duration,' and 'previous' displayed a notable skewness and significant numbers of outliers are visible on the box plot. This suggests that these variables could distort predictive modelling if left untreated. Specifically, 'balance' and 'campaign' featured extreme outlier values.

The 'duration' attribute notably contained information about the length of calls, but since this data is unavailable at prediction time, it should be excluded from predictive modeling to avoid data leakage.

‘pdays ' has a specific situation (taken from the data dictionary) where a value of ‘-1' denotes clients not previously contacted. So despite not technically having any missing values, this encoding indicates a significant portion of clients who had not been contacted, requiring maybe the need to create a binary indicator (previously contacted: True/False) to improve interpretability and modelling performance.

Among categorical attributes, 'poutcome' and 'contact' contained considerable missing data (23% and 10%, respectively). This level of missing data might call for dropping the column or maybe just the creation of an 'unknown' category rather than imputation or exclusion, preserving what information it does provide.

The 'default' attribute had extremely low variability, mainly populated with 'no' responses, which makes me think of it as a candidate for removal.

The target variable, 'subscribed,' is nearly evenly balanced, which is good for classification tasks.

One more thing to note is the ‘day attribute.&nbsp; The documentation has it classed as the day-of-week, but the analysis shows it is almost certainly a day-of-month value (values spread from 1-31).&nbsp; Additionally this attribute might better be classed as categorical rather than numeric since the numerical representation is still just a label rather than something measurable on a scale.

&nbsp;

Description of Data Pre-processing Approach:

Missing values : Minor gaps, such as 'age,' will be handled by median imputation

For categorical attributes like 'poutcome,' 'contact,' 'education,' and 'job,' I plan to add an ‘unknown’ category, despite the size of the missing data in poutcome, I think this should still work.

Categorical attributes will be encoded using appropriate methods: one-hot encoding for attributes with multiple non-ordinal categories and binary encoding for simpler, two-category variables (e.g., 'loan,' 'default').

I will look at scaling or log-transformations for a number of the numeric columns that exhibit skewness, some experimentation will be required here.

I will also look at managing outliers by capping in extreme cases, maybe transforming to compress the scale to minimise the impact of the outlier.&nbsp; More analysis needs to be done on options.

I will take a close look at attributes that all fall almost into one category.&nbsp; They may be in line for being dropped, but I will look at how they interact with other attributes before making this call.

&nbsp;

Description of Features Created or Intended to Create:

As mentioned earlier, to address the -1 value in pdays I will likely create a binary flag to indicate if they have been contacted or not.&nbsp;

I will perform the standard task of transforming categorical attributes to numeric form.

As demonstrated in the notebook, I have looked at combining the day and month attributes to give me a the date the customer was last contacted on.&nbsp; I then tried to turn this into the day of week.&nbsp; While we haven’t been given the year as far as I can tell, it won’t be possible to say definitively that the date in question is a Monday or a Thursday, we should however by substituting an arbitrary year, be able to group dates by their respective days of the week, even if we don’t know what day that is.&nbsp; This may be a flawed analysis an although initial results seem to show a strong correlation between subscription rates and one or two of the days, more work needs to be done.

I will also take a closer look at the various attributes around the campaign contact.&nbsp; There are signs that these impact the target variable, but imbalances, missing data may complicate things.&nbsp; It will be interesting to see how I might combine these attributes into a consolidated variable and see how it tracks with the target variable.

&nbsp;