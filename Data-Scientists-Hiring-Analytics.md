Data Scientist Hiring Analytics
================
Julian Clemente
8/30/2021

``` r
library(knitr)
knitr::opts_chunk$set(echo = TRUE)
```

## Background

### Personal Motivation/Interests

As someone looking to make a career change into the world of Big Data
(specifically as a data analyst), this particular Kaggle dataset
pertaining to the hiring of Data Scientists piqued my interest.
Analyzing this dataset seemed like a relevent and worthwhile data
analytics project that would be insightful and provide some perspective
on what the hiring landscape for data scientists currently looks like.
The results of this project might reveal the reasons why some data
scientists would move to a new company/job as well as the
ease/difficulty associated with HR finding a qualified data scientist
candidate interested in making that change.

### Context

This dataset was collected by an unnamed company that is active in the
big data/data science fields. After offering some data science courses
and training to anyone who’s signed up, the company wants to evaluate
which of these candidates who completed the course are interested in
working for the company or looking for a new employment. This should
effectively lead to a better strategic allocation of, if not a reduction
in, the cost and time spent on planning, registration of the training
and other controllable factors that can affect the overall course
quality. Further tailoring of the courses can also be done once the
company has better understanding of what its participants desire. All of
the candidate’s information related to demographics, education,
experience, etc are gathered upon course registration and can be used
for this analysis.

## Data Analysis Process

The six steps of the data analysis process as well as some guiding
topics that were considered and addressed at each phase are listed
below:

1.  Ask

    -   Problem identification & insight driven business decisions

2.  Prepare

    -   Data storage & organization
    -   Bias, credibility & data integrity
    -   Identification of problems/shortcomings of data

3.  Process

    -   Tool selection
    -   Data cleansing and documentation of process

4.  Analyze

    -   Data formatting
    -   Identification of trends or relationships
    -   Relation of insights to business questions

5.  Share

    -   Storytelling using new data insights
    -   Communication with audience verbally and via data visualization

6.  Act

    -   Final conclusions and future analysis
    -   Application of insights

## Ask

As discussed, this dataset was collected and designed by an unnamed Big
Data company in order for their HR department to understand the factors
and professional/academic characteristics of those looking to leave
current job (AKA turnover) for a different data science position at
another company or simply make a career change into Data Science .
Through the company’s gathered data of the current credentials,
demographics, experience data, the likelihood the course participant is
also looking for a new job or is willing work for the company can be
predicted. Other correlations in the data can be further investigated in
order to understand the turnover rate / career change trends that exists
within the data scientist hiring landscape.

## Prepare

### Data Source and Libraries

