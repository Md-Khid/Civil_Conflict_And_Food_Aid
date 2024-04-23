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
root.dir = ""<your_directory_here>""
```
### Load Data
```
library(readxl)
df  <-  read_excel("FoodAid.xlsx")
```
### Install Packages
```
install.packages(c("stringr","dplyr", "tidyr", "ggplot2", "patchwork","tidyverse", "WDI","ggmap","leaflet", "ggrepel","scales"))
```
## Data Management
a.  Examine the Dataset

Based on the data [dictionary](#data-dictionary), certain variables represent the cumulative totals of various distinct variables. For this reason, it is important to consider the following aspects:

i.  The "overall_conflict" variable denotes the aggregate of both the "minor_conflict" and "major_conflict" variables.

ii. "Total_affected_disasters" corresponds to the summation of "affected_disasters" and "homeless_disasters" variables.

iii. "Total_affected_othercountries" is derived from the summation of "total_affected_neighbours," "total_affected_non_neighbours," and "nda_other_region" variables.

It should be noted that these sets of variables may not be compatible for simultaneous utilisation during the data exploration phase, as doing so may impede the attainment of accurate visualisation representation.

b.  Data Structure

Transforming the dataset into an R data frame results in the generation of 798 observations encompassing 25 variables. Analysing the data's structure reveals that all the variables are predominantly numeric in nature, except for "country," which is designated as a character variable, and "year," which is formatted as a date and time.

### Data Types
```
colnames(df)
head(df)
str(df)
```

<img width="491" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/f1ea89ea-fa0a-4e44-ade6-27649935320b">

c.  Data Transformation

To facilitate the creation of visualisation charts for the assignment, the following data processes will be performed:

i.  The conversion of numeric variables, namely 'overall_conflict,' 'minor_conflict,' 'major_conflict,' 'onsetwar,' 'offsetwar,' and 'polity2,' into categorical factors.

ii. The creation of new variables such as "total_food_aid" (emergency_food_aid + non_emergency_food_aid), "percent_total_food_aid_of_total_aid" (total_food_aid / total_aid), and "total_gdp" (gdp_per_capita \* population).

### Convert numeric variables into Categorical factors
```
df <- df %>%
  mutate(
    overall_conflict = factor(overall_conflict, levels = c(0, 1), labels = c("No", "Yes")),
    minor_conflict = factor(minor_conflict, levels = c(0, 1), labels = c("No", "Yes")),
    major_conflict = factor(major_conflict, levels = c(0, 1), labels = c("No", "Yes")),
    onsetwar = factor(onsetwar, levels = c(0, 1), labels = c("No", "Yes")),
    offsetwar = factor(offsetwar, levels = c(0, 1), labels = c("No", "Yes")),
    
    # Create categories for "polity2" scores
    polity2_category = cut(polity2,
                           breaks = c(-10, -6, 0, 5, 9, 10),
                           labels = c("Highly Autocratic", "Moderately Autocratic", "Neutral/Transitional", "Moderately Democratic", "Highly Democratic"),
                           include.lowest = TRUE)
  )
```
<img width="826" alt="2" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/8ffdc281-a75c-4c85-8a45-583273c07eb8">

### Create New Variables
```
df <- df %>%
  mutate(
    total_food_aid = emergency_food_aid + non_emergency_food_aid,
    percent_total_food_aid_of_total_aid = total_food_aid / total_aid,
    total_gdp = gdp_per_capita * population
  )
```
<img width="583" alt="3" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/079d8e15-8254-4e1c-a3bc-c89ce492fb19">

