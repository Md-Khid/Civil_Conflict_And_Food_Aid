# Project Overview

## Introduction

The intricate relationship between civil conflicts in Sub-Saharan Africa (SSA) and the distribution of emergency food aid is a multifaceted and interconnected matter. This study seeks to delve into this complex interplay. SSA, characterised by its diverse geography and intricate socio-political dynamics, consistently witnesses a recurring cycle of civil conflicts, each with its distinct triggers and consequences. Frequently, these conflicts are underpinned by common factors such as grievances, wealth and resource disparities, and food insecurity. Notably, food scarcity emerges as a prominent contributing factor, exacerbating conditions conducive to conflict and posing significant challenges for conflict resolution and post-conflict recovery.

Within this multifaceted context, emergency food aid serves a multifunctional role and is utilised by various stakeholders, including governments, rebel groups and international organisations. It functions as a tool for conflict prevention, management or even exploitation. This study aims to elucidate the nuanced and occasionally intricate interactions between emergency food aid and civil conflict in SSA. Utilising data spanning an 18-year period from 2002 to 2020, this study will employ various visualisation techniques to generate meaningful insights, fostering a comprehensive understanding of the relationship between conflict and food aid in the SSA region.

## Data
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

## Setting Up the Working Directory and Loading Data

### Set Directory
```
{r}
root.dir = ""<your_directory_here>""
```