This dataset for the “HR Hiring Analytics of Data Scientists” was
downloaded off of
[Kaggle](https://www.kaggle.com/arashnic/hr-analytics-job-change-of-data-scientists).

This raw dataset will be stored locally for cleaning and processing via
RStudio. For sharing the completed analysis, the appropriate files and
this Rmarkdown file of this project will be uploaded to Github, an
online version control repository and website for sharing/collaborating
coding projects.

First, in order to view, process and better visualize these datasets,
the appropriate tidyverse and other visualization packages must be
installed (if so, uncomment line 43) and loaded, which is done so in the
following:

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.3     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.2     ✓ dplyr   1.0.6
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

The downloaded dataset is comprised of 3 csv files which can be
accessed, imported and viewed directly on RStudio with the tidyverse
packages that were just installed. However, only 1 of these csv files
(“aug\_train.csv”) is really useful for the scope of this analysis as it
is supposed to represent real data collected to train a predictive
machine learning model (supervised learning). One of the .csv files
(aug\_test.csv) is for verification that the developed supervised
learning model can accurately predict job interest, whereas the other
unused dataset file (“sample\_submission.csv”) is apparently sample
submission data (again, outside this project’s scope.)

The 19,158 long/narrow formatted observations in our “aug\_train.csv”
file are characterized by 14 attribute columns. What each column
represents is as described in further detail below:

-   enrollee\_id : Unique ID for candidate
-   city: City code
-   city\_ development\_index : Developement index of the city (scaled)
-   gender: Gender of candidate
-   relevent\_experience: Relevant experience of candidate
-   enrolled\_university: Type of University course enrolled if any
-   education\_level: Education level of candidate
-   major\_discipline :Education major discipline of candidate
-   experience: Candidate total experience in years
-   company\_size: No of employees in current employer’s company
-   company\_type : Type of current employer
-   lastnewjob: Difference in years between previous job and current job
-   training\_hours: training hours completed
-   target: 0 – Not looking for job change, 1 – Looking for a job change

### Data Credibility

To ensure this analysis is credible and unbiased, we consider the key
ROCCC criteria:

-   Reliable - Yes, this dataset is reliable. Despite the company
    collecting the HR hiring data is unnamed, this dataset was published
    on Kaggle and has been widely used by other Kaggle users for their
    own data analysis project. Therfore it is reasonable to believe that
    the data source is reliable. Kaggle has given this dataset a
    usability score of 10.0 due to it being easy to understand, its
    inclusion of the appropriate metadata, being saved in a machine
    readible format and being frequently maintained. At the time off
    this analysis, this datast has 1009 upvotes.
-   Original - Yes. The dataset is original since it was directly
    collected by the HR department of the unnamed Big Data company for
    their own analytics interests but is shared online for open source
    projects such as this one.
-   Comprehensive - Yes. This data contains various factors of interest
    that describe potential data scientist job candidates such as
    experience, education level, company size/type as well as level of
    interest for looking for a new job.
-   Current - Yes. This dataset was uploaded 9 months prior to the when
    this data analysis project was conducted, which would be around
    Dec 2020.
-   Cited - N/A. The company that collects this data remains
    anonymous/unnamed.

One problem/shortcoming of this data is that the data was collected
prior to the registration of the course/training offered by this company
(or at least that is my assumption based on the description on Kaggle).
It may be helpful to know whether the specific parameter, “target”,
which describes whether the participant is or is not looking for a job
change was influenced by the offered training. Further investigation or
clarification is needed to determine this. However, for the sake of this
analysis, we can proceed with the original assumption that the
participant’s decision was not influenced by the training itself.

## Process

### Import into RStudio

To begin the process step in our analysis tool of choice (R / RStudio),
we first read in the data from the locally stored our .csv files into R
with the following code.

``` r
# Read the selected csv files into R and assigning them variable names
DS_Candidates_Work_Data <- read.csv("..//Data Scientist Hiring Analytics/Raw Datasets/archive/aug_train.csv")
```

As you can tell already tell from this far into this project, this
Rmarkdown file serves to capture the comprehensive steps taken in all of
the data cleaning/transformation/analysis performed, the coding used to
generate our data visualizations, our interpretation/explanation of
results and our conclusions/recommendations we can draw from it.
Essentialy this writeup serves a similar purpose to Jupyter Notebooks or
any other documentation formats used for coding projects.

### Data Cleansing

To continue processing and/or transforming our data, it is imperative we
take a closer look at our data and ensure it is clean and ready to be
analyzed. Some useful R packages that may be useful to help us
accomplish this are “skimr” and “janitor” which are installed and loaded
in below.

``` r
# Uncomment the following lines if the "skimr" and "janitor" packages are not yet installed, otherwise, proceed to line 192)
#install.packages("skimr")
#install.packages("janitor")

library("skimr")
library("janitor")
```

    ## 
    ## Attaching package: 'janitor'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

One of the function from these libraries that I prefer using when
cleaning dataframe columns is the “clean\_names” function. This function
is used to ensure all column names are unique, only consist of letter,
numbers or the underscore (\_) character and have consistent casing
(lower case is preferred over upper case).

An additional correction that we make is changing the typo of “relevent”
to the proper spelling of “relevant” in the the column name.

``` r
DS_Candidates_Work_Data <- DS_Candidates_Work_Data %>% 
  rename(relevant_experience = relevent_experience)
```

Next, let’s preview the first few rows of our new data frame and the
newly cleaned column names to make sure we’re fully satisfied with the
cleaned output of the column names of our “DS\_Candidate\_Work\_Data”
dataframe.

``` r
head(DS_Candidates_Work_Data)
```

    ##   enrollee_id     city city_development_index gender     relevant_experience
    ## 1        8949 city_103                  0.920   Male Has relevent experience
    ## 2       29725  city_40                  0.776   Male  No relevent experience
    ## 3       11561  city_21                  0.624         No relevent experience
    ## 4       33241 city_115                  0.789         No relevent experience
    ## 5         666 city_162                  0.767   Male Has relevent experience
    ## 6       21651 city_176                  0.764        Has relevent experience
    ##   enrolled_university education_level major_discipline experience company_size
    ## 1       no_enrollment        Graduate             STEM        >20             
    ## 2       no_enrollment        Graduate             STEM         15        50-99
    ## 3    Full time course        Graduate             STEM          5             
    ## 4                            Graduate  Business Degree         <1             
    ## 5       no_enrollment         Masters             STEM        >20        50-99
    ## 6    Part time course        Graduate             STEM         11             
    ##     company_type last_new_job training_hours target
    ## 1                           1             36      1
    ## 2        Pvt Ltd           >4             47      0
    ## 3                       never             83      0
    ## 4        Pvt Ltd        never             52      1
    ## 5 Funded Startup            4              8      0
    ## 6                           1             24      1

The columns look pretty solid in terms of correctness and consistency.
However, from the 6 row output of the “head” function, it is noticeable
that some additional cleaning can be performed on a few of the column
values.

First, let’s focus on the very first column, “enrollee\_id”. Based on
personal experience, whenever identifiers or unique codes are assigned,
they should generally adhere to the rule of limiting to a equal \# of
characters (no more or less). Otherwise this potentially could lead to
indexing problems. For instance from the above “head” output, we notice
that row 5 has an enrollee\_id value of “666” whereas the enrollee\_id
value of the row right above it, “33241” has 2 more characters. For the
sake of consistency, we’ll begin modifying our data frame by updating
the enrollee\_id values to ensure they have exact the same number of
characters as the maximum \# found in this column.

Due to what identifiers typically represent, we shouldn’t expect the
need to perform any mathematical operations on the “enrollee\_id”
values. Therefore, it makes sense to convert these value types from
“int” to “chr”.

Before we do this, we first check for the max \# of digits/characters in
the enrollee\_id column, which shall serve as the standard number of
digits for this column going forward.

``` r
#Make sure there are no null values in this column, which could pose a problem later.
DS_Candidates_Work_Data %>%
  is.na() %>%
  sum()
```

    ## [1] 0

``` r
#Identify what the max number of digits for any value under this column.
max(nchar(DS_Candidates_Work_Data$enrollee_id))
```

    ## [1] 5

``` r
#Identify what the min number of digits for any value under this column.
min(nchar(DS_Candidates_Work_Data$enrollee_id))
```

    ## [1] 1

Knowing that the max \# of chars is 5 and the min \# of chars is 1, we
modify the enrollee\_id column accordingly.

``` r
#We will add leading zero(s) to any value that has 4 or less total characters to adhere to our 5 digit id rule.(E.g. "1" becomes "00001", "199" becomes "00199", etc)
DS_Candidates_Work_Data_mod1 <- DS_Candidates_Work_Data
DS_Candidates_Work_Data[1]<- formatC(DS_Candidates_Work_Data$enrollee_id, width = 5, format = "d", flag = "0") 
DS_Candidates_Work_Data_mod1 <- DS_Candidates_Work_Data
```

Now the “integer” to “character” type conversion can be performed.

``` r
#Convert all the values under the "enrollee_id" column from integers to characters/strings.
DS_Candidates_Work_Data_mod2 <- DS_Candidates_Work_Data_mod1 %>%
  mutate(enrollee_id = as.character(enrollee_id))

#Verify conversion by using "sapply" function as a check.
sapply(DS_Candidates_Work_Data_mod2, class)
```

    ##            enrollee_id                   city city_development_index 
    ##            "character"            "character"              "numeric" 
    ##                 gender    relevant_experience    enrolled_university 
    ##            "character"            "character"            "character" 
    ##        education_level       major_discipline             experience 
    ##            "character"            "character"            "character" 
    ##           company_size           company_type           last_new_job 
    ##            "character"            "character"            "character" 
    ##         training_hours                 target 
    ##              "integer"              "numeric"

Let’s continue exploring our data by examining the possible, unique
values one could get the non-integer and non-numeric columns of
interest. This could indicate where further cleaning can be performed by
bringing our attention to any erroneous data. Based on our “head”
preview earlier, some columns worth looking further into are “city”,
“gender”, “relevant\_experience”, “enrolled\_university”,
“education\_level”, “major\_discipline”, “company\_size”,
“company\_type” and “last\_new\_job”.

``` r
#List the unique values for the columns of interest (basically, non-discrete/qualitative columns).
print("All possible recorded values for city:") 
```

    ## [1] "All possible recorded values for city:"

``` r
  unique(DS_Candidates_Work_Data_mod2$city)
```

    ##   [1] "city_103" "city_40"  "city_21"  "city_115" "city_162" "city_176"
    ##   [7] "city_160" "city_46"  "city_61"  "city_114" "city_13"  "city_159"
    ##  [13] "city_102" "city_67"  "city_100" "city_16"  "city_71"  "city_104"
    ##  [19] "city_64"  "city_101" "city_83"  "city_105" "city_73"  "city_75" 
    ##  [25] "city_41"  "city_11"  "city_93"  "city_90"  "city_36"  "city_20" 
    ##  [31] "city_57"  "city_152" "city_19"  "city_65"  "city_74"  "city_173"
    ##  [37] "city_136" "city_98"  "city_97"  "city_50"  "city_138" "city_82" 
    ##  [43] "city_157" "city_89"  "city_150" "city_70"  "city_175" "city_94" 
    ##  [49] "city_28"  "city_59"  "city_165" "city_145" "city_142" "city_26" 
    ##  [55] "city_12"  "city_37"  "city_43"  "city_116" "city_23"  "city_99" 
    ##  [61] "city_149" "city_10"  "city_45"  "city_80"  "city_128" "city_158"
    ##  [67] "city_123" "city_7"   "city_72"  "city_106" "city_143" "city_78" 
    ##  [73] "city_109" "city_24"  "city_134" "city_48"  "city_144" "city_91" 
    ##  [79] "city_146" "city_133" "city_126" "city_118" "city_9"   "city_167"
    ##  [85] "city_27"  "city_84"  "city_54"  "city_39"  "city_79"  "city_76" 
    ##  [91] "city_77"  "city_81"  "city_131" "city_44"  "city_117" "city_155"
    ##  [97] "city_33"  "city_141" "city_127" "city_62"  "city_53"  "city_25" 
    ## [103] "city_2"   "city_69"  "city_120" "city_111" "city_30"  "city_1"  
    ## [109] "city_140" "city_179" "city_55"  "city_14"  "city_42"  "city_107"
    ## [115] "city_18"  "city_139" "city_180" "city_166" "city_121" "city_129"
    ## [121] "city_8"   "city_31"  "city_171"

``` r
print("All possible recorded values for gender:") 
```

    ## [1] "All possible recorded values for gender:"

``` r
  unique(DS_Candidates_Work_Data_mod2$gender)
```

    ## [1] "Male"   ""       "Female" "Other"

``` r
print("All possible recorded values for relevant_experience:") 
```

    ## [1] "All possible recorded values for relevant_experience:"

``` r
  unique(DS_Candidates_Work_Data_mod2$relevant_experience)
```

    ## [1] "Has relevent experience" "No relevent experience"

``` r
print("All possible recorded values for enrolled_university:") 
```

    ## [1] "All possible recorded values for enrolled_university:"

``` r
  unique(DS_Candidates_Work_Data_mod2$enrolled_university)
```

    ## [1] "no_enrollment"    "Full time course" ""                 "Part time course"

``` r
print("All possible recorded values for education_level:") 
```

    ## [1] "All possible recorded values for education_level:"

``` r
  unique(DS_Candidates_Work_Data_mod2$education_level)
```

    ## [1] "Graduate"       "Masters"        "High School"    ""              
    ## [5] "Phd"            "Primary School"

``` r
print("All possible recorded values for major_discipline:") 
```

    ## [1] "All possible recorded values for major_discipline:"

``` r
  unique(DS_Candidates_Work_Data_mod2$major_discipline)
```

    ## [1] "STEM"            "Business Degree" ""                "Arts"           
    ## [5] "Humanities"      "No Major"        "Other"

``` r
print("All possible recorded values for company_size:") 
```

    ## [1] "All possible recorded values for company_size:"

``` r
  unique(DS_Candidates_Work_Data_mod2$company_size)
```

    ## [1] ""          "50-99"     "<10"       "10000+"    "5000-9999" "1000-4999"
    ## [7] "10/49"     "100-500"   "500-999"

``` r
print("All possible recorded values for company_type:") 
```

    ## [1] "All possible recorded values for company_type:"

``` r
  unique(DS_Candidates_Work_Data_mod2$company_type)
```

    ## [1] ""                    "Pvt Ltd"             "Funded Startup"     
    ## [4] "Early Stage Startup" "Other"               "Public Sector"      
    ## [7] "NGO"

``` r
  print("All possible recorded values for experience:") 
```

    ## [1] "All possible recorded values for experience:"

``` r
  unique(DS_Candidates_Work_Data_mod2$experience)
```

    ##  [1] ">20" "15"  "5"   "<1"  "11"  "13"  "7"   "17"  "2"   "16"  "1"   "4"  
    ## [13] "10"  "14"  "18"  "19"  "12"  "3"   "6"   "9"   "8"   "20"  ""

``` r
print("All possible recorded values for last_new_job:") 
```

    ## [1] "All possible recorded values for last_new_job:"

``` r
  unique(DS_Candidates_Work_Data_mod2$last_new_job)
```

    ## [1] "1"     ">4"    "never" "4"     "3"     "2"     ""

The “city” values look fine. With no observable typos or errors, no
further cleaning is needed.

For “gender”, we can update the blank values to read “Not disclosed” for
further clarity.

``` r
#Mutate/Replace blank value with "Not disclosed"
DS_Candidates_Work_Data_mod3 <- DS_Candidates_Work_Data_mod2 %>%
  mutate(gender = replace(gender, gender=="", "Not disclosed"))

#Verify change
unique(DS_Candidates_Work_Data_mod3$gender)
```

    ## [1] "Male"          "Not disclosed" "Female"        "Other"

For “relevant\_experience”, since there are only 2 possible values, this
specific column is essentially a binary set of data and we can replace
the response “Has relevent experience” with “Y” and replace “No relevent
experience” with “N”. Also, the original response values to this column
have the typo discussed earlier.

``` r
#Mutate/Replace with "Y" or "N" responses accordingly
DS_Candidates_Work_Data_mod4 <- DS_Candidates_Work_Data_mod3 %>%
  mutate(relevant_experience = replace(relevant_experience, relevant_experience=="Has relevent experience", "Y")) %>%
  mutate(relevant_experience = replace(relevant_experience, relevant_experience=="No relevent experience", "N"))
  
#Verify change
unique(DS_Candidates_Work_Data_mod4$relevant_experience)
```

    ## [1] "Y" "N"

We apply a similar type of cleaning we previously performed on the
“gender” column to the “enrolled\_university”, “education\_level”,
“major\_discipline”, “company\_type”, “experience” and “last\_new\_job”
columns where we replace blank values with “Not Disclosed” or “Not
Applicable” depending on the context. This is done for clarity and
consistency.

``` r
#Mutate/Replace remaining blank values in other columns with "Not disclosed"
DS_Candidates_Work_Data_mod5 <- DS_Candidates_Work_Data_mod4 %>%
  mutate(enrolled_university = replace(enrolled_university, enrolled_university=="", "No enrollment data")) %>%
  mutate(enrolled_university = replace(enrolled_university, enrolled_university=="no_enrollment", "Not currently enrolled")) %>%
  mutate(education_level = replace(education_level, education_level=="", "No Data / Not applicable")) %>%
  mutate(major_discipline = replace(major_discipline, major_discipline=="", "Not applicable")) %>%
  mutate(company_type = replace(company_type, company_type=="", "No data / Not applicable")) %>%
  mutate(experience = replace(experience, experience=="", "No data / Not applicable")) %>%
  mutate(last_new_job = replace(last_new_job, last_new_job=="", "No data / Not applicable"))

#Verify changes
unique(DS_Candidates_Work_Data_mod5$enrolled_university)
```

    ## [1] "Not currently enrolled" "Full time course"       "No enrollment data"    
    ## [4] "Part time course"

``` r
unique(DS_Candidates_Work_Data_mod5$education_level)
```

    ## [1] "Graduate"                 "Masters"                 
    ## [3] "High School"              "No Data / Not applicable"
    ## [5] "Phd"                      "Primary School"

``` r
unique(DS_Candidates_Work_Data_mod5$major_discipline)
```

    ## [1] "STEM"            "Business Degree" "Not applicable"  "Arts"           
    ## [5] "Humanities"      "No Major"        "Other"

``` r
unique(DS_Candidates_Work_Data_mod5$company_type)
```

    ## [1] "No data / Not applicable" "Pvt Ltd"                 
    ## [3] "Funded Startup"           "Early Stage Startup"     
    ## [5] "Other"                    "Public Sector"           
    ## [7] "NGO"

``` r
unique(DS_Candidates_Work_Data_mod5$experience)
```

    ##  [1] ">20"                      "15"                      
    ##  [3] "5"                        "<1"                      
    ##  [5] "11"                       "13"                      
    ##  [7] "7"                        "17"                      
    ##  [9] "2"                        "16"                      
    ## [11] "1"                        "4"                       
    ## [13] "10"                       "14"                      
    ## [15] "18"                       "19"                      
    ## [17] "12"                       "3"                       
    ## [19] "6"                        "9"                       
    ## [21] "8"                        "20"                      
    ## [23] "No data / Not applicable"

``` r
unique(DS_Candidates_Work_Data_mod5$last_new_job)
```

    ## [1] "1"                        ">4"                      
    ## [3] "never"                    "4"                       
    ## [5] "3"                        "2"                       
    ## [7] "No data / Not applicable"

For the “company\_size” column, there is an obvious typo for one of the
values. One company size value reads “10/49” instead of “10-49”. This is
corrected below.

``` r
#Mutate/Replace incorrect value. Mutate/Replace blank value with "No data / Not applicable"
DS_Candidates_Work_Data_mod6 <- DS_Candidates_Work_Data_mod5 %>%
  mutate(company_size = replace(company_size, company_size=="10/49", "10-49")) %>%
  mutate(company_size = replace(company_size, company_size=="", "No data / Not applicable"))

#Verify change
unique(DS_Candidates_Work_Data_mod6$company_size)
```

    ## [1] "No data / Not applicable" "50-99"                   
    ## [3] "<10"                      "10000+"                  
    ## [5] "5000-9999"                "1000-4999"               
    ## [7] "10-49"                    "100-500"                 
    ## [9] "500-999"

Lastly, we perform some final checks on dataframe to ensure there is a
matching number of enrollee\_ids as there are observations and that
there are no duplicate observatons.

``` r
#Check the number of distinct enrollee_ids, which should be equal to the number of observations (19,158)
n_distinct(DS_Candidates_Work_Data_mod6$enrollee_id)
```

    ## [1] 19158

``` r
#Check for any duplicated rows
sum(duplicated(DS_Candidates_Work_Data_mod6))
```

    ## [1] 0

## Analyze

### Getting Aquainted with the Data

First, we look at the statistical spread and distribution of our data in
this analysis step. The following produces a high level summary.

``` r
# High level summary of DS_Candidates_Work_Data
summary(DS_Candidates_Work_Data_mod6)
```

    ##  enrollee_id            city           city_development_index
    ##  Length:19158       Length:19158       Min.   :0.4480        
    ##  Class :character   Class :character   1st Qu.:0.7400        
    ##  Mode  :character   Mode  :character   Median :0.9030        
    ##                                        Mean   :0.8288        
    ##                                        3rd Qu.:0.9200        
    ##                                        Max.   :0.9490        
    ##     gender          relevant_experience enrolled_university education_level   
    ##  Length:19158       Length:19158        Length:19158        Length:19158      
    ##  Class :character   Class :character    Class :character    Class :character  
    ##  Mode  :character   Mode  :character    Mode  :character    Mode  :character  
    ##                                                                               
    ##                                                                               
    ##                                                                               
    ##  major_discipline    experience        company_size       company_type      
    ##  Length:19158       Length:19158       Length:19158       Length:19158      
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  last_new_job       training_hours       target      
    ##  Length:19158       Min.   :  1.00   Min.   :0.0000  
    ##  Class :character   1st Qu.: 23.00   1st Qu.:0.0000  
    ##  Mode  :character   Median : 47.00   Median :0.0000  
    ##                     Mean   : 65.37   Mean   :0.2493  
    ##                     3rd Qu.: 88.00   3rd Qu.:0.0000  
    ##                     Max.   :336.00   Max.   :1.0000

Our high level summary already reveals some telling information about
the quantitative data that was collected.

### Part 1: City & Location Data

First, let’s examine the “city\_development\_index”, which is directly
associated with the adjacent “city” columm. Unfortunately, this dataset
only provides a city code \# for identification as opposed to the city
name itself. Therefore, we will be relying, on the
“city\_development\_index” to help characterize these cities. Per
[Wikipedia](https://en.wikipedia.org/wiki/City_development_index) (yes,
a more reliable source for research would have been preferred), City
Development Index or CDI, is a measure of a city’s level of development
and is based on factors such as infrastructure, waste, health, education
and product.

Based on the fact that the mean (0.8288) and median (0.9030) CDI values
of our data are heavily skewed towards the upper limit/max (0.949), most
participants come from a large and highly developed city vs. smaller
cities or towns. We visualize the distribution/representation of each
city code below.

``` r
#Out of the 123 total cities represented, we create a new table to store the 30 most frequently appearing cities on our "DS_Candidates_Work_Data_mod6" data frame in descending order
CityData <- DS_Candidates_Work_Data_mod6 %>% 
  group_by(city) %>%
  summarize(city_count = n()) %>% 
  arrange(desc(city_count)) %>%
  head(30)

#Plot results
CityData %>%
  ggplot(aes(x = reorder(city, -city_count), y = city_count)) + geom_bar(stat = "identity", fill = "dark green") + labs(title = "Top 30 Represented Cities Among Data Science Candidates") + xlab("City Code") + ylab("Count") +
  theme(axis.text.x = element_text(angle = 90)) 
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Limit%20to%2030%20Cities-1.png)<!-- -->

Now let’s correlate the top 30 most represented cities with their
respective CDI metric.

``` r
#First we'll merge (or join) our CityData df with our DS_Candidates_Work_Data_mod6 df based on the "city" value.
CityDatamod1 <- merge(x = CityData, y = DS_Candidates_Work_Data_mod6, by = 'city', all.x = TRUE) 
```

``` r
#Next, we create a subset that only displays the top 30 most represented cities and their corresponding CDIs and counts.
CityDatamod2 <- subset(CityDatamod1, 
              subset = !duplicated(CityDatamod1[c("city", "city_development_index")]),
              select = c("city", "city_development_index", "city_count")) %>%
              arrange(desc(city_count))
```

Both the city count and CDI are both plotted in a visualization to
further investigate for any potential correlation.

``` r
CityDatamod2 %>%
  ggplot(aes(x = reorder(city, -city_count), y = city_count, fill=city_development_index)) + geom_bar(stat = "identity")+
  scale_fill_gradientn(colors = c('green', 'yellow', 'red'), values = c(0, 50, 100/100))+
  labs(title = "Top 30 Represented Cities Among Data Science Candidates", subtitle ="Parameterized by Count & City Development Index (CDI)", x = "City Code", y = "Count", fill = "CDI") +
  theme(axis.text.x = element_text(angle = 90)) 
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Top%2030%20Represented%20Cities-1.png)<!-- -->

