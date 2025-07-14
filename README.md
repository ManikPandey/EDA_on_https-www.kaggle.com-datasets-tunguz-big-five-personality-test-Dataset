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

