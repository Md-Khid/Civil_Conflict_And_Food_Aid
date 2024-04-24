  # Project Overview

## Introduction

This study explores the complex link between civil conflicts in Sub-Saharan Africa (SSA) and emergency food aid distribution. SSA with its diverse geography and socio-political dynamics, experiences recurrent conflicts driven by factors like grievances, wealth disparities and food insecurity. Food scarcity worsens conditions for conflict and hampers conflict resolution and recovery. This study aims to uncover the intricate interactions between emergency food aid and civil conflict in SSA using data from 2002 to 2020. Visualisation techniques will be used to gain insights into this relationship.

## Data Dictionary

The dataset studied covers SSA countries from 2002 to 2020, comprising 54 countries with various variables on conflicts, disasters, economy and politics. Below table lists the dataset variables with brief descriptions.

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

As per the data [dictionary](#data-dictionary), some variables represent combined totals of distinct variables. Hence, it's crucial to consider:

i. "overall_conflict" equals "minor_conflict" and "major_conflict."

ii. "Total_affected_disasters" equals "affected_disasters" and "homeless_disasters."

iii. "Total_affected_othercountries" equals "total_affected_neighbours", "total_affected_non_neighbours" and "nda_other_region."

As using these variable sets simultaneously in data exploration may hinder accurate visualisation.


### b.  Data Structure

Converting the dataset to an R data frame yields 798 observations with 25 variables. Analysis shows most variables are numeric, except "country" noted as a character variable and "year" formatted as date and time.

#### Data Types
```
# Provide summary of data structure
str(df)
```

<img width="491" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/f1ea89ea-fa0a-4e44-ade6-27649935320b">

### c.  Data Transformation

To make visualisation charts for the study, the study will:

i. Convert numeric variables ('overall_conflict', 'minor_conflict', 'major_conflict', 'onsetwar', 'offsetwar' and 'polity2') into categories.

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

ii. Create new variables: "total_food_aid" (sum of emergency_food_aid and non_emergency_food_aid), "percent_total_food_aid_of_total_aid" (total_food_aid divided by total_aid) and "total_gdp" (gdp_per_capita multiplied by population).

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

More data from the World Development Indicators (WDI) will be added to the current dataset focusing on SSA region stats like ‘MS.MIL.XPND.CD’ (Military Expenses) and ‘SN.ITK.DEFC.ZS’ (Prevalence of Undernourishment). Looking at military spending gives insights on security and checking undernourishment levels is crucial for food security which affects civil unrest potential.

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

The World Development Indicators (WDI) dataset will have country names aligned with the existing dataset for accurate identification. Years from the 'year' column in the existing dataset will be converted to integers for standardisation. Both datasets will be merged based on 'country' and 'year' columns.

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

To maintain data integrity and avoid visualisation errors, missing values will be replaced with 'NA' in the merged dataset. This ensures consistency for analysis. Key variables with over 100 missing rows include: 

•	onsetwar (126 missing)

•	offsetwar (126 missing)

•	battle_deaths (126 missing)

•	civilian_deaths (126 missing) 

•	Military Expenditure (128 missing)

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

### Polity2 vs Population
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

The scatter plot depicts SSA countries' Polity2 scores. It can be observed that Eswatini, Eritrea, Gambia, Mauritania, Togo, Chad, Uganda, Ethiopia, Sudan, Angola, Zimbabwe and Rwanda have maintained autocratic governments from 2002 to 2020. These nations might be governed by one-party systems or military rule possibly restricting political freedoms and human rights. The limited emigration from these nations could also be due to hardships, economic constraints, fear, strict immigration policies and risk aversion.

### Polity2 vs Total GDP
```
# Create a scatter plot for polity2 vs. total_gdp in millions of USD
scatter_plotGDP <- ggplot(data = df2, aes(x = polity2, y = total_gdp / 1e6)) +  # Divide by 1e6 to convert to millions
  geom_point(aes(color = ifelse(polity2 >= -10 & polity2 <= 0, "Highlighted", "Other")), size = 2) +  # Highlight condition and reduce point size
  labs(x = "Polity2", y = "Total GDP (Millions USD)") +  
  ggtitle("") +
  scale_y_continuous(labels = scales::comma_format(scale = 1e-6)) +  # Format y-axis labels in millions
  scale_color_manual(values = c("Highlighted" = "red", "Other" = "black"))+
  theme(legend.position = "none") 

# Print the scatter plot
print(scatter_plotGDP)
```
<img width="524" alt="11" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/09536caf-82ba-42f7-b92d-b79192860511">

Countries with lower Polity2 scores (-10 to 0) experienced slower GDP growth from 2002 to 2020, while nations with higher scores (0 to 10) saw stronger growth. This difference may stem from limited political freedom and transparency in lower-scoring countries, discouraging people and investors. Democratic nations tend to offer more stable political climates, attracting investment and boosting GDP.

### Military Expenditure by Country
```
# Calculate the mean Military Expenditure by country and arrange in descending order
df2_mean <- df2 %>%
  group_by(country) %>%
  summarize(mean_afp = mean(`Military Expenditure`, na.rm = TRUE)) %>%
  arrange(desc(mean_afp))

# Filter out rows with NA in polity2_category
df2_filtered <- df2 %>%
  filter(!is.na(polity2_category))

# Create a box plot with fill based on polity2_category
box_plot <- ggplot(data = df2_filtered, aes(x = factor(country, levels = df2_mean$country), 
                                           y = `Military Expenditure` / 1e9,  # Convert to USD billion
                                           fill = polity2_category)) +
  geom_boxplot() +
  labs(x = "Country", y = "Military Expenditure (USD billion)") +  
  ggtitle("") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +  
  labs(fill = "")

# Print the box plot
print(box_plot)
```
<img width="720" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/61d2c03c-774c-48ab-9f7c-5345abd8185b">

Countries with low Polity2 scores, indicating autocratic governance often face recurring conflicts due to their low GDP income levels leading to heightened civil unrest. The diversion of public resources exacerbates these conflicts making these nations vulnerable to insurgent groups. This necessitates substantial military spending to suppress the uprisings resulting in a decline in national well-being. Additionally, it can be observed that countries with limited food supplies also tend to allocate more funds to their military.

### Emergency Food Aid by Onset of War

```
# Filter out NA values in the "onsetwar" variable
df2_filtered <- df2[!is.na(df2$onsetwar), ]

# Create a kernel density plot with a log-scale x-axis
kernel_density_plot <- ggplot(df2_filtered, aes(x = emergency_food_aid, fill = onsetwar)) +
  geom_density(alpha = 0.5) +  # Add a semi-transparent density plot
  labs(x = "Emergency Food Aid", y = "Density") +  # Set axis labels
  ggtitle("") +  # Set plot title
  scale_fill_manual(values = c("Yes" = "red", "No" = "blue")) +  # Define colors
  theme_minimal() + 
  scale_x_log10()  # Set x-axis to log scale

# Print the kernel density plot
print(kernel_density_plot)
```

<img width="720" alt="1" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/f86569cc-044d-4641-9a09-ae043615880b">


### Emergency Food Aid by Overall Conflict

```
# Filter out NA values in the "onsetwar" variable
df2_filtered <- df2[!is.na(df2$overall_conflict), ]

# Create a kernel density plot with a logarithmic x-axis scale
kernel_density_plot <- ggplot(df2_filtered, aes(x = emergency_food_aid, fill = overall_conflict)) +
  geom_density(alpha = 0.5) +  # Add a semi-transparent density plot
  labs(x = "Emergency Food Aid", y = "Density") +  # Set axis labels
  ggtitle("") +  # Set plot title
  scale_fill_manual(values = c("Yes" = "red", "No" = "blue")) +  # Define colors
  theme_minimal() + 
  scale_x_log10()  # Set x-axis to log scale

# Print the kernel density plot
print(kernel_density_plot)
```
<img width="720" alt="2" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/724bd415-7694-4245-b07b-197834c838b0">

The kernel density plot analysis reveals insights into the connection between emergency food assistance and armed conflict dynamics in SSA. Clustering of aid in specific SSA areas indicates vulnerability to food insecurity and associated socio-economic challenges, emphasising targeted humanitarian interventions. Moreover, as aid surpasses a threshold, the likelihood of conflict escalation increases suggesting a failure to address underlying conflict causes despite receiving food aid relief. Overlapping density curves for "Yes" and "No" conflict and onset of war categories imply complex conflict dynamics, with neighbouring regions experiencing similar aid levels exhibiting varying conflict degrees. Uneven aid allocation with some regions receiving more aid than others may heighten conflict risks, emphasising the need for fairer aid distribution to mitigate conflicts.

### Battle Death by Emergency Food Aid

```
# Filter out NA values in the "battle_deaths" and "emergency_food_aid" variables
df2_filtered <- df2 %>%
  filter(!is.na(battle_deaths) & !is.na(emergency_food_aid))

# Create a scatter plot with logarithmic x-axis scale and fill points based on "polity2_category"
correlation_plot <- ggplot(df2_filtered, aes(x = log(battle_deaths), y = emergency_food_aid, fill = polity2_category)) +
  geom_point(shape = 21, size = 3, data = . %>% filter(log(battle_deaths) != 0)) +  # Add scatter points with custom shape and size, excluding x=0 points
  
  labs(x = "Log(Battle Deaths)", y = "Emergency Food Aid") +  # Set axis labels
  ggtitle("") +  
  theme_minimal() +  
  scale_fill_manual(values = c("Highly Autocratic" = "red", "Moderately Autocratic" = "pink",
                               "Neutral/Transitional" = "grey", "Moderately Democratic" = "lightblue", 
                               "Highly Democratic" = "blue")) + 
  guides(fill = guide_legend(title = "Polity2 Category")) +  
  geom_rect(xmin = 3, xmax = 8, ymin = 0, ymax = 200,
            fill = "transparent", color = "blue", alpha = 0)  # Add transparent box

# Print the correlation plot
print(correlation_plot)
```
<img width="720" alt="4" src="https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/b39453ad-727c-4d93-a944-51fe10c859b7">

Regardless of the quantity of emergency food assistance provided, conflicts and wars remain an inevitability. It can be seen that humanitarian aid tends to perpetuate rather than resolve conflicts in the SSA regions. Moreover, the severity of casualties resulting from such conflicts worsens when the received food aid is insufficient prompting nations to engage in warfare to secure limited emergency food supplies. These conflicts often involve autocratic countries competing with other nations, rebel leaders or supporters for control over food distribution.

### Number of Battle Deaths by Country
```
# Filter df2 for the year 2002
df2_2002 <- df2[df2$year == 2002, ]

# Create a basic map with a default view
map <- leaflet() %>%
  setView(lng = 12, lat = -8, zoom = 5) %>%
  addTiles()

# Define marker options for smaller markers
small_marker_options <- markerOptions(radius = 3, fillOpacity = 0.7)

# Iterate through the Coordinates dataset and add markers and labels for each country
for (i in 1:nrow(Coordinates)) {
  country_name <- Coordinates$Country[i]
  country_lng <- Coordinates$Longitude[i]
  country_lat <- Coordinates$Latitude[i]
  
  # Filter df2 for the specific country and year
  df2_country <- df2_2002 %>%
    filter(country == country_name)
  
  # Calculate the total battle deaths for the country
  total_battle_deaths <- sum(df2_country$battle_deaths, na.rm = TRUE)
  
  # Check if battle deaths should be hidden
  if (!is.na(total_battle_deaths) && total_battle_deaths > 1) {
    
    # Check if the country's polity2 value is within the range of 0 to -10
    polity2_value <- df2_country$polity2[1]  # Assuming it's the same for all rows of the same country in 2002
    if (!is.na(polity2_value) && polity2_value >= -10 && polity2_value <= 0) {
      # Add a marker with custom color for countries in the specified polity2 range
      map <- map %>%
        addCircleMarkers(
          lng = country_lng,
          lat = country_lat,
          radius = 10,  # Adjust the marker size
          color = "red",  # You can customize the marker color here
          fillOpacity = 0.7
        )
    } else {
      # Add a smaller marker for countries outside the specified polity2 range
      map <- map %>%
        addCircleMarkers(
          lng = country_lng,
          lat = country_lat,
          color = "blue",  # You can customize the marker color here
          options = small_marker_options  # Use the smaller marker options
        )
    }
    
    # Add a label for the country with total battle deaths information displayed permanently (rounded to whole numbers)
    label_text <- paste(country_name, ":", total_battle_deaths)
    
    map <- map %>%
      addLabelOnlyMarkers(
        lng = country_lng,
        lat = country_lat,
        label = label_text,
        labelOptions = labelOptions(noHide = TRUE, direction = "auto")
      )
    
  }
}

# Display the map
map
```
![12](https://github.com/Md-Khid/Civil_Conflict_And_Food_Aid/assets/160820522/48306fba-bf4d-42b3-833b-b34175dc3671)

To understand the resource-related conflicts, it is noteworthy to observe that a considerable proportion of casualties arising from armed confrontations take place in nations characterised by authoritarian governance. Among the 11 nations with the highest documented battle fatalities, a noteworthy eight belong to the category of authoritarian regimes. These nations encompass Liberia, Côte d’Ivoire, Chad, Sudan, Uganda, Somalia, Rwanda and Angola. In these particular countries, populations have frequently endured protracted periods of political oppression and violence as autocratic leaders within these nations may resort to coercive measures to sustain their control over the populace.

## Conclusion

The analysis SSA countries from 2002 to 2020 uncovers how food aid, though well-intentioned, can unintentionally exacerbate conflicts. Key findings shed light on these complex dynamics:

Firstly, many SSA nations such as Eswatini, Eritrea, Gambia, Mauritania, Togo, Chad, Uganda, Ethiopia, Sudan, Angola, Zimbabwe and Rwanda are governed by autocratic regimes. These regimes limit political freedoms, potentially discouraging emigration.

Secondly, countries with lower Polity2 scores experience slower GDP growth. This discourages emigration and deters investors. In contrast, democratically governed nations enjoy stability, attracting investment and fostering economic growth.

Thirdly, nations with lower Polity2 scores often become trapped in cycles of conflict exacerbated by minimal GDP income levels. Their economies are further strained as they allocate a significant portion of their budgets to military expenditure.

Moreover, emergency food aid allocation reveals disparities with certain regions receiving more assistance than others. Surprisingly, higher food aid levels can exacerbate conflicts especially where nation leaders manipulate distribution to maintain control. The kernel density plot underscores the intricate relationship between emergency food aid and conflict dynamics highlighting clusters of aid in vulnerable regions.

Additionally, when food aid surpasses a certain threshold, conflict escalation likelihood increases suggesting that addressing food insecurity alone may not suffice. Uneven aid allocation heightens conflict risks in resource-limited regions necessitating fairer distribution strategies. In essence, autocratic governance creates an environment where aid access equates to economic and political power to exploit humanitarian assistance. Thereby, sparking disputes and internal conflicts.

To address food insecurity, a comprehensive approach is imperative. Initiatives should prioritise good governance, political freedom and economic stability to break the cycle of conflict and ensure equitable resource distribution. As such, comprehensive strategies addressing root causes are crucial to minimising conflicts in the SSA region.