Judging from how wide a CDI spectrum is represented, our plot above
indicates that there is not a very strong correlation between CDI and
the city count our Data Science course participant originated from. The
top represented city (city\_103) accounts for a significant 22.7%
(4355/19158) of all participants and boasts a very high CDI.
Interestingly, the second most represented city (city\_21) which
accounts for 14.1% (2702/19158) has one of the lowest CDIs compared to
the other top 30 represented cities. This further reinforces the absence
of any correlation between CDI and City representation among the
potential candidates.

However, our work with using our City Data is not over yet. The final
piece of this data subset worth exploring involves determining the how
the ratio between those looking for a job change (target = 1) and those
not looking for a job change (target = 0) varies by our CDI metric.

``` r
#We will re-use a previous df, CityDatamod1, as it contains all our data of interest. However, this time, we will create a slightly different subset that tallies the number of rows where the target = 1 (aka, participant is looking for a job change).
CityDatamod3 <- subset(CityDatamod1, 
              select = c("city", "city_development_index", "city_count", "target")) %>%
              arrange(desc(city_count)) %>%
  group_by(city, city_count, target) %>%
  tally(name="n_job_change")
```

``` r
#We create a new subset, that removes the duplicate city row (where target = 0) that was created when we used the tally function. Additionally, we create a few new columns: One that counts the number of participants not looking for a job change (n_no_job_change) and the corresponding percentage relevent to the the total from that city (perc_no_job_change), the percentage of particpants looking for job change in that city (perc_job_change) and the ratio between those looking for a job change and those who aren't. The ratio is set up so that any number greater than 1 indicates that there are more people looking for a job change than those who aren't while a number less than 1 indicates the opposite.
CityDatamod4 <- subset(CityDatamod3, target!="0") %>%
  select(-target) %>%
  mutate(n_no_job_change = city_count-n_job_change, perc_job_change = n_job_change/city_count, perc_no_job_change = (city_count - n_job_change)/city_count, ratio_job_change = n_job_change/n_no_job_change)
```

