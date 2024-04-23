# Project Overview

## Introduction

The intricate relationship between civil conflicts in Sub-Saharan Africa (SSA) and the distribution of emergency food aid is a multifaceted and interconnected matter. This study seeks to delve into this complex interplay. SSA, characterised by its diverse geography and intricate socio-political dynamics, consistently witnesses a recurring cycle of civil conflicts, each with its distinct triggers and consequences. Frequently, these conflicts are underpinned by common factors such as grievances, wealth and resource disparities, and food insecurity. Notably, food scarcity emerges as a prominent contributing factor, exacerbating conditions conducive to conflict and posing significant challenges for conflict resolution and post-conflict recovery.

Within this multifaceted context, emergency food aid serves a multifunctional role and is utilised by various stakeholders, including governments, rebel groups and international organisations. It functions as a tool for conflict prevention, management or even exploitation. This study aims to elucidate the nuanced and occasionally intricate interactions between emergency food aid and civil conflict in SSA. Utilising data spanning an 18-year period from 2002 to 2020, this study will employ various visualisation techniques to generate meaningful insights, fostering a comprehensive understanding of the relationship between conflict and food aid in the SSA region.

## Data Dictionary
The dataset analysed in this study covers countries located in the SSA region over an 18-year period from 2002 to 2020. It includes data from a total of 54 countries within the SSA region encompassing a wide range of variables related to civil conflicts, natural disasters, economic indicators and political circumstances. The table below outlines the variables of dataset followed by a brief description of the data.

