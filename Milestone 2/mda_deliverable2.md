Mini Data-Analysis Deliverable 1
================

*To complete this milestone, you can either edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to the rest of your mini data analysis project!

In Milestone 1, you explored your data. and came up with research
questions. This time, we will finish up our mini data analysis and
obtain results for your data by:

- Making summary tables and graphs
- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

We will also explore more in depth the concept of *tidy data.*

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 50 points: 45 for your analysis, and
5 for overall reproducibility, cleanliness, and coherence of the Github
submission.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

- Understand what *tidy* data is, and how to create it using `tidyr`.
- Generate a reproducible and clear report using R Markdown.
- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

    library(datateachr) # <- might contain the data you picked!
    library(tidyverse)

# Task 1: Process and summarize your data

From milestone 1, you should have an idea of the basic structure of your
dataset (e.g. number of rows and columns, class types, etc.). Here, we
will start investigating your data more in-depth using various data
manipulation functions.

### 1.1 (1 point)

First, write out the 4 research questions you defined in milestone 1
were. This will guide your work through milestone 2:

<!-------------------------- Start your work below ---------------------------->

1.  Has there been a significant change in maximum flow rates over time?
    How does the beginning of the data set compare to the last decade of
    the dataset?

2.  How do missing values in variables like ‘sym’ or other quality
    indicators impact the analysis and interpretation of flow rate data?

3.  in exercise 1, my graph, “Frequency of Flow Rates for Maximum
    Extreme Type”, had an outlier on the higher end. What does that
    outlier indicate?

4.  What about looking at the minimum extreme type? How does that
    compare to the filtered maximum extreme type data set?
    <!----------------------------------------------------------------------------->

Here, we will investigate your data using various data manipulation and
graphing functions.

### 1.2 (8 points)

Now, for each of your four research questions, choose one task from
options 1-4 (summarizing), and one other task from 4-8 (graphing). You
should have 2 tasks done for each research question (8 total). Make sure
it makes sense to do them! (e.g. don’t use a numerical variables for a
task that needs a categorical variable.). Comment on why each task helps
(or doesn’t!) answer the corresponding research question.

Ensure that the output of each operation is printed!

Also make sure that you’re using dplyr and ggplot2 rather than base R.
Outside of this project, you may find that you prefer using base R
functions for certain tasks, and that’s just fine! But part of this
project is for you to practice the tools we learned in class, which is
dplyr and ggplot2.

**Summarizing:**

1.  Compute the *range*, *mean*, and *two other summary statistics* of
    **one numerical variable** across the groups of **one categorical
    variable** from your data.
2.  Compute the number of observations for at least one of your
    categorical variables. Do not use the function `table()`!
3.  Create a categorical variable with 3 or more groups from an existing
    numerical variable. You can use this new variable in the other
    tasks! *An example: age in years into “child, teen, adult, senior”.*
4.  Compute the proportion and counts in each category of one
    categorical variable across the groups of another categorical
    variable from your data. Do not use the function `table()`!

**Graphing:**

1.  Create a graph of your choosing, make one of the axes logarithmic,
    and format the axes labels so that they are “pretty” or easier to
    read.
2.  Make a graph where it makes sense to customize the alpha
    transparency.

Using variables and/or tables you made in one of the “Summarizing”
tasks:

1.  Create a graph that has at least two geom layers.
2.  Create 3 histograms, with each histogram having different sized
    bins. Pick the “best” one and explain why it is the best.

Make sure it’s clear what research question you are doing each operation
for!

<!------------------------- Start your work below ----------------------------->

**Research Question 1: Change in Maximum Flow Rates Over Time**

    # Summarizing
    summary_stats <- flow_sample %>%
      group_by(year) %>%
      summarise(
        Range = max(flow) - min(flow),
        Mean = mean(flow),
        Median = median(flow),
        SD = sd(flow)
      )
    # This task will provide a general sense of how the flow rate has changed over time.

    # Graphing
    flow_trend_plot <- flow_sample %>%
      ggplot(aes(x = year, y = flow)) +
      geom_line() +
      geom_smooth(method = "lm") +
      labs(title = "Trend of Flow Rate Over Time")
    # This visualization will help in understanding the trend of flow rate across the years.

    flow_trend_plot

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 2 rows containing non-finite values (`stat_smooth()`).

