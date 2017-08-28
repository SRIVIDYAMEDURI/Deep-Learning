# Churn Prediction using Vienna - Data Preparation

## 1. Data Preparation

The aim of this lab is to understand how Vienna’s Data Preparation tools (based on Pendleton) can be used to clean and ingest customer relationship data for churn analytics. 
The dataset used to ingest is from SIDKDD 2009 competition. The dataset consists of heterogeneous noisy data (numerical/categorical variables) from French Telecom company Orange and is anonymized.

## 2. Setup

1.	Begin the lab by creating a New Project by selecting the plus sign from Recent Projects.

![New Project](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/New%20Project.png)

2.	Provide a project name, project directory and select a blank project template as next steps. For the project directory, create a new directory for churn analytics and copy the path to project directory in the wizard.

![Project Name](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/Project%20Name.png)

## 3. Data Source

Data Preparation is part of the Vienna client experience and installed with it. Vienna desktop application, offers an intuitive and powerful ML-based data preparation experience (a.k.a. Project "Pendleton") built on the PROSE (PROgram Synthesis using Example) technology.

PROSE is a framework of technologies for programming by examples – automatic generation of programs from input-output examples at runtime. PROSE includes a pre-defined suite of technologies for various kinds of data wrangling – cleaning and pre-processing raw semi-structure data into a form amenable to analysis.

1.	Select Data Sources and click the + sign to add Data Source.

![Add Data Source](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/Add%20Data%20Source.png)

2.	In the Add Data Source wizard, select File and provide the path of the local file.

![Local File](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/Local%20File.png)

![Find File](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/Find%20File.png)

3.	In the File Details part of Add Data Source wizard, leave all the default options as is. You will be able to preview the data import as shown below.

![File Details](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/File%20Details.png)

4.	In the Data Types part of Add Data Source wizard, notice how all the numeric fields are shown with the Type: Number. If no type is specified, string is assumed. Hence, you do not need to add the type for all the categorical features.

![Data Types](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/Data%20Types.png)
