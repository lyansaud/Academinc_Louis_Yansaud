+++
# Date this page was created.
date = 2016-04-27T00:00:00

# Project title.
title = "Homeless Geospatial Visualization Dashboard with Shiny"

# Project summary to display on homepage.
summary = "This online geospatial visualization mapping tool helped us evaluate the effectiveness of existing and potential homelessness interventions."

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "homeless_la.jpg"


# Tags: can be used for filtering projects.
# Example: `tags = ["Optimization"]`
tags = ["Geospatial Visualization"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to static/img/ folder).
[header] 
  image = "homeless_la2.png"

# Call to action button (optional).
#   Activate the button by specifying a URL and button label below.
#   Deactivate by commenting out parameters, prefixing lines with `#`.
[cta]
  url = "https://drive.google.com/open?id=1elzuswEmnR90O2PtxWdz5sA6r9LwuAKa"
  label = '<i class="fa fa-download"></i> Download the full report here'
  
+++

##### Introduction

Homelessness is soaring in Los Angeles and is a severe issue that is a part of everyday life. 
Our objective for this project:

- Determining the need, demand and potential effects of different strategies for homeless intervention.
- Identifying the areas with high-concentrations of unsheltered homelessness, crime incidents and high danger areas for the homeless community in order to help address the homelessness in full scope, while prioritizing service delivery needs

In order to gain insight on homelessness:

- We cleaned the data and used geospatial analysis to create an online mapping application. 
- This online mapping tool helped us evaluate the effectiveness of existing and potential homelessness interventions, functioned as a framework to determine fast delivery alternatives as well as helping us analyze data in full-scope and allow the rapid deployment of resources and services. 


<img src="/project/data_analysis_homeless.png" width="672" />

##### Shiny Application

<img src="/project/homeless_shiny2.png" width="672" />

The Interactive Map displays the city of Los Angeles and its homeless population in an interactive map. The collapsable Map Controls drop down has the following features:

- Change the homeless measure distribution by either Census Tract or Communities
- Filter the homeless population by year and measure
- Filter the Crime counts and locations by time of day, day of the week, and month of the year
- Filter the Call counts and locations by time of day, day of the week, and month of the year
- Note that the 24 hour day has been split into 4 buckets:
  - Morning: 12:00 AM to 6:00 AM
  - Afternoon: 6:00 AM to 12:00 PM
  - Evening: 12:00 PM to 6:00 PM
  - Night: 6:00 PM to 12:00 AM
- As well, above the legend in the bottom right corner, the user can select the different layers to display: Homeless Measure, Shelters, Crimes, and/or 311 calls.

<img src="/project/homeless_shiny.png" width="672" />

The Crimes and Calls tab displays a plot of the distribution of 311 calls or crime counts across the week and then also buckets them into the time of day following the above mentioned splits. Crimes can be further filtered based on the type of crime from the drop down menu on the left. The Homeless Comparison tab displays the 2017 and 2016 homeless measures side by side to give a quick visual clue into the year over year homeless distribution change across the city of Los Angeles. Similar to the interactive map, the plot can be changed between viewing census tracts or communities. In addition, the same homeless measure filters can be applied, such as viewing the Total Homeless or Total Unsheltered distributions.

##### Conclusion and Key Findings

- We analyzed and visualized the trend of homelessness and associated crimes with the merged dataset by census tract: 
- We then Calculated the correlation between the homeless density and 311 calls
  - We observed a high correlation between density and crimes counts which raised the question that whether high crime rates were a threat to the homeless population or were the homeless causing these crimes
- Analyzed the distribution of crimes and 311 calls across time
  - Number of 311 calls was the highest on Tuesday and during the afternoon hours
  - Crime rate is highest on Saturday afternoon, followed by Tuesday evening and Sunday afternoon and evening.
  - The most frequent type of crime is Assault on Saturday afternoon
  
- Used our Shiny Dashboard to understand which factors could be significant for the unsheltered homeless.
Skid row being at the top even though it has the largest number of shelter counts. Worth noting that calls coming from that area are comparatively quite low and it experiences high crime counts as well. 

##### Recommendations:

- Investigate and access to homeless satisfaction in shelters
- Analyze average age of homeless in shelters to estimate the average age of the total homeless population per census tract. By doing so, we can have then use this data to implement better strategies and procedures to help homelessness.
- Collect more data from successful project to support the decreasing rate of unsheltered homeless.


<a href="https://drive.google.com/open?id=1kcoOuE3aUxqVuvuqiLqzP1tGT6rm5nnk" download>Click to Download the full presentation</a>