![](mda_deliverable2_files/figure-markdown_strict/unnamed-chunk-2-1.png)

**Research Question 2: Impact of Missing Values on Analysis**

    # Summarizing
    sym_counts <- flow_sample %>%
      count(sym, name = "Number_of_Observations")
    # This task will help in understanding the extent of missing or different values in 'sym' variable.

    # Graphing
    sym_flow_plot <- flow_sample %>%
      ggplot(aes(x = sym, y = flow)) +
      geom_boxplot() +
      scale_y_log10() +
      labs(title = "Distribution of Flow Rates by 'sym' Levels")
    # This graph will help in analyzing the distribution of flow rates across different levels of the 'sym' variable.

    sym_flow_plot

    ## Warning: Removed 2 rows containing non-finite values (`stat_boxplot()`).

![](mda_deliverable2_files/figure-markdown_strict/unnamed-chunk-3-1.png)

**Research Question 3: Investigation of Outlier in Frequency of Flow
Rates**

    # Summarizing
    flow_summary <- flow_sample %>%
      summarise(
        Mean = mean(flow),
        SD = sd(flow)
      )
    # This task will help in understanding the central tendency and dispersion of flow rates which is essential to identify outliers.

    # Graphing
    hist_plot <- flow_sample %>%
      ggplot(aes(x = flow)) +
      geom_histogram(binwidth = 5) +
      labs(title = "Histogram of Flow Rates")
    # This task will help in visualizing the distribution of flow rates and identifying any outliers.

    hist_plot

    ## Warning: Removed 2 rows containing non-finite values (`stat_bin()`).

![](mda_deliverable2_files/figure-markdown_strict/unnamed-chunk-4-1.png)

**Research Question 4: Comparison Between Minimum and Maximum Extreme
Types**

    # Summarizing
    extreme_counts <- flow_sample %>%
      group_by(extreme_type) %>%
      summarise(
        Count = n(),
        Proportion = n() / nrow(flow_sample)
      )
    # This task will help in understanding the distribution of different extreme types in the dataset.

    # Graphing
    extreme_comparison_plot <- flow_sample %>%
      ggplot(aes(x = flow, fill = extreme_type)) +
      geom_density(alpha = 0.5) +
      labs(title = "Comparison of Flow Rates between Extreme Types")
    # This task will help in visually comparing the distribution of flow rates between the minimum and maximum extreme types.

    extreme_comparison_plot

    ## Warning: Removed 2 rows containing non-finite values (`stat_density()`).

![](mda_deliverable2_files/figure-markdown_strict/unnamed-chunk-5-1.png)

<!----------------------------------------------------------------------------->

### 1.3 (2 points)

Based on the operations that you’ve completed, how much closer are you
to answering your research questions? Think about what aspects of your
research questions remain unclear. Can your research questions be
refined, now that you’ve investigated your data a bit more? Which
research questions are yielding interesting results?

<!------------------------- Write your answer here ---------------------------->

Graph 1: **Trend of Flow Rate Over Time**

- The flow rate over the years appear to look highly variable. The
  general trend, indicated by the blue line, shows a slight decrease
  over the period shown.
- There are extreme fluctuations, which could be because of inconsistent
  data collection methods, measurement errors, or genuine variation in
  flow rates (which could be interesting).
- Refining the research question: Can we segment the data further, maybe
  by region or source, to better understand trends

Graph 2: **Distribution of Flow Rates by ‘sym’ Levels**

- There appears to be differences in flow rate distribution among the
  ‘sym’ levels. ‘sym’ level E has a higher median flow rate and exhibits
  a wider interquartile range compared to other levels.
- Levels A and B have significantly lower values, with B having some
  outliers.
- Refining the research question: Would be worth looking into what kind
  of factors are behind the difference between Sym A and E

Graph 3: **Histogram of Flow Rates**

- The majority of the data points are clustered in the very low flow
  range, basically near 0. There’s a minor spread between 100-400, but
  these counts are significantly lower than the major peak.
- This suggests that most instances have a low flow rate with some
  exceptions.
- Could be interesting to look more at these outliers though
- Refining the research question: what kind of factors lead to the
  overwhelming number of flow rates near zero?

Graph 4: **Comparison of Flow Rates between Extreme Types**

- With two peaks, one at low flow rates and another at around 200, it
  suggests that there are two primary behaviors or events that lead to
  these peaks in the maximum extreme type
