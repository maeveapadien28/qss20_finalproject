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
##### The notebooks below walk through exactly how I produced my results. They are intended to run in order, beginning with 00_pull. In this README file, each notebook is listed and explains what inputs it takes in, the output produced, and the general method behind the coding.

#### 00_pull_clean
This notebook takes in raw data from each household survey. These files are downloaded directly from the DataFirst and SIDRA website as explained above. For South Africa, the notebook creates a new variable, a boolean "is_metro", and then keeps only the relevent columns for the rest of the project. That cleaned file is then saved as the output. For Brazil, since the data is in Portugese, I create new columns names in English, load the data, and create the same boolean as above. The datatable also has these footnotes that are irrelevent, so I drop them. I then save that cleaned file as the secondary output of this notebook.

#### 01_analysis
This notebook takes in the cleaned South Africa data from the 00_pull_clean notebook. It then computes informal and unemployment rates for host and non-host regions in South Africa by using the lamda function to apply a boolean operator and mean function. It then creates two bar charts (contained in one plot) of informal and unemployment rates for the two categories. That chart is the output of this notebook.
