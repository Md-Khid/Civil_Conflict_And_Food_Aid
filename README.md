  # Project Overview

## Introduction

This study explores the complex link between civil conflicts in Sub-Saharan Africa (SSA) and emergency food aid distribution. SSA with its diverse geography and socio-political dynamics experiences recurrent conflicts driven by factors like grievances, wealth disparities and food insecurity. Food scarcity worsens conditions for conflict and hampers conflict resolution and recovery. This study aims to uncover the intricate interactions between emergency food aid and civil conflict in SSA using data from 2002 to 2020. Visualisation techniques will be used to gain insights into this relationship.
                        
## Software Platform
The data quality check, cleaning process and visualisation creation and analysis for this study will be conducted using the RStudio platform version 2023.06.1, Build 524.

## Set Up Working Directory and Load Data

### Set Directory and Load Data

<img width="681" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/617f321a-327a-46e3-a469-11fb6de24f2c">


### Install Packages
```
# Install necessary R packages for data manipulation, visualisation and mapping
install.packages(c("stringr",     # For string manipulation functions
                   "dplyr",       # For data manipulation functions
                   "ggplot2",     # For creating visualisations using grammar of graphics
                   "patchwork",   # For arranging multiple ggplots into a single figure
                   "WDI",         # For accessing World Bank data
                   "leaflet",     # For creating interactive maps
                   "ggrepel",     # For adding non-overlapping text labels to ggplot2 plots
                   "scales"))     # For modifying axis scales and breaks in ggplot2
```

### Install Libraries
```
# Load necessary libraries for data manipulation and visualisation
library(stringr)      # For string manipulation functions
library(dplyr)        # For data manipulation functions
library(ggplot2)      # For creating visualisations
library(patchwork)    # For combining multiple ggplot2 plots
library(WDI)          # For accessing World Bank data
library(leaflet)      # For creating interactive maps
library(ggrepel)      # For adding text labels to ggplot2 plots
library(scales)       # For scaling functions for ggplot2
```
## Data Management

### a.  Examine the Dataset

As per the data [description](https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/blob/main/FoodAid.xlsx), some variables represent combined totals of distinct variables. Hence, it's crucial to consider:

i. "overall_conflict" equals "minor_conflict" and "major_conflict."

ii. "Total_affected_disasters" equals "affected_disasters" and "homeless_disasters."

iii. "Total_affected_othercountries" equals "total_affected_neighbours", "total_affected_non_neighbours" and "nda_other_region."

As using these variable sets simultaneously in data exploration may hinder accurate visualisation.


### b.  Data Structure

Converting the dataset to an R data frame yields 798 observations with 25 variables. Analysis shows most variables are numeric except "country" noted as a character variable and "year" formatted as date and time.

#### Data Types

<img width="491" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/f1ea89ea-fa0a-4e44-ade6-27649935320b">

### c.  Data Transformation

To make visualisation charts for the study, the study will:

i. Convert numeric variables ('overall_conflict', 'minor_conflict', 'major_conflict', 'onsetwar', 'offsetwar' and 'polity2') into categories.

#### Convert numeric variables into Categorical factors

<img width="824" alt="2" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/5e93efdd-de35-457f-a7bb-45b3a457c34a">

ii. Create new variables: "total_food_aid" (sum of emergency_food_aid and non_emergency_food_aid), "percent_total_food_aid_of_total_aid" (total_food_aid divided by total_aid) and "total_gdp" (gdp_per_capita multiplied by population).

#### Create New Variables

<img width="1124" alt="3" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/c8c8d84e-1485-4d43-990d-484ac231fe4c">


#### Extract the Year from the ‘year’ Column for Data Merging 

<img width="668" alt="4" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/23ccd993-039c-4d5c-b35c-e09a96b78103">

### d. Additional Data Abstraction

More data from the World Development Indicators (WDI) will be added to the current dataset focusing on SSA region stats like ‘MS.MIL.XPND.CD’ (Military Expenses) and ‘SN.ITK.DEFC.ZS’ (Prevalence of Undernourishment). Looking at military spending gives insights on security and checking undernourishment levels is crucial for food security which affects civil unrest potential.

#### Abstract Additional Data from WDI API

<img width="664" alt="5" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/07091986-c867-4cbf-bfc7-3e16a0300859">

### e.	Merging Data

The World Development Indicators (WDI) dataset will have country names aligned with the existing dataset for accurate identification. Years from the 'year' column in the existing dataset will be converted to integers for standardisation. Both datasets will be merged based on 'country' and 'year' columns.

<img width="686" alt="5" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/a7e98a28-7bbe-4829-b323-c5cf298cd016">

#### Rename variables

<img width="684" alt="6" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/eceb2413-1e28-4ded-a116-b3b01d81667b">

### f.	Missing Values

To maintain data integrity and avoid visualisation errors, missing values will be replaced with 'NA' in the merged dataset. This ensures consistency for analysis. Key variables with over 100 missing rows include: 

•	onsetwar (126 missing)

•	offsetwar (126 missing)

•	battle_deaths (126 missing)

•	civilian_deaths (126 missing) 

•	Military Expenditure (128 missing)

#### Check for Missing Values

<img width="557" alt="7" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/9f573c9e-539b-42c6-952c-727fbdf4bd3e">

#### Create and Store Country Locations

