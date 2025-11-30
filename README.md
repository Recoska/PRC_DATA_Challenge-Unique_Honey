<h1 align="center"> PRC Data Challenge 2025 </h1> <br>

<p align="center">
  PRC Data Challenge 2025 Team: Unique Honey
</p>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Introduction](#introduction)
- [Additional Data](#additional-data)
- [EDA](#eda)
- [Data Generation](#data-generation)
- [Model Training](#model-training)



<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Introduction

This repository contains the additional data and code for the PRC Data Challenge 2025. It includes everything needed to generate the final dataset and to train the machine learning model used for fuel-consumption prediction, enabling full reproducibility of the results.

All openly available external data is included and described in the Additional Data folder. The project consists of two main processes:

Data Generation – how the final dataset used for prediction is created.

Model Training – how the ML model is trained.

The Requirements section lists all libraries needed to run the pipelines. All code is written in Jupyter Notebook (.ipynb) format.

## Additional Data

We used three openly accessable data sources:

Aircraft Information:
https://github.com/atoff/OpenAircraftType/tree/master
In this repository a dataset is included and the following informations are taken based on the typecode:
- Wake Turbulence Category. L=Light,M=Medium,H=Heavy,J=Jumbo,S=Super
- Type of engines. P=Piston,J=JET,T=Turboprop/shaft,R=Rocket,E=Electric
- Number of engines.

Airport Information:
https://ourairports.com/data/
Here we included the type of the airport meaning its size.

ERA5 Weather Data:

## EDA

In the EDA folder scripts used for assessing the data is included. Here are the files listed and what plots they show:
- fuel_train.ipynb = Assessing different fuel segments and also as fuel per seconds
- fuel_analyze.ipynb = takes processed data and assesses fuel consumption based on typecode or the flightphase
- flightlist_train.ipynb = is a high level analysis of the training dataset
- compare_sub_files.ipynb = compares the training files with the submission files and gives relevant plots
- get_flights = gets all flights and gives relevant plots for analyzing them

Based on these plots some restrictions are done on data generation and some cleaning.



## Data Generation

The data generation process begins with data cleaning, performed using clean_data.ipynb. This script smooths the data, detects certain types of errors, and applies interpolation where necessary. It also creates some intermediate columns that are used later in the workflow but are not included in the final dataset.

Data cleaning is applied to all three datasets at the trajectory level: training, submission, and final. After cleaning, the same script proceeds to generate the final dataset. This step must be run separately for the training, submission, and final ranking datasets.

In this phase, a search algorithm identifies the start and end segments of each trajectory used for fuel consumption prediction and extracts the relevant segment. The dataframes_combine step then merges this extracted segment with the additional information required for fuel prediction modeling. Finally, build_final_row constructs the final dataset by generating new features and selecting the most important ones.


## Model Training