``` r
#Now merge our dfs.
CityDatamod5 <- merge(x = CityDatamod4, y = DS_Candidates_Work_Data_mod6, by = 'city', all = TRUE) 

#Then create another dataframe that captures all of our previous city data (top 30) as well as the participant count of those people looking for a job change.
CityDatamod6 <- subset(CityDatamod5, 
              subset = !duplicated(CityDatamod5[c("city", "city_development_index")]),
              select = c("city","city_count", "city_development_index","n_job_change", "n_no_job_change", "perc_job_change", "perc_no_job_change", "ratio_job_change")) %>%
              arrange(desc(city_count)) %>%
              head(30)

#One quick note that should be mentioned that it is understood that the larger the sample size, the more accurate the results of the job change ratio will tend to be. However, the minimum city_count (113) of the selected top 30 cities  should still be sufficient enough for this analysis.
```

Now, let’s try to create a data visualization that illustrates the
correlation (if any) between the participant’s orgin city, the
associated city development index and their level of interest in looking
for a new data science job. We shall do this using a scatter plot where
the y-axis represents the target ratio and the color/size of each point
represents the city and its corresponding CDI.

``` r
CityDatamod6 %>%
  ggplot(aes(x = reorder(city, -ratio_job_change), y = ratio_job_change, color = city_development_index, size = city_development_index)) + geom_point(stat = "identity", position = "stack")+
  scale_color_gradientn(colors = c('red', 'yellow', 'green'), values = c(0, 50, 100/100))+
  labs(title = "Top 30 Represented Cities Among Data Science Candidates", subtitle ="Parameterized by Target Ratio (Interest vs. No Interest in Job Change) & CDI", x = "City Code", y = "Target Ratio", color = "CDI", size = "CDI") +
  theme(axis.text.x = element_text(angle = 90)) 
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Top%2030%20Cities%20(by%20Target%20Ratio)-1.png)<!-- -->

The results are intriguing. Of the top 30 represented cities, only 2
cities (city\_11 & city\_21) had ratios greater than 1. This indicates
that in both these cities, a majority of the participants are looking
for job change in Data Science. Comparing these two points to the right
side of the graph, we notice the points are noticeably smaller in size
and more orange/red in color. Therefore, we can expect that CDI has an
influence in the job change interest. Perhaps, location plays a
considerable role and these people are looking to relocate to a city
with a higher CDI.

Another metric we calculated was the percentages of people looking for a
job change as well as those who were not. This time we’ll plot these as
separate density curves overlapped on a single density plot. Instead of
identifying the city on the x-axis, we’ll plot the CDI values
themselves. Also, we’ll indicate the mean CDI of the top 30 cities
sampled with a dashed purple line, in order to give some perspective in
what the percentages look like in the most common cities our Data
Science candidates came from.

``` r
CityDatamod6 %>%
   select(-ratio_job_change) %>% 
   gather(type, identity, perc_job_change:perc_no_job_change) %>% 
   ggplot(., aes(x=city_development_index, y=identity, fill=forcats::fct_rev(type))) +
   geom_density(stat="identity", alpha=0.5) +
  labs(title = "Top 30 Represented Cities Among Data Science Candidates", subtitle ="Parameterized by CDI & Interest in Job Change (%)", x = "CDI", y = "% Interest") +
  scale_fill_discrete("Job Interest", 
                      labels=c("Not looking for Job Change", "Looking for Job Change")) +
  theme(axis.text.x = element_text(angle = 0)) + geom_vline(aes(xintercept=mean(city_development_index)),
            color="purple", linetype="dashed", size=0.75)
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Top%2030%20Cities%20by%20CDI%20&%20Job%20Change-1.png)<!-- -->

