# Churn Prediction using AMLWorkbench - Data Preparation

## 1. Objectives

The aim of this lab is to understand how Vienna’s Data Preparation tools (based on Pendleton) can be used to clean and ingest customer relationship data for churn analytics.

The dataset used to ingest is from SIDKDD 2009 competition. The dataset consists of heterogeneous noisy data (numerical/categorical variables) from French Telecom company Orange and is anonymized.

## 2. Setup

1.	Begin the lab by creating a New Project by selecting the plus sign from Recent Projects.

![New Project](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/New%20Project.png)

2.	Provide a project name, project directory and select a blank project template as next steps. For the project directory, create a new directory for churn analytics and copy the path to project directory in the wizard.

![Project Name](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Project%20Name.png)

## 3. Data Source

Data Preparation is part of the Vienna client experience and installed with it. Vienna desktop application, offers an intuitive and powerful ML-based data preparation experience (a.k.a. Project "Pendleton") built on the PROSE (PROgram Synthesis using Example) technology.

PROSE is a framework of technologies for programming by examples – automatic generation of programs from input-output examples at runtime. PROSE includes a pre-defined suite of technologies for various kinds of data wrangling – cleaning and pre-processing raw semi-structure data into a form amenable to analysis.

1.	Select [Data Sources](Deep-Learning/blob/master/Unit Testing Bots.md) and click the + sign to add Data Source.

![Add Data Source](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Add%20Data%20Source.png)

2.	In the Add Data Source wizard, select File and provide the path of the local file.

![Local File](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Local%20File.png)

![Find File](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Find%20Files.png)

3.	In the File Details part of Add Data Source wizard, leave all the default options as is. You will be able to preview the data import as shown below.

![File Details](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/File%20Details.png)

4.	In the Data Types part of Add Data Source wizard, notice how all the numeric fields are shown with the Type: Number. If no type is specified, string is assumed. Hence, you do not need to add the type for all the categorical features.

![Data Types](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Data%20Types.png)

5.	In the Sampling part of Add Data Source wizard, select sample: “Top 1000 (Active)” and leave all other options default. Vienna allows users to have multiple samples per data source. The Active indicator lets the user choose which sample to use when displaying the data source.

![Sampling part](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Sampling%20part.png)

6.	Do not include path column in the Path Column part of Add Data Source wizard.

![Path Column Handling](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Path%20Column%20Handling.png)

## 4. Data Cleansing

1.	The concept of missing values is important to understand in order to successfully manage data.  If the missing values are not handled properly, the predictive models can be inaccurate. Handling missing values with Vienna is very simple. In this lab, we will replace the missing values with 0. Select the full dataset and then Transforms->Handle Missing Values to replace all missing values with 0.

![Handle Missing Values](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Handle%20Missing%20Values.png)

![Column Metrics](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Column%20Metrics.png)

2.	Select the full dataset and then Transforms->Remove Duplicates to eliminate duplicate copies of repeating data.

![Remove Duplicates](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Remove%20Duplicates.png)

3.	We can get rid of year and month fields from our dataset as they intuitively do not make sense to include in our dataset. Select the year column first and then Transforms->Remove Column.

    Similarly, remove the month column.

![Remove Column](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Remove%20Column.png)

4.	After following all the above steps, the summary steps should look as follows. Note that in the Handle missing values step, all the column names are displayed as we want this to apply on the full dataset. Additionally, a .dprep file would be created which can be used to create a data frame (details in next lab).

![Steps](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Steps.png)
