Mini Data-Analysis Deliverable 1
================

# Welcome to your (maybe) first-ever data analysis project!

And hopefully the first of many. Let’s get started:

1.  Install the [`datateachr`](https://github.com/UBC-MDS/datateachr)
    package by typing the following into your **R terminal**:

<!-- -->

    install.packages("devtools")
    devtools::install_github("UBC-MDS/datateachr")

’2. Load the packages below.

``` r
library(datateachr)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

3.  Make a repository in the <https://github.com/stat545ubc-2023>
    Organization. You can do this by following the steps found on canvas
    in the entry called [MDA: Create a
    repository](https://canvas.ubc.ca/courses/126199/pages/mda-create-a-repository).
    One completed, your repository should automatically be listed as
    part of the stat545ubc-2023 Organization.

# Instructions

## For Both Milestones

- Each milestone has explicit tasks. Tasks that are more challenging
  will often be allocated more points.

- Each milestone will be also graded for reproducibility, cleanliness,
  and coherence of the overall Github submission.

- While the two milestones will be submitted as independent
  deliverables, the analysis itself is a continuum - think of it as two
  chapters to a story. Each chapter, or in this case, portion of your
  analysis, should be easily followed through by someone unfamiliar with
  the content.
  [Here](https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/)
  is a good resource for what constitutes “good code”. Learning good
  coding practices early in your career will save you hassle later on!

- The milestones will be equally weighted.

## For Milestone 1

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-1.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work below --->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to the mini-analysis GitHub repository you made
earlier, and tag a release on GitHub. Then, submit a link to your tagged
release on canvas.

**Points**: This milestone is worth 36 points: 30 for your analysis, and
6 for overall reproducibility, cleanliness, and coherence of the Github
submission.

# Learning Objectives

By the end of this milestone, you should:

- Become familiar with your dataset of choosing
- Select 4 questions that you would like to answer with your data
- Generate a reproducible and clear report using R Markdown
- Become familiar with manipulating and summarizing your data in tibbles
  using `dplyr`, with a research question in mind.

# Task 1: Choose your favorite dataset

The `datateachr` package by Hayley Boyce and Jordan Bourak currently
composed of 7 semi-tidy datasets for educational purposes. Here is a
brief description of each dataset:

- *apt_buildings*: Acquired courtesy of The City of Toronto’s Open Data
  Portal. It currently has 3455 rows and 37 columns.

- *building_permits*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 20680 rows and 14 columns.

- *cancer_sample*: Acquired courtesy of UCI Machine Learning Repository.
  It currently has 569 rows and 32 columns.

- *flow_sample*: Acquired courtesy of The Government of Canada’s
  Historical Hydrometric Database. It currently has 218 rows and 7
  columns.

- *parking_meters*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 10032 rows and 22 columns.

- *steam_games*: Acquired courtesy of Kaggle. It currently has 40833
  rows and 21 columns.

- *vancouver_trees*: Acquired courtesy of The City of Vancouver’s Open
  Data Portal. It currently has 146611 rows and 20 columns.

**Things to keep in mind**

- We hope that this project will serve as practice for carrying our your
  own *independent* data analysis. Remember to comment your code, be
  explicit about what you are doing, and write notes in this markdown
  document when you feel that context is required. As you advance in the
  project, prompts and hints to do this will be diminished - it’ll be up
  to you!

- Before choosing a dataset, you should always keep in mind **your
  goal**, or in other ways, *what you wish to achieve with this data*.
  This mini data-analysis project focuses on *data wrangling*,
  *tidying*, and *visualization*. In short, it’s a way for you to get
  your feet wet with exploring data on your own.

And that is exactly the first thing that you will do!

1.1 **(1 point)** Out of the 7 datasets available in the `datateachr`
package, choose **4** that appeal to you based on their description.
Write your choices below: **\<\<put them in “Start your work
below”\>\>**

**Note**: We encourage you to use the ones in the `datateachr` package,
but if you have a dataset that you’d really like to use, you can include
it here. But, please check with a member of the teaching team to see
whether the dataset is of appropriate complexity. Also, include a
**brief** description of the dataset here to help the teaching team
understand your data.

<!-------------------------- Start your work below ---------------------------->

1: cancer_sample

2: apt_buildings

3: flow_sample

4: steam_games

<!----------------------------------------------------------------------------->

1.2 **(6 points)** One way to narrowing down your selection is to
*explore* the datasets. Use your knowledge of dplyr to find out at least
*3* attributes about each of these datasets (an attribute is something
such as number of rows, variables, class type…). The goal here is to
have an idea of *what the data looks like*.

*Hint:* This is one of those times when you should think about the
cleanliness of your analysis. I added a single code chunk for you below,
but do you want to use more than one? Would you like to write more
comments outside of the code chunk?

<!-------------------------- Start your work below ---------------------------->

### Dataset 1: “steam_games”

    ## [1] "Number of rows: 40833"

    ## [1] "Number of variables: 21"

    ## [1] "Class type: spec_tbl_df" "Class type: tbl_df"     
    ## [3] "Class type: tbl"         "Class type: data.frame"

### Dataset 2: “cancer_sample”

    ## [1] "Number of rows: 569"

    ## [1] "Number of variables: 32"

    ## [1] "Class type: spec_tbl_df" "Class type: tbl_df"     
    ## [3] "Class type: tbl"         "Class type: data.frame"

### Dataset 3: “flow_sample”

    ## [1] "Number of rows: 218"

    ## [1] "Number of variables: 7"

    ## [1] "Class type: tbl_df"     "Class type: tbl"        "Class type: data.frame"

### Dataset 4: “apt_buildings”

    ## [1] "Number of rows: 3455"

    ## [1] "Number of variables: 37"

    ## [1] "Class type: tbl_df"     "Class type: tbl"        "Class type: data.frame"

<!----------------------------------------------------------------------------->

1.3 **(1 point)** Now that you’ve explored the 4 datasets that you were
initially most interested in, let’s narrow it down to 1. What lead you
to choose this one? Briefly explain your choice below.

<!-------------------------- Start your work below ---------------------------->

I choose the dataset, “flow_sample”! It looks interesting and water is
necessary for both our survial as humans but our environment also
requires water to be sustained. It would be interesting to see if these
flow rates can be analyzed for trends that can be used to develop
platforms on environmental impact and sustainable water usage. With
variables ranging from the flow rate to the type of extremes and
timestamps, there is potential for complex analysis to be done.
<!----------------------------------------------------------------------------->

1.4 **(2 points)** Time for a final decision! Going back to the
beginning, it’s important to have an *end goal* in mind. For example, if
I had chosen the `titanic` dataset for my project, I might’ve wanted to
explore the relationship between survival and other variables. Try to
think of 1 research question that you would want to answer with your
dataset. Note it down below.

<!-------------------------- Start your work below ---------------------------->

What is the relationship between the `month` and `flow` in the dataset;
am I able to use this data to see variation between seasons?
<!----------------------------------------------------------------------------->

# Important note

Read Tasks 2 and 3 *fully* before starting to complete either of them.
Probably also a good point to grab a coffee to get ready for the fun
part!

This project is semi-guided, but meant to be *independent*. For this
reason, you will complete tasks 2 and 3 below (under the **START HERE**
mark) as if you were writing your own exploratory data analysis report,
and this guidance never existed! Feel free to add a brief introduction
section to your project, format the document with markdown syntax as you
deem appropriate, and structure the analysis as you deem appropriate. If
you feel lost, you can find a sample data analysis
[here](https://www.kaggle.com/headsortails/tidy-titarnic) to have a
better idea. However, bear in mind that it is **just an example** and
you will not be required to have that level of complexity in your
project.

# Task 2: Exploring your dataset

If we rewind and go back to the learning objectives, you’ll see that by
the end of this deliverable, you should have formulated *4* research
questions about your data that you may want to answer during your
project. However, it may be handy to do some more exploration on your
dataset of choice before creating these questions - by looking at the
data, you may get more ideas. **Before you start this task, read all
instructions carefully until you reach START HERE under Task 3**.

2.1 **(12 points)** Complete *4 out of the following 8 exercises* to
dive deeper into your data. All datasets are different and therefore,
not all of these tasks may make sense for your data - which is why you
should only answer *4*.

Make sure that you’re using dplyr and ggplot2 rather than base R for
this task. Outside of this project, you may find that you prefer using
base R functions for certain tasks, and that’s just fine! But part of
this project is for you to practice the tools we learned in class, which
is dplyr and ggplot2.

1.  Plot the distribution of a numeric variable.
2.  Create a new variable based on other variables in your data (only if
    it makes sense)
3.  Investigate how many missing values there are per variable. Can you
    find a way to plot this?
4.  Explore the relationship between 2 variables in a plot.
5.  Filter observations in your data according to your own criteria.
    Think of what you’d like to explore - again, if this was the
    `titanic` dataset, I may want to narrow my search down to passengers
    born in a particular year…
6.  Use a boxplot to look at the frequency of different observations
    within a single variable. You can do this for more than one variable
    if you wish!
7.  Make a new tibble with a subset of your data, with variables and
    observations that you are interested in exploring.
8.  Use a density plot to explore any of your variables (that are
    suitable for this type of plot).

2.2 **(4 points)** For each of the 4 exercises that you complete,
provide a *brief explanation* of why you chose that exercise in relation
to your data (in other words, why does it make sense to do that?), and
sufficient comments for a reader to understand your reasoning and code.

<!-------------------------- Start your work below ---------------------------->

# Exploring the Flow Sample Dataset

## Introduction

This project aims to explore the `flow_sample` dataset to identify
patterns and trends related to water flow across years, months, and
stations.

## Research Question

What is the relationship between the `month` and `flow` in the dataset;
am I able to use this data to see variation between seasons?

### 2.1: Data Exploration

#### Exercise 1: Plot the distribution of a numeric variable

My aim when creating a frequency graph focused on flow rates at maximum
extreme-type filters, was to gain a comprehensive understanding of water
usage under worst-case scenarios. When doing further statistical
analysis on the data, I would be able to identify systems skewed that
operate at lower flow rates and others that operate higher rates. This
is significant for identifying areas that could be targeted for water
conservation and efficiency improvements. These outliers can contribute
to platforms centred around environmental impact and sustainable water
usage.

``` r
# Firstly, I filtered the data to only include rows where the 'extreme_type' is 'maximum'
flow_sample_filtered_max <- flow_sample %>% filter(extreme_type == 'maximum')


#I then created a histogram based on this new subset of data
ggplot(flow_sample_filtered_max, aes(x=flow)) + 
  geom_histogram(binwidth=25, fill="blue", alpha=0.7, color="black") + 
  ggtitle("Frequency of Flow Rates for Maximum Extreme Type") +
  xlab("Flow Rate") +
  ylab("Frequency")
```

![](mda_deliverable1_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

### Exercise 2: Investigate the Number of Missing Values per Variable

I wanted look at the number of missing values per variable because it is
important for determining the quality of the dataset. A high number of
missing values in a particular variable could impact its reliability and
may require further data handling. Also, understanding missing data
patterns is helpful for better data preprocessing which can lead to
better questions, conclusions, and quality of research in general. Below
I create 2 plots. For context, when I created the first plot (includes
all variables), the number of missing data points from variable ‘sym’
affected the clarity of the other variables. I then created the exact
same plot with the exclusion of ‘sym’ to more clearly see the missing
values for the other variables.

``` r
# Here I count the number of missing values for each variable in the dataset
missing_values_count <- flow_sample %>%
  summarise(across(everything(), ~sum(is.na(.), na.rm = TRUE)))

# Convert the summarized data to a longer format using pivot_longer
missing_values_long <- missing_values_count %>% 
  pivot_longer(cols = everything(), names_to = "Variable", values_to = "Missing_Values")

# Create a bar plot to visualize the number of missing values for each variable
# This plot will show each variable on the x-axis and the number of missing values on the y-axis
ggplot(missing_values_long, aes(x = Variable, y = Missing_Values)) +
  geom_bar(stat = "identity", fill = "red", alpha = 0.7, color = "black") +
  ggtitle("Number of Missing Values Per Variable") +
  xlab("Variables") +
  ylab("Number of Missing Values")
```

![](mda_deliverable1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
# Count the number of missing values for each variable in the dataset
missing_values_count_excludingSYM <- flow_sample %>%
  summarise(across(everything(), ~sum(is.na(.), na.rm = TRUE)))

# Convert the summarized data to a longer format using pivot_longer
# Also filter out the 'sym' column from the dataset
missing_values_long_excludingSYM <- missing_values_count_excludingSYM %>% 
  pivot_longer(cols = everything(), names_to = "Variable", values_to = "Missing_Values") %>%
  filter(Variable != "sym")

# Create a bar plot to visualize the number of missing values for each variable
# Here, the 'sym' column is excluded from the plot
ggplot(missing_values_long_excludingSYM, aes(x = Variable, y = Missing_Values)) +
  geom_bar(stat = "identity", fill = "red", alpha = 0.7, color = "black") +
  ggtitle("Number of Missing Values Per Variable (Excluding 'sym')") +
  xlab("Variables") +
  ylab("Number of Missing Values")
```

![](mda_deliverable1_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

### Exercise 3: Explore the Relationship Between Month and Flow Rate for Seasonal Variation

I next wanted to analyze the relationship between “month” and “flow
rate” with a focus on uncovering seasonal variations. This was of
interest as certain months may exhibit significantly different flow
rates compared to others, for example, summer time could exhibit higher
flow rate because of increased water sports activities (swimming in
pools) or simply watering gardens. Understanding these dynamics is
essential for long-term water management strategies, as it could
highlight changing patterns in water flow rates that correlate with
certain months.

``` r
# I first filtered the dataset to include only the variables of interest, "month" and "flow"
flow_and_month <- flow_sample %>% select(month, flow)

# Next I created a boxplot to visualize the relationship between "month" and "flow"
ggplot(flow_and_month, aes(x = factor(month), y = flow)) +
  geom_boxplot(fill = "purple", alpha = 0.6, outlier.shape = 16, outlier.size = 1) +
  ggtitle("Seasonal Variation in Flow Rates by Month") +
  xlab("Month") +
  ylab("Flow Rate")
```

    ## Warning: Removed 2 rows containing non-finite values (`stat_boxplot()`).

![](mda_deliverable1_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

### Exercise 4: Filter Observations to Focus on Recent Years and Maximum Flow Rates

My aim in this exercise was to look at the flow rates for maximum
extreme-type filters (similar to exercise 1), but shifting the focus to
only the most recent years in the dataset. The reason for focusing on
recent data is to see if there are any recent trends in water usage. As
the dataset extends back to a century ago, much has changed and
developed, it would be more relevant for our knowledge to look at recent
years.

``` r
# I first filtered the data to only include rows where the 'extreme_type' is 'maximum' and the year is between 2010 and 2018
flow_sample_filtered_recent_max <- flow_sample %>% 
  filter(extreme_type == 'maximum' & year >= 2005 & year <= 2018)

# I then created a line graph to visualize the trend of flow rates over the years
ggplot(flow_sample_filtered_recent_max, aes(x=year, y=flow, group=1)) + 
  geom_line(color="blue") + 
  geom_point(color="red") +
  ggtitle("Trend of Flow Rates for Maximum Extreme Type for Years 2010-2018") +
  xlab("Year") +
  ylab("Flow Rate")
```

![](mda_deliverable1_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->
<!----------------------------------------------------------------------------->

# Task 3: Choose research questions

**(4 points)** So far, you have chosen a dataset and gotten familiar
with it through exploring the data. You have also brainstormed one
research question that interested you (Task 1.4). Now it’s time to pick
4 research questions that you would like to explore in Milestone 2!
Write the 4 questions and any additional comments below.

<!--- *****START HERE***** --->

### Future Research questions

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

<!----------------------------->

# Overall reproducibility/Cleanliness/Coherence Checklist

## Coherence (0.5 points)

The document should read sensibly from top to bottom, with no major
continuity errors. An example of a major continuity error is having a
data set listed for Task 3 that is not part of one of the data sets
listed in Task 1.

## Error-free code (3 points)

For full marks, all code in the document should run without error. 1
point deduction if most code runs without error, and 2 points deduction
if more than 50% of the code throws an error.

## Main README (1 point)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- In a sentence or two (or more??), briefly explains how to engage with
  the repository. You can assume the person reading knows the material
  from STAT 545A. Basically, if a visitor to your repository wants to
  explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## Output (1 point)

All output is readable, recent and relevant:

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

(0.5 point deduction if any of the above criteria are not met. 1 point
deduction if most or all of the above criteria are not met.)

Our recommendation: right before submission, delete all output files,
and re-knit each milestone’s Rmd file, so that everything is up to date
and relevant. Then, after your final commit and push to Github, CHECK on
Github to make sure that everything looks the way you intended!

## Tagged release (0.5 points)

You’ve tagged a release for Milestone 1.

### Attribution

Thanks to Icíar Fernández Boyano for mostly putting this together, and
Vincenzo Coia for launching.
