# Intermediate/Advanced-Level Challenge: Aggregating and Harmonizing TrialNet Data
This repository contains the scripts used to generate the AI-ready dataset for the Intermediate/Advanced-level Data Centric Challenge using data from four studies within the Type 1 Diabetes TrialNet (TrialNet) network, including:
* TN01 (Pathway to Prevention),
* TN16 (Long-Term Investigative Follow-Up),
* TN19 (ATG-GSCF in New Onset T1D), and
* TN20 (Immune Effects of Oral Insulin in Relatives at Risk for Type 1 Diabetes Mellitus)

Participants were instructed to 1) prepare a single dataset by aggregating all data files associated with one or more longitudinal studies on T1D listed above, and 2) augment the single dataset to ensure AI-readiness.

FI Consulting, led by Dr. Alice Loveys, successfully consolidated and unified multiple TrialNet datasets and identified data outliers. The team enhanced raw data to ensure consistent variable representation and identified numeric and categorical “missingness” to prevent modeling bias, thus enhancing TrialNet data for AI-readiness. The team prepared a dataset for time-series analysis, making the data more likely to inform prevention and personalized treatment plans for those at risk of diabetes and diabetes-related complications. FI Consulting selected the prize to present their challenge results at the NIH Office of Data Science Strategy (ODSS) Data Sharing and Reuse Seminar Series. The recording from the May 10, 2024 presentation is available [HERE](https://www.youtube.com/watch?v=CrABW02QB30).

## Preprocessing Challenge Datasets
To make dataset file sizes more manageable to merge in the NIDDK-CR Analytics Workbench environment hosted by AWS, while enabling Challengers to retain as many features as possible, the NIDDK-CR Support Team performed feature redactions and participant sampling (as described in the table below) prior to making the data available in the Workbench environment. This sampling schema retained the maximum number of participants and features that can be successfully merged in the Workbench environment, while maintaining a justifiable and useful study design for many potential use-cases, including multiple disease outcomes and life-course events. 

| Study | Datasets |  Features *    |Participants| Data Dictionary|
|------:|----------|----------------|------------|----------------|
|TN01|    32       |1,658           | 234,614    |[TN01_Data Challenge_Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/tn01-nh/TN01_Data_Challenge_Data_Dictionary_V1.pdf)|
|TN16|    13       |263             | 567        |[TN16_Data Challenge_Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/TN16_LIFT/TN16_Data_Challenge_Data_Dictionary_V1.pdf)|
|TN19|    24       |955             | 119        |[TN19_Data Challenge_Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/TN19_ATG_GCSF/TN19_Data_Challenge_Data_Dictionary_V1.pdf)|
|TN20|    29       |1,009           | 112        |[TN20 Data Challenge Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/TN20_IEOI/TN20_Data_Challenge_Data_Dictionary_V1.pdf)|

(*) Features that were fully empty (i.e., no non-missing values), free-text, or non-informative (i.e., all entries have the same value, or administrative variable) have been redacted from the study datasets. Please reference the [name of file] that contains a list of features that were redacted/dropped from the TN01, TN16, TN19, and TN20 datasets.

Documentation used to preprocess the TN01, TN16, TN19, and TN20 datasets to generate the Challenge-specific datasets described above are available in the [name of folder]. Please reference the [name of file] that contains a list of features that were redacted/dropped from the TN01, TN16, TN19, and TN20 datasets.

If you are requesting access to, or have access to the TrialNet data from the NIDDK-CR, please reference this documentation to replicate the Challenge-specific datasets that were made available to participants for the Data Centric Challenge. 

### Study Documentation
Additional information about each study and corresponding documentation (e.g., protocols/MOPs, data collection instruments, etc.) are available for download from the NIDDK-CR website:
* TN01: https://repository.niddk.nih.gov/studies/tn01-nh/ 
* TN16: https://repository.niddk.nih.gov/studies/TN16_LIFT/ 
* TN19: https://repository.niddk.nih.gov/studies/TN19_ATG_GCSF/ 
* TN20: https://repository.niddk.nih.gov/studies/TN20_IEOI/

## Generating the AI-Ready Data

### Title of Project: Data Curation and Harmonization via AI/ML Assisted Semantic Interoperability Algorithm (SIA) 

#### _Description of AI-Ready Dataset_
The FI Consulting (FI) AI ready dataset is a curated and preprocessed dataset optimized for modeling and machine learning AI tasks. FI created this data set by merging all available study results into a single raw data set and then optimizing the data set in a sequential fashion. This AI ready dataset represents data on 235,396 patients contained in 259,064 rows and 473 columns. Each row represents a visit record.

As the data submission title suggests, FI has developed an algorithm to rapidly facilitate a data curator with the merging of large data sets from multiple sources using a FI developed AI/ML assisted semantic interoperability algorithm (SIA). FI has successfully demonstrated this methodology when merging data sets containing greater than 1,500 column headers and 400,000 values. This method identifies human error misspellings and typos not just in headers but in values. It also allows for standardization and de-duplication of variables. It future proofs studies by allowing for additional suggested headers as well. Workbench restrictions prevented FI from employing this method in this challenge (no graph database conversion allowed). What follows is a more traditional approach to preparing data sets from multiple sources.

#### _Data Enhancements and Methods used for preparing AI-ready dataset_

The first area FI addressed was raw data enhancement to assure consistent variable representation for optimal data modeling and machine learning. These enhancements included column header harmonization, variable unit and data type harmonization, and the identification of errant, zero, and null values.

Date and time column header harmonization.

In the raw data set, date and time components were in distinct columns (dd, mm, yyyy , hour, sec). Since each column represents an independent variable in modeling, this is not an optimal way to represent date and time. Instead, FI consolidated these columns into a single date time format.

For date, FI filtered data column headers for those representing a date unit such as month, day, or year, then merged those columns into a single column with the date format of mm/dd/yyyy. FI then eliminated the separate month, day, year columns. Similarly for time, FI filtered column headers for those representing a time unit such as hour, minute, and second and merged them into a single column with a format of hh:min:ss.

FI recognizes that in merged data sets, further column header semantic harmonization is possible. For example, two headers may represent the same test even though the header names differ. The most challenging problem is how to understand semantic relationships among text data. Curators are doing this manually, which is time-consuming and may make human errors. Curators may also require specialized training and expertise in medical or bioinformatics domain. Interpretation of semantic relationships can be subjective and context dependent. FI recommends further data set harmonization using the SIA algorithm.  SIA is part of a methodology that streamlines data curation.  A human still makes the final determination on harmonization. 

Data Type Conversion and Measurement Unit Standardization. 

For meaningful modeling and analysis, a column’s variables must be consistent in data type. Additionally, if the variable represents a measurement, all variables in that column must be represented by the same measurement unit. If two people had the same blood glucose, but one was measured in mmol/L and the other in mg/dL, the absolute value of the test results would be different. The model would not recognize this difference and would not be able to rectify it. Correcting and standardizing data type must occur before any imputing of missing numeric variables and encoding categorical variables.

Correcting data types

FI ran code to validate variable values data types within a column. For categorical variables, FI examined those columns with more than 20 unique values by displaying them and then judging if the data should be converted to numerical variables. And, for numeric variables with less than 10 unique values, FI displayed them for assessment to determine if they should be converted to categorical variables.

Value types for Hct were represented as either a percentage or an integer. FI harmonized the Hct data type, so all were represented as a percentage of blood. 

Standardizing measurement variables

FI used the data dictionary to identify measurement variables. FI assured each value was represented based on either SNOMED standards or the Observational Medical Outcomes Partnership Common Data Model since this is NIDDK-CDR’s reported Common Data Model (CDM). FI also identified disparate measurement units by creating histograms of numeric data types. If the numeric data type values all have the same unit of measurement, the resulting histogram had a single curve. However, if the histogram had two curves, this suggested multiple units of measurement. FI identified and harmonized the following variable measurement units.

Converted variable: to standard measurement pairs.
* Height: cm
* Weight: kg
* Glucose results: mg/dl
* Hbg: mg/dl

Handling Errant Values

Identifying Data within 99.5% Range
When data is input into a database, there is the chance that there is not accurately input due to human-error. This leads to inaccurate, and in some cases, implausible data. To address this in a dataset as large as this one, FI determined a percentile range for variables with a numeric data type. FI operated under the assumption that most data are input correctly and that incorrect data inputs are a small portion of the total dataset. FI filtered columns that had an indicator for result to only include the middle 99.5%. This filter was only applied to values that were marked as “Yes” for having a normal value. Values labeled as “No” were already known to have abnormal values and did not need to be addressed this way. Only values that have a “Yes” label were filtered as they as supposed to be an acceptable value. The filter removes any that were more likely to be entered in error.

The use of the standard definition of outliers to filter the data was another possibility. FI decided against this as outliers are typically calculated as 1.5 times the inter-quartile range less than the first quartile or greater than the third quartile. The removal of these outliers would remove legitimate data that appear in healthcare measurements. A model that generates a conclusion based on a set of healthcare data should not have people with outlier measurements dismissed.

Addressing variables with a “zero value” 

While some zero values may be acceptable for a given variable, FI identified where this was not the case. FI selected only those variables, such as weight or height, for which the value cannot be zero. These values were located by viewing distributions and unique values for numeric variables. FI used context to either remove the variable or impute a value to a non-zero value. Removing the variable will result in an “NA” value for the modeling.

Time-series analysis optimization

The second area FI focused on was optimizing the data for meaningful time-series analysis by harmonizing the data on “MaskID” and “Visit Date” to establish a clear and unique reference point for each patient's data across multiple visits.

Harmonizing by MaskID and Visit Date:

To ensure different lab results are correctly associated with each patient, FI used “MaskID” and “Date_of_Draw” (the date the lab sample was collected) as primary keys to embed lab results. This maintained the uniqueness of the “MaskID” and “Date_of_Draw” combinations. FI proceed by changing the “Date_of_Draw” in the lab result record to “Visit_Dt”. This allowed FI to merge the embedded lab results with other information, ensuring that “MaskID” and “Visit_Dt” together acted as a unique identifier for each entry in the dataset.

#### _How did you handle the missing data_

The data set should represent the most informative and reliable data available for meaningful data analysis.

Identifying missing (NULL) or incorrect zero values

Incorrect or missing values can adversely affect data modeling and analysis. Zero or NULL values may incorrectly introduce modeling bias. To handle NULL values, FI identified those columns with more than 99.95% missing data points and removed those columns. Removing columns containing a substantial amount of missing data eliminated factors that would have minimal impact on subsequent modeling and analysis. Imputing the missing values in those columns could introduce bias into any modeling and is therefore not recommended.

Graph data science is unique in that it can handle null values.  FI would recommend database conversion to a graph database format for further data exploration and analysis. 

Remaining categorical variables

For categorical variables with missing values, FI  used an encoding categorical variables method. First, FI identified those categorical variables with missing values. ‘NaN’ or ‘null’ values that were assigned a specific category or label to ensure that no information was lost. By doing so, FI effectively transformed the missing data points into a distinct category of their own. The encoding technique can preserve the integrity of the original dataset while ensuring that the missing values are treated as meaningful entities rather than being disregarded or excluded. Encoding categorical variables facilitates downstream analysis, including machine learning and statistical modeling.

Remaining numeric variables
For numeric variables with missing values below 50%, FI chose to impute the missing values using the K-Nearest Neighbors (KNN) Imputer. This method allows missing value estimations based on the similarity between data points, helping to maintain the integrity of the dataset. It can capture complex relationships and patterns in the data.

For numeric variables with missing values above 50% and less than 99%, FI created a Missing Indicator. This means instead of imputing, FI created a binary indicator variable that flags whether a value was missing or not. This can help machine learning models learn from the missingness pattern.

#### _Potential Use-cases for AI-Ready Dataset_

Diabetes:  Identifying risks for diabetes development or complication risk

Because this data set is optimized for time-series analysis, the dataset may be valuable for identifying those at risk of developing diabetes or those at risk from developing serious diabetic complications. The data contains longitudinal records that allow for tracking the progression of diabetes in patients over time. Researchers and healthcare practitioners can employ time series analysis techniques to monitor the evolution of the disease and identify trends or patterns in patient outcomes.

A modeler could extract feature importance from the trained machine learning model allowing researchers and healthcare professionals to leverage this information to gain insights into the factors that play a significant role in the development or progression of diabetes. The result can guide preventive measures and personalized treatment plans for individuals at risk of diabetes or diabetic complications. Even without developing machine learning models, a researcher could build statistical modeling and correlation studies, to identify the variables that impact or correlate with each other.