| Variable Name       | Variable Labels                                                                 | Source                                                                                                      |
|---------------------|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| country             | Country Name                                                                   |                                                                                                             |
| year                | Year                                                                           |                                                                                                             |
| overall_conflict<sup>1</sup>     | Civil conflict: =1 if more than 25 battle-related deaths, =0 if otherwise      | [Uppsala Conflict Data Program (UCDP)](https://ucdp.uu.se/)<sup>1</sup>                                                   |
| minor_conflict<sup>1</sup>       | Civil conflict: =1 if >25 to <1000 battle-related deaths, =0 if otherwise      |                                                                                                             |
| major_conflict<sup>1</sup>       | Civil conflict: =1 if >999 battle-related deaths, =0 if otherwise              |                                                                                                             |
| onsetwar<sup>1</sup>             | Onset (i.e. start) of civil conflict - more than 25 battle-related deaths      |                                                                                                             |
| offsetwar<sup>1</sup>            | Offset (i.e. end) of civil conflict - more than 25 battle-related deaths       |                                                                                                             |
| battle_deaths<sup>1</sup>        | Number of battle-related deaths due to civil conflict                          |                                                                                                             |
| civilian_deaths<sup>1</sup>      | Number of civilian deaths due to government attacks                           |                                                                                                             |
| death_disasters<sup>2</sup>     | Number of deaths by natural disasters                                         | [Emergency event database (EM-DAT) by CRED](https://www.emdat.be/)<sup>2</sup>                                         |
| injured_disasters<sup>2</sup>   | Number of injured by natural disasters                                        |                                                                                                             |
| affected_disasters<sup>2</sup>  | Number of people requiring immediate assistance from natural disasters        |                                                                                                             |
| homeless_disasters<sup>2</sup>  | Number of people who became homeless from natural disasters                   |                                                                                                             |
| total_affected_disasters<sup>2</sup>      | Total number affected by natural disasters in a country                       |                                                                                                             |
| total_affected_othercountries<sup>2</sup> | Total number affected by natural disaster in other countries                   |                                                                                                             |
| total_affected_neighbours<sup>2</sup>     | Total number affected by disasters, immediate neighboring countries           |                                                                                                             |
| total_affected_non_neighbours<sup>2</sup> | Total number affected by disasters, non-immediate neighboring countries       |                                                                                                             |
| nda_other_region<sup>2</sup>              | Number of natural disaster affected people in non-Sub-Saharan African regions  |                                                                                                             |
| emergency_food_aid<sup>3</sup>              | Emergency food aid received, in million USD                                   | [Creditor Reporting System (CRS) by OECD](https://stats.oecd.org/Index.aspx?DataSetCode=CRS1)<sup>3</sup>              |
| non_emergency_food_aid<sup>3</sup>          | Non-humanitarian or development food aid, in million USD                      |                                                                                                             |
| total_aid<sup>3</sup>                       | Total aid for all sectors (code 1000), constant price & in million USD        |                                                                                                             |
| gdp_per_capita<sup>4</sup>                  | GDP per capita, PPP (constant 2011 international $)                           | [World Development Indicators](https://databank.worldbank.org/source/world-development-indicators)<sup>4</sup>           |
| inflation<sup>4</sup>                       | Inflation, GDP deflator (annual %)                                            |                                                                                                             |
| population<sup>4</sup>                    | Population, total                                                              |                                                                                                             |
| polity2<sup>5</sup>                         | Polity2 score (-10 to 10), where -10 for most autocratic regime and 10 for most democratic regime | [Polity IV study database](https://www.systemicpeace.org/politystudy.html)<sup>5</sup>                              |


## Software Platform
The data quality check, cleaning process and visualisation creation and analysis for this study will be conducted using the RStudio platform version 2023.06.1, Build 524.

## Set Up Working Directory and Load Data

### Set Directory
```
# Set the root directory path 
root.dir = "<your_directory_here>"
```
### Load Data
```
# Load readxl package for reading Excel files
library(readxl)

# Read Excel file named "FoodAid.xlsx" and store as 'df' dataframe
df <- read_excel("FoodAid.xlsx")

```
### Install Packages
```
# Install necessary R packages for data manipulation, visualisation and mapping
install.packages(c("stringr",     # For string manipulation functions
                   "dplyr",       # For data manipulation functions
                   "tidyr",       # For data tidying functions
                   "ggplot2",     # For creating visualisations using grammar of graphics
                   "patchwork",   # For arranging multiple ggplots into single figure
                   "tidyverse",   # Meta-package that loads several packages for data science tasks
                   "WDI",         # For accessing World Bank data
                   "ggmap",       # For creating maps using Google Maps
                   "leaflet",     # For creating interactive maps
                   "ggrepel",     # For adding non-overlapping text labels to ggplot2 plots
                   "scales"))     # For modifying axis scales and breaks in ggplot2

```

### Install Libraries
```
# Load necessary libraries for data manipulation and visualisation
library(stringr)      # For string manipulation functions
library(dplyr)        # For data manipulation functions
library(tidyr)        # For data tidying functions
library(ggplot2)      # For creating visualisations
library(patchwork)    # For combining multiple ggplot2 plots
library(tidyverse)    # For data manipulation and visualisation functions
library(WDI)          # For accessing World Bank data
library(ggmap)        # For creating maps with ggplot2
library(leaflet)      # For creating interactive maps
library(ggrepel)      # For adding text labels to ggplot2 plots
library(scales)       # For scaling functions for ggplot2
```
## Data Management
### a.  Examine the Dataset

Based on the data [dictionary](#data-dictionary), certain variables represent the cumulative totals of various distinct variables. For this reason, it is important to consider the following aspects:

i.  The "overall_conflict" variable denotes the aggregate of both the "minor_conflict" and "major_conflict" variables.

ii. "Total_affected_disasters" corresponds to the summation of "affected_disasters" and "homeless_disasters" variables.

iii. "Total_affected_othercountries" is derived from the summation of "total_affected_neighbours," "total_affected_non_neighbours," and "nda_other_region" variables.

It should be noted that these sets of variables may not be compatible for simultaneous utilisation during the data exploration phase, as doing so may impede the attainment of accurate visualisation representation.

### b.  Data Structure

Transforming the dataset into an R data frame results in the generation of 798 observations encompassing 25 variables. Analysing the data's structure reveals that all the variables are predominantly numeric in nature, except for "country," which is designated as a character variable, and "year," which is formatted as a date and time.

#### Data Types
```
# Provide summary of data structure
str(df)
```

<img width="491" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/f1ea89ea-fa0a-4e44-ade6-27649935320b">

### c.  Data Transformation

To facilitate the creation of visualisation charts for the study, the following data processes will be performed:

i.  The conversion of numeric variables, namely 'overall_conflict,' 'minor_conflict,' 'major_conflict,' 'onsetwar,' 'offsetwar,' and 'polity2,' into categorical factors.

#### Convert numeric variables into Categorical factors
```
# Convert variables to factors with "No" and "Yes" labels
df <- df %>%
  mutate(
    overall_conflict = factor(overall_conflict, levels = c(0, 1), labels = c("No", "Yes")),
    minor_conflict = factor(minor_conflict, levels = c(0, 1), labels = c("No", "Yes")),
    major_conflict = factor(major_conflict, levels = c(0, 1), labels = c("No", "Yes")),
    onsetwar = factor(onsetwar, levels = c(0, 1), labels = c("No", "Yes")),
    offsetwar = factor(offsetwar, levels = c(0, 1), labels = c("No", "Yes")),
    
    # Create categories for "polity2" scores
    polity2_category = cut(polity2,
                           breaks = c(-10, -6, 0, 5, 9, 10),  # Define breaks for categorization
                           labels = c("Highly Autocratic", "Moderately Autocratic", "Neutral/Transitional", "Moderately Democratic", "Highly Democratic"),  # Define labels for each category
                           include.lowest = TRUE)  # Include lowest value in the first interval
  )

```
<img width="826" alt="2" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/8ffdc281-a75c-4c85-8a45-583273c07eb8">

ii. The creation of new variables such as "total_food_aid" (emergency_food_aid + non_emergency_food_aid), "percent_total_food_aid_of_total_aid" (total_food_aid / total_aid), and "total_gdp" (gdp_per_capita \* population).

#### Create New Variables
```
# Mutate the dataframe to calculate the total food aid by summing emergency and non-emergency food aid
# Calculate the percentage of total food aid compared to total aid
# Compute the total GDP by multiplying GDP per capita with population
df <- df %>%
  mutate(
    total_food_aid = emergency_food_aid + non_emergency_food_aid,
    percent_total_food_aid_of_total_aid = total_food_aid / total_aid,
    total_gdp = gdp_per_capita * population
  )

```
<img width="583" alt="3" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/079d8e15-8254-4e1c-a3bc-c89ce492fb19">

#### Extract the Year from the ‘year’ Column for Data Merging 

```
# Extract the first four characters from the 'year' column and create a new column called 'year'
df <- df %>%
  mutate(year = substr(year, 1, 4))
```
<img width="665" alt="4" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/5961f291-02fe-4dc5-b14c-c64a4c196012">

### d. Additional Data Abstraction

Additional data will be retrieved from the World Development Indicators (WDI) databank and incorporated into the existing dataset. This task involves the extraction of data series specific to the SSA region, including ‘MS.MIL.XPND.CD’ (Military Expenses) and ‘SN.ITK.DEFC.ZS’ (Prevalence of Undernourishment). The examination of military expenses can offer valuable insights into regional security and expenditures related to conflicts, while the assessment of undernourishment prevalence is a crucial indicator of food insecurity, with the potential to contribute to civil unrest.

#### Abstract Additional Data from WDI API
```
# Define the list of Sub-Saharan African countries
sub_saharan_africa_countries <- c(
  "AO", "BJ", "BF", "BI", "CV", "CM", "CF", "TD", "KM", "CG", "CI", "DJ", "ER",
  "SZ", "ET", "GM", "GH", "GN", "GW", "KE", "LS", "LR", "MG", "MW", "ML", "MR",
  "MZ", "NA", "NE", "NG", "RW", "SN", "SL", "SO", "ZA", "SD", "TZ", "TG", "UG",
  "ZM", "ZW", "CD"
)

# Define the list of indicators
indicators <- c(
  "MS.MIL.XPND.CD",     # Military Expenses
  "SN.ITK.DEFC.ZS"      # Prevalence of Undernourishment
)

# Fetch WDI data for the selected indicators and countries
wdi_data <- WDI(
  country = sub_saharan_africa_countries,
  indicator = indicators,
  start = 2002,
  end = 2020
)

# View the retrieved data
View(wdi_data)
```
<img width="724" alt="5" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/c3d49050-fefd-45e6-8b28-ec1db56c6737">

