# Exploratory Data Analysis for Machine

# Learning

#### Project Overview

**Dataset Summary: Big Five Personality Traits**

**Overview:**

**Code link in github:-** https://github.com/ManikPandey/EDA_on_https-www.kaggle.com-datasets-
tunguz-big-five-personality-test-Dataset

This dataset is taken from Kaggle (link:- https://www.kaggle.com/datasets/tunguz/big-five-
personality-test).

**Big five personality test dataset.** This dataset contains over **1 million responses** (specifically,
1,015,342 entries) collected online between 2016 and 2018 via an interactive personality test. The
test is based on the

**Big Five personality traits** (also known as OCEAN or the five-factor model), which groups personality
into five broad dimensions:

1.Openness,

2.Conscientiousness,

3. Extraversion,

4.Agreeableness, and

5.Neuroticism.

**Key Variables**

- **Personality Trait Responses:**
    - 50 items (e.g., EXT1, AGR1, CSN1, EST1, OPN1) rated on a 1–5 scale.
    - Each set of 10 questions measures one of the five traits.
- **Timing Data:**
    - For each question, the time taken to respond (in milliseconds, variables ending
       in _E).
    - testelapse: Total time (in seconds) spent on the survey page.
- **User Metadata:**
    - dateload: Timestamp when the survey was started.
    - screenw, screenh: User's screen width and height.
    - introelapse, endelapse: Time spent on the intro and finalization pages.


- IPC: Number of records from the user's IP address (used to filter for unique
    responses).
- country: User's country (determined technically, not self-reported).
- lat_appx_lots_of_err, long_appx_lots_of_err: Approximate latitude and longitude
    (with limited accuracy).

**Dataset Size**

- **Total records:** 1,015,
- **Variables per record:**
    - 50 personality trait responses
    - 50 response times
    - 8+ metadata fields

**Possible Target Variables**

Depending on the project focus, potential target variables include:

- **Trait Scores:** Calculated scores for each of the Big Five traits (from the 50 responses)
- **Correlation between traits:** We can check for correlation between different traits.
- **Test Completion Time:** testelapse—useful for behavioral analysis.
- **Country or Region:** For demographic or cross-cultural studies.
- **Response Patterns:** Such as consistency or speed (e.g., unusually fast completions).

**What Makes This Dataset Valuable**

- **Large, diverse sample** : Over a million responses from around the world.
- **Rich behavioral data** : Includes both answers and response times.
- **Demographic context** : Country and technical metadata allow for subgroup analysis.

This dataset is well-suited for exploring relationships between personality traits, response behavior,
and demographic factors.

**1. Dataset Summary**

The dataset contains responses to the Big Five personality test, collected through an online survey.
Each row represents one participant’s answers to 50 personality items and associated metadata. The
dataset is large, with over 1 million entries and 110 columns.

**Sample of the First 5 Records**

```
EXT1 EXT2 EXT3 EXT4 EXT5 ... dateload screenw screenh introelapse testelapse
```
###### 4.0 1.0 5.0 2.0 5.0 ... 2016 - 03 - 03 02:01:01 768.0 1024.0 9.0 234.


```
EXT1 EXT2 EXT3 EXT4 EXT5 ... dateload screenw screenh introelapse testelapse
```
###### 3.0 5.0 3.0 4.0 3.0 ... 2016 - 03 - 03 02:01:20 1360.0 768.0 12.0 179.

###### 2.0 3.0 4.0 4.0 3.0 ... 2016 - 03 - 03 02:01:56 1366.0 768.0 3.0 186.

###### 2.0 2.0 2.0 3.0 4.0 ... 2016 - 03 - 03 02:02:02 1920.0 1200.0 186.0 219.

###### 3.0 3.0 3.0 3.0 5.0 ... 2016 - 03 - 03 02:02:57 1366.0 768.0 8.0 315.


**Handling Missing Values**

- **Row deletion:** Removing all rows with any null values reduced the dataset from 1,015,340 to
    695,703 records. This approach ensures data completeness but results in data loss.
- **Forward fill:** Alternatively, missing values were filled using the last observed non-null value
    (fillna(method='ffill')). This can introduce bias or inaccuracies but preserves more data.

