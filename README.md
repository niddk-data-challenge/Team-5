# Intermediate/Advanced-Level Challenge: Aggregating and Harmonizing TrialNet Data
This repository contains the scripts used to generate the AI-ready dataset for the Intermediate/Advanced-level Data Centric Challenge using data from four studies within the Type 1 Diabetes TrialNet (TrialNet) network. 

## Preprocessing Challenge Datasets
To make dataset file sizes more manageable to merge in the NIDDK-CR Analytics Workbench environment hosted by AWS, while enabling Challengers to retain as many features as possible, the NIDDK-CR Support Team performed feature redactions and participant sampling (as described in the table below) prior to making the data available in the Workbench environment. This sampling schema retained the maximum number of participants and features that can be successfully merged in the Workbench environment, while maintaining a justifiable and useful study design for many potential use-cases, including multiple disease outcomes and life-course events. 

| Study | Datasets |  Features *    |Participants| Data Dictionary|
|------:|----------|----------------|------------|----------------|
|TN01|    32       |1,658           | 234,614    |[TN01_Data Challenge_Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/tn01-nh/TN01_Data_Challenge_Data_Dictionary_V1.pdf)|
|TN16|    13       |263             | 567        |[TN16_Data Challenge_Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/TN16_LIFT/TN16_Data_Challenge_Data_Dictionary_V1.pdf)|
|TN19|    24       |955             | 119        |[TN19_Data Challenge_Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/TN19_ATG_GCSF/TN19_Data_Challenge_Data_Dictionary_V1.pdf)|
|TN20|    29       |1,009           | 112        |[TN20 Data Challenge Data Dictionary_V1.pdf](https://repository.niddk.nih.gov/media/studies/TN20_IEOI/TN20_Data_Challenge_Data_Dictionary_V1.pdf)|

(*) Features that were fully empty (i.e., no non-missing values), free-text, or non-informative (i.e., all entries have the same value, or administrative variable) have been redacted from the study datasets.

## Documentation
Scripts used to preprocess the TN01, TN016, TN19, and TN20 datasets to generate the Challenge-specific datasets described above are available in the [name of folder]. Please reference the 

If you are requesting access to, or have access to the TrialNet data from the NIDDK-CR, please use these scripts to replicate the Challenge-specific datasets that were made available to participants for the Data Centric Challenge. 

### Study Documentation
Additional information about each study and corresponding documentation (e.g., protocols/MOPs, data collection instruments, etc.) are available for download from the NIDDK-CR website:
* TN01: https://repository.niddk.nih.gov/studies/tn01-nh/ 
* TN16: https://repository.niddk.nih.gov/studies/TN16_LIFT/ 
* TN19: https://repository.niddk.nih.gov/studies/TN19_ATG_GCSF/ 
* TN20: https://repository.niddk.nih.gov/studies/TN20_IEOI/ 
