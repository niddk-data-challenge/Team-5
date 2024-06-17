# Intermediate/Advanced-Level Challenge: Aggregating and Harmonizing TrialNet Data
This repository contains the scripts used to generate the AI-ready dataset for the Intermediate/Advanced-level Data Centric Challenge using data from four studies within the Type 1 Diabetes TrialNet (TrialNet) network. 

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

The FI Consulting (FI) AI ready dataset is a curated and preprocessed dataset optimized for modeling and machine learning AI tasks. FI created this data set by merging all available study results into a single raw data set and then optimizing the data set in a sequential fashion. This AI ready dataset represents data on 235,396 patients contained in 259,064 rows and 473 columns. Each row represents a visit record.

As the data submission title suggests, FI has developed an algorithm to rapidly facilitate a data curator with the merging of large data sets from multiple sources using a FI developed AI/ML assisted semantic interoperability algorithm (SIA). FI has successfully demonstrated this methodology when merging data sets containing greater than 1,500 column headers and 400,000 values. This method identifies human error misspellings and typos not just in headers but in values. It also allows for standardization and de-duplication of variables. It future proofs studies by allowing for additional suggested headers as well. Workbench restrictions prevented FI from employing this method in this challenge (no graph database conversion allowed). What follows is a more traditional approach to preparing data sets from multiple sources.
