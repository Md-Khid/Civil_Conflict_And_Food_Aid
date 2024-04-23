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
<img width="681" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/617f321a-327a-46e3-a469-11fb6de24f2c">


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
<img width="824" alt="2" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/5e93efdd-de35-457f-a7bb-45b3a457c34a">

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
<img width="1124" alt="3" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/c8c8d84e-1485-4d43-990d-484ac231fe4c">


#### Extract the Year from the ‘year’ Column for Data Merging 

```
# Extract the first four characters from the 'year' column and create a new column called 'year'
df <- df %>%
  mutate(year = substr(year, 1, 4))
```
<img width="668" alt="4" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/23ccd993-039c-4d5c-b35c-e09a96b78103">

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
<img width="664" alt="5" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/07091986-c867-4cbf-bfc7-3e16a0300859">

### e.	Merging Data
The country names in the World Development Indicators (WDI) dataset will be renamed to match the names in the existing dataset to ensure accurate country identification. Numerical values such as ‘2002’ will be extracted from the ‘year’ column in the existing dataset and converted into integers for standardisation. Both datasets will be merged using the ‘country’ and ‘year’ columns as the basis for identification.

#### Data Transformation for Merging WDI Data
```
# Rename specific countries in the dataset to match common naming conventions
wdi_data <- wdi_data %>%
  mutate(
    country = case_when(
      country == "Congo, Rep." ~ "Congo",  # Change "Congo, Rep." to "Congo"
      country == "Congo, Dem. Rep." ~ "Democratic Republic of the Congo",  # Change "Congo, Dem. Rep." to "Democratic Republic of the Congo"
      country == "Gambia, The" ~ "Gambia",  # Change "Gambia, The" to "Gambia"
      TRUE ~ country  # Keep other values unchanged
    )
  )
```
#### Convert the 'year' Column in the 'df' DataFrame to Integer and Perform Data Merging
```
# Convert the 'year' column in dataframe 'df' to integer type
df$year <- as.integer(df$year)

# Merge dataframe 'df' with dataframe 'wdi_data' based on the common columns 'country' and 'year', storing the result in dataframe 'df2'
df2 <- left_join(df, wdi_data, by = c("country", "year"))

# Write the merged dataframe 'df2' to a CSV file named 'df2.csv', excluding row names
write.csv(df2, file = "df2.csv", row.names = FALSE)

# Display the first few rows of the merged dataframe 'df2'
head(df2)
```

<img width="686" alt="5" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/a7e98a28-7bbe-4829-b323-c5cf298cd016">

#### Rename variables
```
# Renaming columns in dataframe df2 using the pipe operator %>%
df2 <- df2 %>%
  rename(
    "Military Expenditure" = MS.MIL.XPND.CD, # Renaming column MS.MIL.XPND.CD to "Military Expenditure"
    "Prevalence of Undernourishment" = SN.ITK.DEFC.ZS # Renaming column SN.ITK.DEFC.ZS to "Prevalence of Undernourishment"
  )
```
<img width="684" alt="6" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/eceb2413-1e28-4ded-a116-b3b01d81667b">

### f.	Missing Values
To ensure a consistent data flow and prevent the generation of visualisation chart errors, missing values will be replaced with ‘NA’ to maintain the integrity of the merged dataset, making it more suitable for analysis and interpretation. Therefore, it is important to consider the following variables, each of which has more than 100 missing rows, during the exploratory data analysis phase:
•	onsetwar (126 missing)
•	offsetwar (126 missing)
•	battle_deaths (126 missing)
•	civilian_deaths (126 missing)
•	Armed Forces Personnel (128 missing)
•	Prevalence of Undernourishment (190 missing)

#### Check for Missing Values
```
# Calculate the count of missing values for each column in df2
df2.missingcounts <- colSums(is.na(df2))

# Filter columns where the count of missing values is greater than 100
df2.missingcounts[df2.missingcounts > 100] # not more than 100 data rows
```
<img width="557" alt="7" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/9f573c9e-539b-42c6-952c-727fbdf4bd3e">