- Refining the research question: Because of the peak at the 200 flow
  mark for the maximum extreme type, are there specific conditions,
  events, or anomalies during those periods?
  <!----------------------------------------------------------------------------->

# Task 2: Tidy your data

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

- Each row is an **observation**
- Each column is a **variable**
- Each cell is a **value**

### 2.1 (2 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have \>8 variables, just
pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

**2.1**

    ## Rows: 218
    ## Columns: 7
    ## $ station_id   <chr> "05BB001", "05BB001", "05BB001", "05BB001", "05BB001", "0…
    ## $ year         <dbl> 1909, 1910, 1911, 1912, 1913, 1914, 1915, 1916, 1917, 191…
    ## $ extreme_type <chr> "maximum", "maximum", "maximum", "maximum", "maximum", "m…
    ## $ month        <dbl> 7, 6, 6, 8, 6, 6, 6, 6, 6, 6, 6, 7, 6, 6, 6, 7, 5, 7, 6, …
    ## $ day          <dbl> 7, 12, 14, 25, 11, 18, 27, 20, 17, 15, 22, 3, 9, 5, 14, 5…
    ## $ flow         <dbl> 314, 230, 264, 174, 232, 214, 236, 309, 174, 345, 185, 24…
    ## $ sym          <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…

1.  station_id: Each value represents the identifier of a station - this
    is tidy.
2.  year: Each value represents the year of observation - this is tidy.
3.  extreme_type: Each value represents the type of extreme - this is
    tidy.
4.  month: Each value represents the month of observation - this is
    tidy.
5.  day: Each value represents the day of observation - this is tidy.
6.  flow: Each value represents the flow rate - this is tidy.
7.  sym: Each value represents some quality indicator - this is tidy.

<!----------------------------------------------------------------------------->

### 2.2 (4 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

**2.2**

    # Untidying the data by merging year, month, and day into a single column
    flow_sample_untidy <- flow_sample %>%
      unite("date", year:day, sep = "-")

    # Displaying the untidy data
    head(flow_sample_untidy)

    ## # A tibble: 6 × 4
    ##   station_id date               flow sym  
    ##   <chr>      <chr>             <dbl> <chr>
    ## 1 05BB001    1909-maximum-7-7    314 <NA> 
    ## 2 05BB001    1910-maximum-6-12   230 <NA> 
    ## 3 05BB001    1911-maximum-6-14   264 <NA> 
    ## 4 05BB001    1912-maximum-8-25   174 <NA> 
    ## 5 05BB001    1913-maximum-6-11   232 <NA> 
    ## 6 05BB001    1914-maximum-6-18   214 <NA>

    # Tidying the data back by separating the date column into year, month, and day
    flow_sample_tidy <- flow_sample_untidy %>%
      separate(date, into = c("year", "month", "day"), sep = "-")

    ## Warning: Expected 3 pieces. Additional pieces discarded in 218 rows [1, 2, 3, 4, 5, 6,
    ## 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, ...].

    # Displaying the tidy data
    head(flow_sample_tidy)

    ## # A tibble: 6 × 6
    ##   station_id year  month   day    flow sym  
    ##   <chr>      <chr> <chr>   <chr> <dbl> <chr>
    ## 1 05BB001    1909  maximum 7       314 <NA> 
    ## 2 05BB001    1910  maximum 6       230 <NA> 
    ## 3 05BB001    1911  maximum 6       264 <NA> 
    ## 4 05BB001    1912  maximum 8       174 <NA> 
    ## 5 05BB001    1913  maximum 6       232 <NA> 
    ## 6 05BB001    1914  maximum 6       214 <NA>

<!----------------------------------------------------------------------------->

### 2.3 (4 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the remaining tasks:

<!-------------------------- Start your work below ---------------------------->

1.  Has there been a significant change in maximum flow rates over time?
    How does the beginning of the data set compare to the last decade of
    the dataset?

2.  How do missing values in variables like ‘sym’ or other quality
    indicators impact the analysis and interpretation of flow rate data?

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

Based on the interpretations of the results from 1.3, I decided to go
with my first 2 research questions because they had the most intersting
results. I wanted to delve further into the downward trend seen in the
max flow rate graph. I also wanted to see if there was anything else
that could explain the big differences in flow rate between Sym A and E.

<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