**Reverse Scoring**

Some items are negatively worded and require reverse scoring for accurate trait computation. The
following items were reverse-scored:

- **Extraversion:** EXT2, EXT4, EXT6, EXT8, EXT
- **Emotional Stability:** EST2, EST
- **Agreeableness:** AGR1, AGR3, AGR5, AGR
- **Conscientiousness:** CSN2, CSN4, CSN6, CSN
- **Openness:** OPN2, OPN4, OPN

_Reverse-scoring formula:_
new_value = 6 - original_value

**Dropping Less Useful Columns**

Columns like screenh, screenw, lat_appx_lots_of_err, and long_appx_lots_of_err were dropped to
focus on core survey and personality data.

**Aggregating Big Five Traits**

For each participant, the average score for each Big Five trait was computed:

- **EXT_score:** Mean of EXT1–EXT
- **EST_score:** Mean of EST1–EST
- **AGR_score:** Mean of AGR1–AGR
- **CSN_score:** Mean of CSN1–CSN
- **OPN_score:** Mean of OPN1–OPN

**Encoding Categorical Variables**

- **Country:** Encoded as country_code for easier analysis and modeling.

**Date and Time Formatting**

- **dateload:** Converted to datetime for time-based analysis, then reduced to only the time
    component for clarity.

#### Checking Skewness of BIG Five traits
#### Searching for outliers



Visualizing With and Without Outliers

After removing the data, we can still see there are some outlier on the right side of the graph, So lets
do the same thing by capping the data to 98percentile

### Transformation:

Transformation of Testelapse_capped98 data

Log Transformation

testelapse_capped98_log: skewness = 3.

##### Trying Box-Cox Transformation

Skewness after Box-Cox: -0.
Lambda used: -0.

visualizing histogram with and wihtout outliers in Testelapse data

Original data vs capped 98 vs Box cox transformed data


### Visualizing Big Five Traits and Testelapse (Box-Cox Transformed)

1. Histograms for Big Five Traits and Testelapse_Boxcox

### Hypotheses Testing

1. Personality Traits and Test Completion Time

There is a significant association between Conscientiousness (CSN_score) and the time taken to
complete the test (testelapse_log or testelapse_capped98_log). Rationale: More conscientious
individuals may complete the survey more efficiently, resulting in shorter completion times

**H0:** There is no any significant association between Conscientiousness (CSN_score) and the time
taken to complete the test (testelapse or testelapse_boxcox)

**H1:** There is a significant association between Conscientiousness (CSN_score) and the time taken to
complete the test (testelapse or testelapse_boxcox).

_Rationale:_ More conscientious individuals may complete the survey more efficiently, resulting in
shorter completion times

2. Inter-Trait Relationships
H: Extraversion (EXT_score) and Openness (OPN_score) are positively correlated. Rationale: People
who are outgoing may also be more open to new experiences.

**H0:** Extraversion (EXT_score) and Openness (OPN_score) are not positively correlated.

**H1:** Extraversion (EXT_score) and Openness (OPN_score) are positively correlated.

_Rationale:_ People who are outgoing may also be more open to new experiences.

3. Group Differences

Participants with high Agreeableness (AGR_score) tend to have lower test completion times
compared to those with low Agreeableness. Rationale: Agreeable individuals may be more
cooperative and focused during surveys.

**H0:** There is a no realtion between test completion time and Agreeableness. Participants with high
Agreeableness (AGR_score) don't have any signigicant affect on completion times compared to those
with low Agreeableness.

**H1:** Participants with high Agreeableness (AGR_score) tend to have lower test completion times
compared to those with low Agreeableness. i.e there is a realtion betwen test completion time and
Agreeableness

_Relation:_ Agreeable individuals may be more cooperative and focused during surveys.

## Summary

**Big Five Personality Traits Dataset: EDA Summary & Analysis**

**1. Data Summary**
**Dataset Overview:**
**2. Data Exploration Plan**
**Vision for Analysis:**
- **Understand trait distributions:** Assess the overall and country-wise distributions of Big Five
    scores.