To conclude the results of this section’s analysis, we should generally
expect candidates who are currently residing in relatively lower CDI
areas (&lt; 0.65) are more likely to be interested in looking for a new
career in Data Science as it correlates to a new location. With the
“work from home” option becoming more and more prominent in today’s
society, it’ll be interesting to see how job listings and offerings that
push and advocate for this type of work (as opposed to paying for
expensive relocation packages) will affect this relationship.

### Part 2: Education

In this part of the data analysis, we’ll look beyond where the
participant came from and their external/environmental influences that
could impact whether they’re interested to find a new job or not, but
instead, examine closer their educational history and background.

Using the cleaned version of the df that contains all our potential
candidates data (DS\_Candidates\_Work\_Data\_mod6), we’ll create a new
df (called EducationData) to store all the columns that may be useful in
this section.

``` r
EducationData <- DS_Candidates_Work_Data_mod6 %>%
  select(enrollee_id, enrolled_university, education_level, major_discipline, experience, training_hours, target)
```

Let’s visualize the comparison between the different disciplines these
potential Data Scientist job candidates majored in through the use of
another bar chart.

``` r
EducationData %>% ggplot(aes(forcats::fct_relevel(major_discipline, c( "No Major", "Arts","Business Degree","Other", "Humanities","Not Applicable", "STEM")), fill=major_discipline)) + 
  geom_bar(stat="count") +
  labs(title = "Major Disciplines for Data Scientist Course Participants", x = "Count", y = "Major Discipline", fill = "Major Discipline") + 
  geom_text(aes(label = ..count..), stat= "count", vjust = 0.5, size=3) +
  theme(axis.text.x = element_text(angle = 90))
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Breakdown%20by%20Major-1.png)<!-- -->

We can immediately observe that the majors of a large portion (75.6%) of
the Data Science Course participants were of STEM (Science, Technology,
Engineering & Mathematics) backgrounds.

Those individuals with STEM backgrounds generally have a considerable
amount more relevent experience with statistics and programming than
other majors such as Humanities or Arts have. Therefore, it isn’t too
surprising to see why someone with a STEM degree would have or look to
having a Data Science career.

However, because having a more relevant background may sometimes not be
enough to prepare or qualify an individual new to Data Science, it is
important to also take a look at the distribution of the amount of
training hours in Data Science each person had gone through. A histogram
would be helpful visualization for this which is what we plot below.

``` r
EducationData %>% ggplot(aes(x= training_hours)) + 
  geom_histogram(aes(fill= ..count.. ), binwidth=20, stat="bin", lwd = 0.2) + 
  scale_x_continuous(name = "Training Hours ", breaks = seq(0, 340, 10), limits=c(0, 340)) +
  scale_fill_gradient( low = "yellow", high = "dark green") +
  labs(title = "Total Amount of Training Hours Among Data Science Candidates", x = "Count", y = "Count", fill = "Count") +
  stat_bin(binwidth=20, geom="text", colour="black", size=3, aes(label=..count.., y=1.05*(..count..))) +
  theme(axis.text.x = element_text(angle = 90)) 
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Breakdown%20by%20Total%20Amount%20of%20Training%20Hrs-1.png)<!-- -->

As shown by our histogram, most of those who participated in the
company’s data science courses only had between 10 to 30 hours of
training. This specific 10-30 hour training bin represents nearly a
quarter (24.7%) of the entire sample. This % representation continue to
drop as the \# of hours of training increases. Only 3.6% had greater
than 200 hours of training whereas 9.0% had virtually little to no
training at all with &lt; 10 hours.

Now that we’ve realized the the significant STEM major representation as
well as the distribution of total training hours, we move on to
evaluating the education level and current university enrollment. The
data visualizations for these are presented below.

``` r
EducationData %>%  ggplot(aes(x = enrolled_university, fill = enrolled_university))+
  geom_bar(stat = "count") +
  labs(title = "University Enrollment Status Among Data Science Candidates",  x = "Enrollment Status", y = "Count", fill = "Enrollment Status") +
   geom_text(aes(label = ..count..), stat = "count", vjust = -0.3, colour = "black") +
  theme(axis.text.x = element_text(angle = 90))
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Breakdown%20by%20Univ%20Enrollemnt%20Status-1.png)<!-- -->

``` r
EducationData %>%  ggplot(aes(x = education_level, fill = education_level))+
  geom_bar(stat = "count") +
  labs(title = "Highest Education Level Completed Among Data Science Candidates",  x = "Education Level", y = "Count", fill = "Enrollment Education") +
   geom_text(aes(label = ..count..), stat = "count", vjust = -0.3, colour = "black") +
  theme(axis.text.x = element_text(angle = 90))
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Breakdown%20by%20High%20Edu%20Level-1.png)<!-- -->

As we can clearly see from the data visualizations above, in regards to
education background, the most common participant (by % of each
category) fpr the company’s data science courses would be: \* college
graduate with a Bachelors - (72.1%) \* in a STEM major - (75.6%) \* that
is no longer or not currently enrolled in university - (72.1%) \* with
around 10-30 total hours of relevant training - (24.7%).

If Data Science participants of this educational background/history
appear to be attractive and qualified hires to the company, then it can
definitely be said that they are at least reaching and getting their
target audience to register.

However, the correlation between our education data and the company
targets still needs further investigation in order to establish that, in
addition to registration, the company is achieving their goal, from a
hiring perspective as well.

``` r
#Create a modified dataframe that "unites" the current enrollment status, highest education level completed and major into a single column. 
EducationDatamod1 <- EducationData %>%
  unite(enroll_eduLevel_maj, enrolled_university, education_level, major_discipline, sep = ", ")
```

