# QSS 20 Final Project README (Maeve Padien)
### Analyzing the economic impact of hosting the World Cup on poor, urban households
##### *This is only my intital README from 8/18. It will be changed and updated as I continue to work on and refine my final project*

## Project Description
FIFA promotes the World Cup as an opportunity to alleviate poverty, bring tourism, and solve economic problems. Underneath that claim  is an idea that a spurt of growth and tourism across a very brief time permanently due to the tournament helps poor households in the country. This project tests FIFA's claim. It asks if hosting the World Cup promotes development, if it supports poor households in the country, and if any changes are lasting. It considers if hosting exacerbates exisiting issues of inequality and poverty. This project also uses a particular definition of development. It centers on individuals and their experience in poverty. Development cannot just mean GDP growth, it must include an assessment of the living conditions and experiences of the poorest households. In this project, I look at two cases, the 2010 tournament in South Africa, and the 2014 tournament in Brazil. In particular, in each country I look at host and non-host cities to compare changes in economic outcomes. I use three different years for each tournament to address my temporal question.

#### Data Used
For this project, I use continous national household surveys conduct by the government of Brazil and South Africa. PNAD Contínua is Brazil's survey, and I use data from 2012, 2014, and 2016. For South Africa, I use the Quarterly Labour Force Survey (QLFS) for the final quarter of 2008, 2010, and 2012. All of this data is open access through each country's respective statistics agency.

#### Data Access
The South Africa data can be downloaded from the Department of Statistics of South Africa website. The University of Cape Town operates the DataFirst platform which organizes the raw Stata files from South Africa, and users can directly download those files by selecting the appropriate year, as I did. Here is the link to the DataFirst site: https://www.datafirst.uct.ac.za/dataportal/index.php/catalog/214

The Brazil data is downloaded via the website SIDRA which is hosted by the government agency in charge of the household survey. To get each table, a user goes to the site and selects the variables, time period, and locations desired. Since this is a more particular process, the xlsx that process produced also exists in this repo, in the data folder. If interested, here is the link to the SIDRA site: https://sidra.ibge.gov.br. Select the PNAD tab, then the tiny list button on the header, and select the tables required. (4093, 5947, 6371, 5439)

## Overview of Notebooks
##### The notebooks below walk through exactly how I produced my results. They are intended to run in order, beginning with 00_pull. In this README file, each notebook is listed and explains what inputs it takes in, the output produced, and the general method behind the coding. Order: 00_pull, 01_clean, 02_analysis

### 00_pull
##### This notebook takes in all of the raw data files (as explained above), and then stacks all of the South Africa data into one DataFrame. It also standarizes naming inconsistencies across years. For Brazil, since all of the variables are different, the notebook leaves them as seperate files. However, it translates the information from Portugese to English, and removes header and source rows. Since this is a repeatative process done four seperate times, the notebook uses a function to execute. Once those changes are made, it saves the intermediate data files described below.

##### **Input**
data/southafrica_2008.dta, data/southafrica_2010.dta, data/southafrica_2012.dta
data/brazil_4092.xlsx, data/brazil_5947.xlsx, data/brazil_6371.xlsx, data/brazil_5439.xlsx

##### **Output**
data/southafrica_all.dta
data/brazil_lstatus.csv, data/brazil_socialsecurity.csv, data/brazil_hours.csv, data/brazil_income.csv

### 01_clean
##### This notebook takes in the intermediate data files from 00_pull and produces the calculated variables required for the analysis. It also standarizes city names across datasets as the national survey altered them each year. It then creates a flag variable to tag each location as a host or non host. Then, it reduces the Brazilan dataset to only three host and nonhost regions (6 total) in order to be able to better compare (matched roughly on population). Finally, it computes Brazil's informal employment rate via the social security table. It does that by saying informal employment is equal to employees who pay social security divided by all employed. All formal employees must pay social security, so this can be used similary to the South Africa variable on informality.

##### ***Input***
data/southafrica_all.dta
data/brazil_lstatus.csv, data/brazil_socialsecurity.csv, data/brazil_hours.csv, data/brazil_income.csv

##### ***Output***
data/southafrica_analysis.dta
data/brazil_socialsecurity_analysis.csv, data/brazil_hours_analysis.csv, data/brazil_income_analysis.csv

### 02_analysis
#### This notebook takes in the intermediate data files from the 01_clean notebook. It then computes the informal employment rates by year and host status for both Brazil and South Africa. It then disaggregates that rate to consider per-city changes to informal employment from two years after the tournament from two years before. It then looks specifically at Johannesburg and calculates the informal employment rate over time there by both gender and then sector (i.e. construction, retail). Finally, it produces the four figures based on those calculations.

##### ***Input***
data/southafrica_analysis.dta
data/brazil_socialsecurity_analysis.csv, data/brazil_hours_analysis.csv, data/brazil_income_analysis.csv

##### ***Output***
fig1_informality_aggregate.png, fig2_informality_disaggregate.png, fig3_johannesburg_gender.png, fig4_johannesburg_sectors.png