- **Behavioral patterns:** Analyze response times and completion behaviors.
- **Demographic insights:** Explore how traits and behaviors vary across countries.
- **Trait interrelations:** Investigate correlations between personality traits.
- **Outlier and anomaly detection:** Identify and address extreme values in responses and
    timings.
**Steps:**
1. Generate descriptive statistics for all variables.
2. Visualize trait distributions and relationships (histograms, scatter plots, pair plots).
3. Examine response time data for skewness and outliers.
4. Explore demographic patterns using country-level aggregations.
5. Formulate and test hypotheses about trait relationships and behavioral outcomes.
**3. Exploratory Data Analysis (EDA) Results**
   
**Trait Distributions:**
- Most trait scores (Extraversion, Emotional Stability, Conscientiousness) are nearly normally
    distributed.
- Agreeableness and Openness show slight negative skewness.

**Outlier Detection & Response Time:**
- Extreme outliers in testelapse (max: 11,892,718 sec) suggest data entry or behavioral
    anomalies.
- Capping at the 98th/99th percentile and applying Box-Cox transformation normalizes timing
    data.
**4. Data Cleaning & Feature Engineering**
**Missing Values:**

- Personality items: 1,783 missing per column.
- Country: 77 missing.
- Approach: Rows with any nulls removed (reduced to 695,703 records), or forward-fill used as
    alternative.

**Reverse Scoring:**

- Negatively worded items reverse-scored for accurate trait computation (e.g., EXT2, EST2,
    AGR1, etc.).
- Formula: new_value = 6 - original_value.

**Feature Aggregation:**

- Trait scores computed as the mean of their 10 respective items (e.g., EXT_score =
    mean(EXT1–EXT10)).

**Encoding & Formatting:**

- Country encoded as country_code.
- Timestamps converted to datetime, then reduced to time component.

**Visualization Outputs:**

- **Histograms:** For each trait and test completion time.
  
- **Boxplots:** For outlier detection in timing data.
- **Pair plots:** For trait interrelationships and country differences.
**5. Key Findings & Insights**
- **Trait Distributions:** Most traits are nearly normal; Agreeableness and Openness slightly
skewed.
- **Outliers:** Test completion time contains extreme outliers; capping and transformation are
necessary.
- **Trait Relationships:** Extraversion and Openness are positively correlated (Pearson r = 0.149, p
< 0.001).
- **Behavioral Patterns:** No meaningful relationship between Conscientiousness or
Agreeableness and test completion time, despite statistical significance due to large sample
size.


- **Country Differences:** Visualizations show country-level variation in trait averages.
**6. Hypotheses**
1. **Conscientiousness and Completion Time:** Higher Conscientiousness (CSN_score) is
associated with shorter test completion times.
2. **Extraversion and Openness:** Extraversion (EXT_score) and Openness (OPN_score) are
positively correlated.
3. **Agreeableness and Completion Time:** High Agreeableness (AGR_score) leads to faster test
completion.
**7. Significance Test Discussion**

**Hypothesis Tested:**
_Conscientiousness is associated with shorter test completion time._

- **Null Hypothesis (H0):** No significant association between CSN_score and test completion
    time.
- **Alternative (H1):** Higher CSN_score correlates with shorter completion time.

**Results:**

- Correlation (log-transformed): 0.025, p-value < 0.001
- Correlation (Box-Cox transformed): 0.034, p-value < 0.001

**Interpretation:**

- The correlation is statistically significant but extremely small, indicating no practical
    relationship.
- The null hypothesis is accepted: Conscientiousness does not meaningfully predict test
    completion speed.
**8. Conclusion & Next Steps**

**Key Takeaways:**

- The dataset is robust, diverse, and suitable for advanced behavioral and demographic
    analyses.
- Trait distributions are mostly normal; outliers in timing data must be addressed for modeling.
- Some trait relationships exist (e.g., Extraversion–Openness), but behavioral predictions (e.g.,
    completion speed) are weak.

**Next Steps:**

- Further investigate demographic and cultural influences on trait distributions.
- Apply advanced modeling (e.g., clustering, predictive analytics) to uncover deeper insights.
- Explore response patterns (e.g., consistency, speed) for potential quality control or
    behavioral research.