Then, the target column is translated from a numeric to string/character
per the following key: 0 - “Not looking for new job” & 1 - “Looking for
new job”

``` r
EducationDatamod2<- EducationDatamod1 %>%
  mutate(target= ifelse(as.character(target) == "0", "Not looking for new job", as.character(target))) %>%
  mutate(target= ifelse(as.character(target) == "1", "Looking for new job", as.character(target))) %>%
  rename(job_search_status = target)
```

Create a modified dataframe that counts the frequency of each
combination education data and stores only the 20 most frequent results
(minimum sample size of 100 for each group/combination of enrollment
status, highest level of education and major) .

``` r
EducationDatamod3 <- EducationDatamod2 %>% 
  group_by(enroll_eduLevel_maj) %>% 
  summarise(Freq=n()) %>% 
  arrange(desc(Freq)) %>%
  head(20)
```

Then perform a merge using the last 2 modified dataframes we created.

``` r
EducationDatamod4 <- merge(x = EducationDatamod3, y = EducationDatamod2, by = 'enroll_eduLevel_maj', all.x = TRUE) 
```

Followed by the series of subset creation per a similar process to what
was done earlier in Part 1.

``` r
#Next, we create a subset that contains only the columns of interest
EducationDatamod5 <- subset(EducationDatamod4,
                     select = c("enroll_eduLevel_maj", "Freq", "training_hours", "job_search_status"))
                      
# This subset is created to conditionally tally the "job_search_status" columm
EducationDatamod6 <- EducationDatamod5 %>%
  arrange(desc(Freq)) %>%
  group_by(enroll_eduLevel_maj, Freq, job_search_status) %>%
  tally(name = "n_job_change")
  

# Then a final new df that only displays the 20 most frequent educational background combinations.
EducationDatamod7 <-  subset(EducationDatamod6, job_search_status != "Not look for new job") %>%
  select (-job_search_status) %>%
  mutate(n_no_job_change = Freq - n_job_change, perc_job_change = n_job_change/Freq, perc_no_job_change = (Freq - n_job_change)/Freq, ratio_job_change = n_job_change/n_no_job_change)

EducationDatamod8 <- subset(EducationDatamod7, 
              subset = !duplicated(EducationDatamod7[c("enroll_eduLevel_maj")]),
              select = c("enroll_eduLevel_maj","Freq", "n_job_change", "n_no_job_change", "perc_job_change", "perc_no_job_change", "ratio_job_change")) %>%
              arrange(desc(Freq)) %>%
              head(20)
```

The visualization of the most common academic backgrounds (where n &gt;
100) with respect to the target job search metrics is shown below.
Again, the target ratio is defined as the percentage of those looking
for a new job over the percentage not looking for a new job.

``` r
EducationDatamod8 %>% ggplot(aes(x=reorder(enroll_eduLevel_maj, ratio_job_change ), y=ratio_job_change, fill=enroll_eduLevel_maj )) + 
    geom_bar(position="dodge", stat="identity", alpha = 0.5) +
  ylim(0,1) +
  coord_polar(theta = "y") + 
  labs(title = "Target Ratios by Academic Background", subtitle = "For each academic group, n > 100", x = "Academic Background (descending count)", y = "Target Ratio", fill = "Academic Background: Enrollment Status, Highest Education Completed & College Major") +
  theme(axis.text=element_text(size=7), axis.title=element_text(size=10), legend.position="none")
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Target%20Ratios%20by%20Academic%20Background-1.png)<!-- -->

As we can see from our polar coordinate bar plot, Full time enrolled
Graduate students majoring in a STEM degree are most likely to be
looking for a new job, followed closely by not currently enrolled
Graduate Stem (perhaps recently graduated). There appears to be a
significant gap following these two groups.

What still needs to be accounted for is the average total amount of Data
Science training hours spent by each academia group. We create a final
EducationData df below that averages these values for each of the 20
groups examined.

``` r
EducationDatamod9 <- EducationDatamod5 %>%
    group_by(enroll_eduLevel_maj) %>% 
    summarise_each(funs(mean=mean(training_hours, na.rm=TRUE))) %>%
  select(-Freq_mean, -job_search_status_mean)
```

    ## Warning: `summarise_each_()` was deprecated in dplyr 0.7.0.
    ## Please use `across()` instead.

    ## Warning: `funs()` was deprecated in dplyr 0.8.0.
    ## Please use a list of either functions or lambdas: 
    ## 
    ##   # Simple named list: 
    ##   list(mean = mean, median = median)
    ## 
    ##   # Auto named with `tibble::lst()`: 
    ##   tibble::lst(mean, median)
    ## 
    ##   # Using lambdas
    ##   list(~ mean(., trim = .2), ~ median(., na.rm = TRUE))

``` r
EducationDatamod10 <- merge(x = EducationDatamod9, y = EducationDatamod8, by = 'enroll_eduLevel_maj', all.x = TRUE) 
```

We visualize this new df next using a scatter plot of the mean total
training hours for each academic background group and the corresponding
target ratio.

``` r
EducationDatamod10 %>% ggplot(aes(x = training_hours_mean, y = ratio_job_change, color = enroll_eduLevel_maj)) +
  geom_point(stat = "identity") +
  labs(title = "Target Ratio vs. Average Total Training Hours", subtitle = "By Academic Background",   x = "Average Total Training Hours", y = "Target Ratio", color = "Academic Background") +
 geom_text(aes(label=ifelse(ratio_job_change>0.5,as.character(enroll_eduLevel_maj),'')),hjust=.4,vjust=2, size=2.5) +
 geom_text(aes(label=ifelse(ratio_job_change<0.2,as.character(enroll_eduLevel_maj),'')),hjust=.4,vjust=2, size=2.5) +
 theme(axis.text=element_text(size=10), axis.title=element_text(size=10), legend.position="none")
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Target%20Ratio%20vs.%20Average%20Tot%20Training%20Hours-1.png)<!-- -->

All the academic backgrounds where the target ratio is greater than 0.5
or less than 0.2 are specifically labeled in our scatter plot.Based on
our visualization, it is clear that full time enrolled participant
whether they be graduates or Masters in a STEM degree appear strongly
interested in job change or new career in Data Science. However, this
does not appear to be the case wit hall STEM degree holders. While the
academic background group holding a STEM Phd may have one of the higher
average amount of total training hours, they represent a fairly low
target ratio and do not appear to have much interest in changing jobs.
Other groups that appear to have very low interest in switching to a new
job include those are not currently enrolled in any college courses but
have masters in humanities or who’s highest education was high school or
primary school.

### Part 3: Work Experience

In this final part of the analysis section, we’ll examine the the
enrollee’s current or previous work experience and the pertinent
information involving their work as a factor in whether or not they are
looking for a new job. Starting with our
DS\_Candidates\_Work\_Data\_mod6 dataframe, we’ll trim down to a more
concise df that captures just the columns of interest for this section.

``` r
WorkExpData <-DS_Candidates_Work_Data_mod6 %>%
  select(relevant_experience, experience, company_size, company_type, last_new_job, target)
```

One thing that was observed while parsing through and reviewing our new
WorkExpData df, is that the values under the Experience column can be
further modified/cleaned up. Currently, these values is a max of
discrete values for the \# of work experience each potential candidate
has as well as comparative value if the \# is above or below a certain
threshold (&lt; 1 or &gt; 20). From personal experience, there isn’t
much of a difference between someone with 7 years of experience vs. one
with 8 years. Therefore, it may be more useful and convenient to group
the years of experience by intervals of 5 as follows. Additionally, we
rename the values for “0” and “1” as “Not looking for new job” and
“Looking for new job” respectively.