#### Create and Store Country Locations
```
# Create a data frame with coordinates for multiple countries
Coordinates <- data.frame(
  Country = c("Angola", "Benin", "Burkina Faso", "Burundi", "Cape Verde", "Cameroon", 
              "Central African Republic", "Chad", "Comoros", "Republic of the Congo", 
              "Côte d'Ivoire", "Djibouti", "Eritrea", "Eswatini", "Ethiopia", "Gambia", 
              "Ghana", "Guinea", "Guinea-Bissau", "Kenya", "Lesotho", "Liberia",
              "Madagascar", "Malawi", "Mali", "Mauritania", "Mozambique", "Namibia",
              "Niger", "Nigeria", "Rwanda", "Senegal", "Sierra Leone", "Somalia",
              "South Africa", "Sudan", "Tanzania", "Togo", "Uganda", "Zambia", "Zimbabwe",
              "Democratic Republic of the Congo"),
  Longitude = c(17.873887, 2.315834, -1.561593, 29.918886, -24.013197, 12.639232, 
                21.640959, 18.731186, 43.261206, 15.827659, -5.54708, 42.590275, 
                38.84683, 31.4659, 39.782334, -15.439505, -0.10599, -1.027727,  -15.6538,
                37.9062, 28.2336, -9.4295, 46.869107, 34.3015, -3.9962, 20.2559, 35.5296, 
                18.6657, 8.0817, 7.4951, 29.8739, 14.4974, -11.7922, 45.3435, -28.816623,
                30.217636, 34.8888, 1.2126, 32.2903, 27.8493, 29.1549, -4.0383),
  Latitude = c(-11.202692, 9.30769, 12.238333, -3.373056, 16.5388, 5.96607, 6.573778, 
               15.454166, -11.6455, -0.228021, 7.539988, 11.748718, 15.179384, -26.5225, 
               9.145, 13.443182, 13.443182, 7.257472, 11.8037, -1.2921, -29.609, 6.4281, 
               -18.8792, -13.2543, 17.5707, 20.3487, -18.6657, -22.9576, 17.6078, 9.0820, 
               -1.9403, 14.4974, 8.5636, 5.1521, -25.746111, 15.7887, -6.369028, 8.7808, 
               1.3733, -13.1339, -17.8252, -4.0383)
)

# Print the Coordinates data frame
print(Coordinates)
```
<img width="698" alt="8" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/89bb55e8-7d00-4aaa-9f6d-22d41b15088c">

## Data Findings

The scatter plot presents data on the Polity2 scores of countries in Sub-Saharan Africa. Notably, countries including Eswatini, Eritrea, Gambia, Mauritania, Togo, Chad, Uganda, Ethiopia, Sudan, Angola, Zimbabwe and Rwanda have maintained autocratic forms of government from 2002 to 2020. These nations appear to have continued to embrace autocratic leadership, which heavily influences the lives of their citizens. It is plausible that these countries are governed by one-party systems or military juntas, allowing their leaders to steadily consolidate power. As a result, adjustments in their legal frameworks have been made to restrict political freedoms and human rights, creating a false appearance of legitimacy for autocratic rule. This type of autocratic governance may have imposed hardships on the citizens and limited opportunities for emigration from these nations. Various factors, such as economic constraints, fear of potential repercussions, strong social and familial ties, limited access to unbiased information, strict immigration policies and aversion to risk could contribute to discouraging migration.

#### Polity2 vs Population
```
# Filter df2 for the year 2002
df2_2002 <- df2 %>% filter(year == 2002)

# Filter df2 for the year 2020
df2_2020 <- df2 %>% filter(year == 2020)

# Determine the y-axis limits based on both 2002 and 2020 data
y_axis_limits <- range(df2_2002$population / 1e6, df2_2020$population / 1e6)

# Create the scatter plot for year 2002 with labels for countries with polity2 values from 0 to -10
scatterplot_2002 <- ggplot(data = df2_2002, aes(x = polity2, y = population / 1e6, label = country)) +
  geom_point() +
  labs(x = "Polity2", y = "Population (in millions)") +
  ggtitle("Year 2002") +
  geom_text_repel(
    aes(x = polity2, y = population / 1e6),
    data = df2_2002 %>% filter(polity2 >= -10 & polity2 <= 0),
    size = 2,
    box.padding = 0.5
  ) +
  scale_y_continuous(labels = comma_format(), limits = y_axis_limits)  # Set y-axis limits

# Create the scatter plot for year 2020 with labels for countries with polity2 values from 0 to -10
scatterplot_2020 <- ggplot(data = df2_2020, aes(x = polity2, y = population / 1e6, label = country)) +
  geom_point(aes(color = ifelse(polity2 >= -10 & polity2 <= 0, "Highlighted", "Other")),
             size = 2) +
  labs(x = "Polity2", y = "Population (in millions)") +
  ggtitle("Year 2020") +
  geom_text_repel(
    aes(x = polity2, y = population / 1e6),
    data = df2_2020 %>% filter(polity2 >= -10 & polity2 <= 0),
    size = 2,
    box.padding = 0.5
  ) +
  scale_color_manual(values = c("Highlighted" = "red", "Other" = "black")) +
  theme(legend.position = "none") 

# Print the scatter plots separately for year 2002 and 2020
print(scatterplot_2002)
print(scatterplot_2020)
```
#### Yr.2002
<img width="524" alt="9" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/1929b2c4-5475-48f1-b2d2-c05e26535803">

#### Yr.2020

<img width="525" alt="10" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/231f2f84-c073-4adc-873d-94d9ab4a035b">

Over the years, countries with lower Polity2 scores (ranging from -10 to 0) have consistently experienced slower GDP growth between 2002 and 2020. On the other hand, nations with higher Polity2 scores (ranging from 0 to 10) have seen stronger GDP growth. This difference in economic performance may be because countries with lower scores have limited political freedom and transparency. This can discourage people from leaving these countries and make it less attractive for investors to do business there due to the unfavourable political climate. In contrast, countries with democratic governments tend to have more stable political systems and a better environment for business. This attracts more business owners and investors, ultimately boosting the economy and leading to stronger GDP growth. Another potential explanation for the variations in GDP growth among countries with lower Polity2 scores may be linked to increased income inequality, possibly stemming from progressive tax policies. Notably, increased economic freedom tends to result in reduced taxation and relaxation of regulations.