(If it makes more sense, then you can make/pick two versions of your
data, one for each research question.)

<!--------------------------- Start your work below --------------------------->

**Data prep for Research question 1**

    # Filtering data for maximum extreme type and arranging by year
    max_flow_data <- flow_sample %>%
      filter(extreme_type == "maximum") %>%
      arrange(year) %>%
      # Dropping the 'sym' column as it might not be relevant for this analysis
      select(-sym) %>%
      # Creating a new column to represent the decade
      mutate(decade = (year %/% 10) * 10)

**Data prep for Research question 2**

    # Creating a new variable to categorize the presence and absence of data in 'sym'
    flow_sample_with_sym_flag <- flow_sample %>%
      # Handling missing values by filtering out rows with NA in 'flow' column
      filter(!is.na(flow)) %>%
      mutate(sym_present = ifelse(is.na(sym), "No", "Yes")) %>%
      # Dropping the extreme_type, month, and day columns as they might not be relevant for this analysis
      select(-extreme_type, -month, -day) %>%
      # Arranging by 'sym_present' to have a tidy dataset
      arrange(sym_present) %>%
      # Creating a new column to categorize flow rate as High, Medium, or Low
      mutate(flow_category = case_when(
        flow > quantile(flow, 0.75, na.rm = TRUE) ~ "High",
        flow < quantile(flow, 0.25, na.rm = TRUE) ~ "Low",
        TRUE ~ "Medium"
      ))

<!----------------------------------------------------------------------------->

# Task 3: Modelling

## 3.0 (no points)

Pick a research question from 1.2, and pick a variable of interest
(we’ll call it “Y”) that’s relevant to the research question. Indicate
these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: Has there been a significant change in maximum
flow rates over time? How does the beginning of the data set compare to
the last decade of the dataset?

**Variable of interest**: Maximum flow rate (flow) over time (year)

<!----------------------------------------------------------------------------->

## 3.1 (3 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

- **Note**: It’s OK if you don’t know how these models/tests work. Here
  are some examples of things you can do here, but the sky’s the limit.

  - You could fit a model that makes predictions on Y using another
    variable, by using the `lm()` function.
  - You could test whether the mean of Y equals 0 using `t.test()`, or
    maybe the mean across two groups are different using `t.test()`, or
    maybe the mean across multiple groups are different using `anova()`
    (you may have to pivot your data for the latter two).
  - You could use `lm()` to test for significance of regression
    coefficients.

<!-------------------------- Start your work below ---------------------------->

**Linear Regression Analysis**

- In this model, the year acts as the independent variable (X), and the
  maximum flow rate will be the dependent variable (Y).

- In the output, the coefficient for year will show average change in
  maximum flow rate for each additional year. A p-value less than 0.05
  for the year variable would suggest that our hypothesis that the
  change in flow rate over time is statistically significant.

<!-- -->

    # Load necessary library
    library(dplyr)

    # Filter the data for maximum flow rates
    max_flow_data <- flow_sample %>%
      filter(extreme_type == "maximum")

    # Fit the linear regression model
    flow_model <- lm(flow ~ year, data = max_flow_data)
    # Print the summary of the model to the screen to view the results
    summary(flow_model)

    ## 
    ## Call:
    ## lm(formula = flow ~ year, data = max_flow_data)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -96.31 -43.85 -12.97  34.30 272.62 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept) 946.2019   363.3154   2.604   0.0105 *
    ## year         -0.3740     0.1851  -2.021   0.0458 *
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 60.82 on 107 degrees of freedom
    ## Multiple R-squared:  0.03677,    Adjusted R-squared:  0.02776 
    ## F-statistic: 4.084 on 1 and 107 DF,  p-value: 0.04579

<!----------------------------------------------------------------------------->

## 3.2 (3 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

- Be sure to indicate in writing what you chose to produce.
- Your code should either output a tibble (in which case you should
  indicate the column that contains the thing you’re looking for), or
  the thing you’re looking for itself.
- Obtain your results using the `broom` package if possible. If your
  model is not compatible with the broom function you’re needing, then
  you can obtain your results by some other means, but first indicate
  which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

**3.2**

I chose to produce regression coefficients and their associated p-values
from my fitted model.

Produced Values:

1.  Regression Coefficient for year: -0.3739812
2.  P-value for year coefficient: 0.04578777