``` r
WorkExpDatamod1 <-WorkExpData %>%
  mutate(experience = replace(experience, as.numeric(experience) >= 1 & as.numeric(experience) <= 5, "1 - 5")) %>%
  mutate(experience = replace(experience, as.numeric(experience) > 5 & as.numeric(experience) <= 10, "6 - 10")) %>%
  mutate(experience = replace(experience, as.numeric(experience) > 10 & as.numeric(experience) <= 15, "11 - 15")) %>%
  mutate(experience = replace(experience, as.numeric(experience) > 15 & as.numeric(experience) <= 20, "16 - 20")) %>%
  mutate(target = replace(target, as.character(target) == 0, "Not looking for new job")) %>%
  mutate(target = replace(target, as.character(target) == 1, "Looking for new job"))

#Verify changes
unique(WorkExpDatamod1$experience)
```

    ## [1] ">20"                      "11 - 15"                 
    ## [3] "1 - 5"                    "<1"                      
    ## [5] "6 - 10"                   "16 - 20"                 
    ## [7] "No data / Not applicable"

``` r
unique(WorkExpDatamod1$target)
```

    ## [1] "Looking for new job"     "Not looking for new job"

``` r
#Remove rows where, for experience, there is no data / no applicable, since the sample size for this is very small and shouldn't be very useful.
WorkExpDatamod2<-WorkExpDatamod1[!(WorkExpDatamod1$experience=="No data / Not applicable"),]
```

Then we prepare another modified dataframe that counts the number
corresponding with to the target value (whether or not there is interest
in looking for a new job)

``` r
WorkExpDatamod3 <- WorkExpDatamod2 %>%
  group_by(relevant_experience, experience, target) %>%
  tally(name = "target_count") 
```

``` r
#Re-order the years of experience in increasing order.
WorkExpDatamod3$experience <- factor(WorkExpDatamod3$experience, levels = c("<1", "1 - 5", "6 - 10", "11 - 15", "16 - 20", ">20"))

WorkExpDatamod3 %>%
  ggplot(aes( x=relevant_experience, y =target_count, fill = target,)) +
  geom_bar(stat = "identity", width = 0.75) +
  facet_grid(~experience) +
  labs(title = "Relevance & Number of Years Experience vs. Interest in Job Change", x = "Relevant Experience?", y = "Count", fill = "Job Change Interest") +
  geom_text(aes(label = target_count), stat = "identity",  colour = "black", size = 2.5, vjust=1.5, position = position_stack())
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Years%20exp%20vs%20Job%20Change%20interest-1.png)<!-- -->

Based on our visualization, we see that the group we expect to see
largest number of potential candidates with interest in finding a new
Data Science job with previous relevant experience is the 6 - 10 years
of experience range. Those with 1 - 5 years of experience also represent
a large proportion looking for a new job in data science, although
nearly half of these people may not have any relevant experience.

Now, let’s focus on the information we have regarding the current
companies that each course participant works for by creating another
modified df for this. Company size and company type are the specific
parameters we are interested in as we count the \# of individuals
interested/disinterested in finding a new job.

``` r
#Perform count for each of the target values.
WorkExpDatamod4 <- WorkExpDatamod2 %>%
  group_by(company_size, company_type, target) %>%
  tally(name = "target_count") 

#Reorder the company size by accending order.
WorkExpDatamod4$company_size <- factor(WorkExpDatamod4$company_size, levels = c("<10", "10-49", "50-99", "100-500", "500-999", "1000-4999", "5000-9999", "10000+", "No data / Not applicable"))
```

We create a facet wrap bar graph below, broken down by company type with
company size on the x-axis.

``` r
WorkExpDatamod4 %>%
  ggplot(aes(x=company_size, y =target_count, fill = target )) +
  geom_bar(stat = "identity", width = 0.75) +
  facet_wrap(~company_type) +
  labs(title = "Current Company Type & Size vs. Interest in Job Change", x = "Company Size", y = "Count", fill = "New Job  Interest") +
  geom_text(aes(label = target_count), stat = "identity", vjust = 2, colour = "black", size = 2.5, position = position_stack()) +
  theme(axis.text.x = element_text(angle = 90)) 
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Company%20Type%20&%20Size%20vs.%20Job%20Change%20interest-1.png)<!-- -->

Clearly based on the results above, it is no surprise that a majority
who don’t currently have a company type or size identified (or no data
was provided), would consist largely comprise the \# of participants
looking for a new job/job change (58%). Therefore, to remove we’ll
remove this in a new modified df and re-plot accordingly since it was
clearly obvious. It’s removal will also help to to uncover more hidden
insight.

``` r
#Remove the "No data / Not applicable" group from company_type
WorkExpDatamod5<-WorkExpDatamod4[!(WorkExpDatamod4$company_type=="No data / Not applicable"),]

#Remove the "Other" group from company_type.
WorkExpDatamod6<-WorkExpDatamod5[!(WorkExpDatamod5$company_type=="Other"),]

#Perform same operation above but for company_size where value is "No data / Not applicable".
WorkExpDatamod7<-WorkExpDatamod6[!(WorkExpDatamod6$company_size=="No data / Not applicable"),]

#Replot
WorkExpDatamod7 %>%
  ggplot(aes(x=company_size, y =target_count, fill = target )) +
  geom_bar(stat = "identity", width = 0.75) +
  facet_grid(~company_type) +
  labs(title = "Current Company Type & Size vs. Interest in Job Change", x = "Company Size", y = "Count", fill = "New Job  Interest") +
  geom_text(aes(label = target_count), stat = "identity", vjust = 2, colour = "black", size = 2, position = position_stack()) +
  theme(axis.text.x = element_text(angle = 90)) 
```

![](Data-Scientists-Hiring-Analytics_files/figure-gfm/Company%20Type%20&%20Size%20vs.%20Job%20Change%20interest%20(remove%20misc)-1.png)<!-- -->

From our new and improved faceted bar graph, we can see that a majority
of our participants overwhelmingly come from private limited companies
of all sizes. Regardless of the size of the company or the the company
type, there is no stand out that shows more participants coming from a
particular company type/size are more interested in looking in a new job
vs. keeping their current job. Other than a few companies where the
sample size is fairly small, most combinations of company types and
sizes have a ratio of anywhere between 5:1 to 7:1 in terms of not
looking for a new job vs. looking for a new job. Further details about
the particular company need to be investigated as company size and type
aren’t sufficient or definitive enough.

## Share

The preferable method of sharing these findings would be to do so using
the RMarkdown file (.rmd) and publishing the documented analysis process
and findings on an online Data Science community such as Kaggle or via
personal online portfolio. The company that collected the data scientist
course data is unnamed so there is no use in trying to reach out and
share the insights documented on this R Markdown notebook. The selected
method I’ve chosen to share his project is via Github and personal Data
Analysis portfolio. With the in-line R code/chunks used throughout the
case study documentation and analysis process, making sharing this .rmd
file convenient to publish, Github is equipped with the appropriate
kernals to run the code and create the visualizations as intended. Also,
as a popular version control tool, this analysis is easily accessible
andsimple to revisit and update as necessary.

## Act

### Discussion

To reiterate, the purpose of this analysis was to help identify what
sort of academic, professional or background traits typify course
registrants looking to find a Data Science position within the company
offering this course. This could be anything from the turnover of an
experienced Data Scientists with years of relevant experience or a fresh
(or even currently enrolled) college student looking to find their first
job in the field. The overall goal is to help this company understand
and fulfill its hiring needs by correlating the vast backgrounds of it’s
many participants with that of someone looking to work for this company.
All three parts of our analysis reveal some key insights that could help
the Human Resources department of the unnamed Big Data company with
their recruitment for potential new Data Scientists.