<img width="698" alt="8" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/89bb55e8-7d00-4aaa-9f6d-22d41b15088c">

## Data Findings

### Polity2 vs Population

#### Yr.2002
<img width="524" alt="9" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/1929b2c4-5475-48f1-b2d2-c05e26535803">

#### Yr.2020

<img width="525" alt="10" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/231f2f84-c073-4adc-873d-94d9ab4a035b">

The scatter plot depicts SSA countries' Polity2 scores. It can be observed that Eswatini, Eritrea, Gambia, Mauritania, Togo, Chad, Uganda, Ethiopia, Sudan, Angola, Zimbabwe and Rwanda have maintained autocratic governments from 2002 to 2020. These nations might be governed by one-party systems or military rule possibly restricting political freedoms and human rights. The limited emigration from these nations could also be due to hardships, economic constraints, fear, strict immigration policies and risk aversion.

### Polity2 vs Total GDP

<img width="524" alt="11" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/09536caf-82ba-42f7-b92d-b79192860511">

Countries with lower Polity2 scores (-10 to 0) experienced slower GDP growth from 2002 to 2020 while nations with higher scores (0 to 10) saw stronger growth. This difference may stem from limited political freedom and transparency in lower-scoring countries, discouraging people and investors. Democratic nations tend to offer more stable political climates attracting investment and boosting GDP.

### Military Expenditure by Country

<img width="720" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/61d2c03c-774c-48ab-9f7c-5345abd8185b">

Countries with low Polity2 scores indicating autocratic governance often face recurring conflicts due to their low GDP income levels leading to heightened civil unrest. The diversion of public resources exacerbates these conflicts making these nations vulnerable to insurgent groups. This necessitates substantial military spending to suppress the uprisings resulting in a decline in national well-being. Additionally, it can be observed that countries with limited food supplies also tend to allocate more funds to their military.

### Emergency Food Aid by Onset of War

<img width="720" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/f86569cc-044d-4641-9a09-ae043615880b">


### Emergency Food Aid by Overall Conflict

<img width="720" alt="2" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/724bd415-7694-4245-b07b-197834c838b0">

The kernel density plot analysis reveals insights into the connection between emergency food assistance and armed conflict dynamics in SSA. Clustering of aid in specific SSA areas indicates vulnerability to food insecurity and associated socio-economic challenges, emphasising targeted humanitarian interventions. Moreover, as aid surpasses a threshold, the likelihood of conflict escalation increases suggesting a failure to address underlying conflict causes despite receiving food aid relief. Overlapping density curves for "Yes" and "No" conflict and onset of war categories imply complex conflict dynamics, with neighbouring regions experiencing similar aid levels exhibiting varying conflict degrees. Uneven aid allocation with some regions receiving more aid than others may heighten conflict risks emphasising the need for fairer aid distribution to mitigate conflicts.

### Battle Death by Emergency Food Aid

<img width="720" alt="4" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/b39453ad-727c-4d93-a944-51fe10c859b7">

Regardless of the quantity of emergency food assistance provided, conflicts and wars remain an inevitability. It can be seen that humanitarian aid tends to perpetuate rather than resolve conflicts in the SSA regions. Moreover, the severity of casualties resulting from such conflicts worsens when the received food aid is insufficient prompting nations to engage in warfare to secure limited emergency food supplies.

### Number of Battle Deaths by Country

![12](https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/48306fba-bf4d-42b3-833b-b34175dc3671)

To understand the resource-related conflicts, it is noteworthy to observe that a considerable proportion of casualties arising from armed confrontations take place in nations characterised by authoritarian governance. Among the 11 nations with the highest documented battle fatalities, a noteworthy eight belong to the category of authoritarian regimes. These nations encompass Liberia, Côte d’Ivoire, Chad, Sudan, Uganda, Somalia, Rwanda and Angola.

## Conclusion

The analysis SSA countries from 2002 to 2020 uncovers how food aid, though well-intentioned, can unintentionally exacerbate conflicts. Key findings shed light on these complex dynamics:

Firstly, many SSA nations such as Eswatini, Eritrea, Gambia, Mauritania, Togo, Chad, Uganda, Ethiopia, Sudan, Angola, Zimbabwe and Rwanda are governed by autocratic regimes. These regimes limit political freedoms, potentially discouraging emigration.

Secondly, countries with lower Polity2 scores experience slower GDP growth. This discourages emigration and deters investors. In contrast, democratically governed nations enjoy stability, attracting investment and fostering economic growth.

Thirdly, nations with lower Polity2 scores often become trapped in cycles of conflict exacerbated by minimal GDP income levels. Their economies are further strained as they allocate a significant portion of their budgets to military expenditure.

Moreover, emergency food aid allocation reveals disparities with certain regions receiving more assistance than others. Surprisingly, higher food aid levels can exacerbate conflicts especially where nation leaders manipulate distribution to maintain control. The kernel density plot underscores the intricate relationship between emergency food aid and conflict dynamics highlighting clusters of aid in vulnerable regions.

Additionally, when food aid surpasses a certain threshold, conflict escalation likelihood increases suggesting that addressing food insecurity alone may not suffice. Uneven aid allocation heightens conflict risks in resource-limited regions necessitating fairer distribution strategies. In essence, autocratic governance creates an environment where aid access equates to economic and political power to exploit humanitarian assistance. Thereby, sparking disputes and internal conflicts.