- These produced values suggests that the maximum flow rate decreases by
  about 0.374 units (on average) each year.

- The p-value associated with this coefficient is approximately 0.046,
  (p\<0.05). This suggests that there is a statistical significance
  between the year and the maximum flow rate. Also, circling back to
  3.1, this p\<0.05 value supports the hypothesis that maximum flow rate
  has been changing over time.

<!-- -->

    # Load necessary library
    library(broom)

    # Use broom to tidy up the output
    tidy_output <- tidy(flow_model)

    # Print the tidy output to screen
    print(tidy_output)

    ## # A tibble: 2 × 5
    ##   term        estimate std.error statistic p.value
    ##   <chr>          <dbl>     <dbl>     <dbl>   <dbl>
    ## 1 (Intercept)  946.      363.         2.60  0.0105
    ## 2 year          -0.374     0.185     -2.02  0.0458

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

    # Load necessary package
    library(fs)

    # Create a new directory called 'output' in your current working directory
    dir_create("output")

    # Verify that the directory has been created
    dir_exists("output")

    ## output 
    ##   TRUE

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 4.1 (3 points)

Take a summary table that you made from Task 1, and write it as a csv
file in your `output` folder. Use the `here::here()` function.

- **Robustness criteria**: You should be able to move your Mini Project
  repository / project folder to some other location on your computer,
  or move this very Rmd file to another location within your project
  repository / folder, and your code should still work.
- **Reproducibility criteria**: You should be able to delete the csv
  file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

**4.1**

I took the summary table from research question 1; it looks at how flow
rate has changed generally over time.

    library(tidyverse)
    library(here)

    ## here() starts at /Users/jamesforward/Desktop/STAT 545/Git repos/mda_jf

    # Write the summary table to a csv file in the output directory
    write_csv(summary_stats, here("output", "summary_stats.csv"))

<!----------------------------------------------------------------------------->

## 4.2 (3 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

- The same robustness and reproducibility criteria as in 4.1 apply here.

<!-------------------------- Start your work below ---------------------------->

     # Write the model object to an R binary file
    saveRDS(flow_model, file = "output/flow_model.rds")

    # Load the model object from the R binary file
    loaded_flow_model <- readRDS(file = "output/flow_model.rds")

    # Optionally, to verify the loaded model is identical to the original model, 
    # you can compare the summary of both models
    summary(flow_model)

    ## 
    ## Call:
    ## lm(formula = flow ~ year, data = max_flow_data)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -96.31 -43.85 -12.97  34.30 272.62 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept) 946.2019   363.3154   2.604   0.0105 *
    ## year         -0.3740     0.1851  -2.021   0.0458 *
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 60.82 on 107 degrees of freedom
    ## Multiple R-squared:  0.03677,    Adjusted R-squared:  0.02776 
    ## F-statistic: 4.084 on 1 and 107 DF,  p-value: 0.04579

    summary(loaded_flow_model)

    ## 
    ## Call:
    ## lm(formula = flow ~ year, data = max_flow_data)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -96.31 -43.85 -12.97  34.30 272.62 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept) 946.2019   363.3154   2.604   0.0105 *
    ## year         -0.3740     0.1851  -2.021   0.0458 *
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 60.82 on 107 degrees of freedom
    ## Multiple R-squared:  0.03677,    Adjusted R-squared:  0.02776 
    ## F-statistic: 4.084 on 1 and 107 DF,  p-value: 0.04579

<!----------------------------------------------------------------------------->

# Overall Reproducibility/Cleanliness/Coherence Checklist

Here are the criteria we’re looking for.

## Coherence (0.5 points)

The document should read sensibly from top to bottom, with no major
continuity errors.

The README file should still satisfy the criteria from the last
milestone, i.e. it has been updated to match the changes to the
repository made in this milestone.

## File and folder structure (1 points)

You should have at least three folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (1 point)

All output is recent and relevant:

- All Rmd files have been `knit`ted to their output md files.
- All knitted md files are viewable without errors on Github. Examples
  of errors: Missing plots, “Sorry about that, but we can’t show files
  that are this big right now” messages, error messages from broken R
  code
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (Rmd) files have been updated.
- There should be no relic output files. For example, if you were
  knitting an Rmd to html, but then changed the output to be only a
  markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

## Tagged release (0.5 point)

You’ve tagged a release for Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