In the first part of our analysis we evaluated each participant’s city
of origin and the associated City Development Index (CDI). CDI is a
measure of a city’s level of development in areas such as
infrastructure, education and health. As revealed by this section of the
analysis, one may be able to expect that candidates originating from a
city with a CDI less than 0.65 are more likely to be looking/interested
in a new job versus candidates that are content with their current
situation in a city with a relatively higher CDI. Looking for a new job
vs. not looking for a new job largely correlates with the decision of to
move to a new city. A candidate who is unhappy with their living
situation (we can typically expect CDI is an indicator of how well a
city can provide the quality of life one looks for), may try to find a
new job in another city that satisfies their quality of life standards
and expectations. One main takeaway for HR from these results is that
they are more likely to find new candidates interested in positions at
their company with them from these types of cities where CDI is
typically lower. Obviously this assumes that the company itself is
located in a city with a higher CDI and would be willing to potentially
cover a relocation package to that new city, which can be costly.
However no information was provided in regards to the unnamed company’s
location/CDI and further exploration will be needed. In addition,
another limitation and note to consider about basing candidate’s job
change interest (or disinterest) is that the qualifications of the
candidate (in terms of their academic background and any relevant
experiences) are not yet taken into account. Fortunately, we address
these areas in the subsequent analysis sections.

The potential candidates academic background is closely considered and
evaluated in Part 2 of this analysis. We examine attributes such as
highest level of education completed, major discipline, \# of training
hours completed and whether the participant is currently enrolled as a
student (part time or full time) or not at all. Because of the technical
and math-intensive nature of Data Science, it wasn’t too surprising to
discover that a significant majority of course participants had come
from a STEM background in college.The \# of training hours completed for
Data Science wasn’t too signficant, however, as the average total \# of
training hours came out to roughly 10-30 hours. In this context,
training hours refer to any learning time (excluding college enrolled
course or through a on-the-job learning experience through a current
employer) that is focused and geared to learning Data Science. For
example, this could even refer to taking the Data Science offered course
by the Big data company itself. Typically those who don’t have relevant
job experience or did not specifically major/specialize in Data Science
while in College would require more training hours (how much exactly
requires further investigation and is not within this analysis scope).
Therefore, we can suppose that quite a bit of these candidates received
their Data Science learning mostly through college or relevant
experience, or that those without as strong of a background/experience
in it, did not invest as many hours to learn the discipline. The former
is further reinforced as our subsequent data visualizations show that a
majority of participants are already college graduates (bachelors) that
are not currently enrolled in any full time or part time coursework for
higher education (i.e. masters or PHd in data science or related).

Of the various combinations of academic backgrounds that the course
participants represented, we identifed the 20 most common combinations
of (current enrollment and type, highest education level completed and
college major, if applicable) and grouped them to assess correlations
with their target ratio. We defined target ratio as the ratio between
whether a participants is looking for a new job vs. not looking for a
new job. Our polor coordinate bar graph revealed that the top 2 academic
background groups with the highest ratio represented participants who
had already graduated from college (bachelors) with a STEM degree. The
difference between the first (76.4%) and second (75.2%) highest ratio
groups is whether that the former is currently full time enrolled. The
subsequent scatter plot further clarifies the difference between these
two academic groups as the group where no enrollment is specified
(presumably no enrollment) has a considerably higher average amount of
training hours versus the full time enrolled group. This is easily
explainable by the amount of free time a non-enrolled person would have
versus that of someone who is a full time student. Despite this, it is
clear that those who have already earned a STEM college degree (graduate
only) are expected to be more interested in finding a new Data Science
job than those who majored in something such as the Arts, Humanities or
Business and/or did not complete college (highest education level is
primary or high school). Interestingly, those with STEM backgrounds but
have PHDs also represent a group that has a low target ratio. Perhaps,
it can be inferred that a different field (perhaps academic/university
research in specialized Data Science topics such as Machine Learning,
AI, etc) is more suited and aligned for their professional goals.
Therefore, it is recommended that the big data company considers the
Graduate STEM (presumably bachelors, not masters or PHD) group as a
“sweet spot” , in terms of gauging the overall job change interest
levels across the represented academic groups.

Academics aside, the current and prior work experience for these
potential candidates is also crucial to evaluate as it provides
practical knowledge of how to apply Data Science in a real world
setting. This is the specific area we hone in on in Part 3 of our
analysis. The first plot we created was a side by side bar graph that
showed the count of the number of people who were interested in finding
a new job, not interested in finding a new job, as broken up by whether
they had relevant Data Science job experience and additionally faceted
by the range for the \# years of experience. One important insight that
we learn from this data visualization is that the 1-5 and 6-10 years of
experience groups largely comprise the total course participants.
Between these two groups, a larger proportion of participants with
between 1-5 years of experience are more interested in finding a new
career vs. having no interest. As the total number of years of
experience increase, the gap between the count of those with relevant
experience and those without relevant experience significantly widens.
This means that people who are looking to making a career change,
typically do so at a younger age with either &lt;1 years of total
experience or 1-5 years of total experience. It is shown to be rare that
someone with 20+ years of experience (irrevelant to data science) would
be looking to make a career shift to Data Science after participating in
the companys data science coursework. Other than the group with &lt;1
year of relevant experience (where the count is exactly equal), the
remaining groups show that the count not looking for a career change in
data science (whether this be turnover to a new company as a current
data scientist or a career change) exceeds (sometimes drastically) the
count for those that are looking for a new job. This tells us that in
order to more successfully recruit experienced Data Scientists, the
company should look into career opportunities that already established
data science desire at later stages of their career. Perhaps this may
mean increased leadership opportunities or roles in mentoring younger
data scientists. There are obviously increased roles and
responsibilities that go along with the levels/years of experience.
There are only a limited number of these “higher” level roles in a
company (not everyone can be a lead data analyst/data manager). Having
such a role in your current company, more likely roots you into staying
vs. early/mid career data scientists with less than 10 years of
experience, who can find similar increased roles through job changes.
Therefore, the company should understand the general difficulty in
recruiting more experienced data scientists compared to earlier/mid
career data scientists simply due to the various structures and
organizations that exist.

Another plot we created in this section is a faceted bar graph that
illustrates a side by side bar graph and breakdown of the current
company types/sizes that the potential candidates work for. By far, most
participants who currently work, are employed by a Private Limited
company of all various sizes. The 3 most common company sizes were those
between 50-99 employees (relatively small), 100 - 500 (small) and
10,000+ (very large). The other company types we examined were early
stage startups, funded startups, NGOs and the public sector.
Unfortunately there was simply no stand out in that for all the various
company types and sizes, the ratio between current employees not looking
for a new job far exceeded those that were actually were searching.
However, it was observed that overall, the target ratio between interest
in a new job vs. no interest was generally higher for Private Limited
companies as opposed to the remaining company types. There tends to be a
negative connotation when it comes the term “corporation”. Therefore, it
may be worth exploring company culture as a factor in employee
retention. However, this is not specific to data scientists but for all
types of employees.

### Summary

The key takeaways from our analysis that the company should consider and
may utilize/act on from a hiring perspective is as follows:

-   Understand that there are geographical and quality of life
    influences from the city of origin for course participants that may
    influence their design to find new jobs. However, after a certain
    threshold (appears 0.65 CDI per our collected data), the location
    has little to no influence as CDI continues to rise.
-   The more experience (11+ years) data scientists are typically more
    “rooted” with their current employer, meaning that job
    changes/turnover often much less often than those with in the 1-5 or
    6-10 years of experience range. This may also suggest there is less
    of a desire to re-learn and get accustomed to the operations of a
    new company in later stages in one’s career, whereas earlier career
    candidates are willing to be more flexible.
-   WIth the exception of PHD holders, participants with STEM degrees
    (bachelors or masters) in general are most representative of those
    looking to make the switch to a new company or get into a data
    science job for the first time. Because the total training hours
    varies so greatly between high job change interest (or target ratio)
    participants, the total hours of specialized training is not
    indicative of a strong correlation.
-   Compared to start-ups, NGOs or the public sector, a significant
    majority of course participants come from private limited
    company/corporations. While, in general, there is not strong
    evidence that suggests the size of a company affects
    turnover/change, the private limited companies appear to have a
    higher proportion of turnover/change than the other company types.
    Further research should be done to investigate if and what the
    defining characteristics are for these different company types are
    and how certain things such as management style, company culture,
    employee benefits & pay/compensation can vary.
