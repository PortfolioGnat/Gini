# Gini
___
# Gini Coefficient Dataset
Below you will find different examples of visualizations that pull from a dataset called Gini. But...What is the Gini Coefficient?\
In economics, the [Gini Coefficient](https://en.wikipedia.org/wiki/Gini_coefficient), also known as the Gini Index or Gini Ratio, measures income, wealth, or consumption inequality within a particular nation or social group.

# **Visualization 1: Initial Attempt**
![Visualization 1](/gini1.png)

## The image shows the Gini coefficient at a certain numerical year. It has also been color-coded based on whether or not it is the USA or "Other Countries".

I decided to create a scatterplot as it shows the Gini coefficient in the USA comparatively to the rest of the world. For the USA, wealth inequality started lower and then rose by about 10%.\
As for the other countries, it seems that a lot of them that are placed towards the bottom of the scatterplot follow a similar pattern despite the inability to tell them apart.\
Another pattern for the "Other Countries" is that the higher the wealth inequality, the more sporadic the information gets.\
This could also be because countries with higher economic inequality failed to report their Gini coefficient consistently throughout the years. However, it can have multiple contributing unknown factors, which is why this visualization may be difficult to read.\
Generally, when you look at the data as one body of information, you can only take away that economic inequality is spread so far beyond the scope of anything interpretable in this state, excluding the trend of the Gini Coefficient in the United States.\
Most percentages of inequality range from twenty to sixty percent, with some outliers reaching seventy and one slightly above that.

## Notes/Commentary:
1. Something that I personally did not enjoy about this visualization is how many countries are included. There is only so much space given to depict tangible information while loading it with as many perspectives as possible.
2. I also wished that there were lines ([smoothing](https://en.wikipedia.org/wiki/Smoothing)) going through the points that correspond to their respective countries, even if it were to be non-descript.
3. It would allow for some type of visualization by way of trends and to see more clearly what countries had missing data through a specific period of time.
4. The visualization can also be cleaned up by eliminating the underscores in the names of the variables on the x and y axes.
5. It could have used its own title defining and further depicting/explaining what the visual pertains to.

### It looks readable initially, but it lacks the specificity needed to tell a clear, tangible story. There are also a few aesthetic elements that could definitely be improved upon.
___
## RStudio Code for Initial Attempt:

gini <-read.csv('shared/gini.csv')
> This loads the gini coefficient dataset into RStudio.

View(gini)
> Displays the dataset as a table in a separate window within RStudio.

gini <- gini[, colSums(is.na(gini)) != nrow(gini)]
> Removes the columns that are full of N/A's

library(tidyr)
> Loads a new package into RStudio.

long_gini <- gini %>% pivot_longer(cols = starts_with('X'),names_to = 'Year',values_to = 'Gini_Coeff')
> Converts the dataset from wide to long format by creating a new separate spreadsheet called "long_gini".

long_gini$Indicator.Code <- NULL
> Deletes the "Indicator Code" column that contains irrelevant information.

long_gini$Indicator.Name <- NULL
> Deletes the "Indicator Name" column that contains irrelevant information.

long_gini$Country.Code <- NULL
> Deletes the "Country Code" column that contains irrelevant information.

long_gini <- long_gini %>% filter(!is.na(Gini_Coeff))
> This deletes all the N/A rows in the "Gini_Coeff" column.

long_gini$Year_Numerical <- substr(long_gini$Year, nchar(long_gini$Year) - 3, nchar(long_gini$Year))
> This code extracts all the values from the "Year" column in the "long_gini" dataset and saves it as a new column named "Year_Numerical".

long_gini$Year_Numerical <- as.numeric(long_gini$Year_Numerical)
> The code that was copied into the "Year_Numerical column gets converted into strictly numerical values by excluding the "x" variable that we originally started with.

long_gini$USA <- ifelse(long_gini$Country.Name=='United States', 'USA', 'Other Countries')
> This creates a new column that differentiates between USA and "Other Countries" by utilizing if/else statements. Example: if USA = TRUE, else = FALSE = Other Countries.

mplot(long_gini)
> This asks the software to plot the data as a visualization. It then prompts you with the following:

1: 1-variable (histogram, density plot, etc.)\
2: 2-variable (scatter, boxplot, etc.)
> Select one by entering a value for the visualization you would like to create.

Selection: 2
> I chose the second value to produce a scatterplot.

Once I enter the desired values in the "Manipulate" pop-up using the gear icon, the expression of the visualization is as follows:
> gf_point(Gini_Coeff ~ Year_Numerical, data = long_gini, color = ~ USA) |>\
  > gf_theme(legend.position = "right") |>\
  > gf_labs(title = "", caption = "")

# **Visualization 2: Second Attempt**
![Visualization 2](/gini2.png)

## The image shows the Gini coefficients for all of the Caribbean countries included in the dataset at certain numerical years. It has also been color-coded by individual country.

For visualization two, I chose a smoothed scatterplot. In this visualization, the information that is depicted is the numerical year on the x-axis, the Gini coefficient on the y-axis, all color-coded by country as depicted by the guide. Here I focused on Caribbean countries to make the country list shorter, but to also selfishly discover more unique information about the area of the world that I come from.\
In the visualization, you can really see which countries lacked data, as those were not smoothed and only had one or two data points. As for the data that was able to be smoothed, there isn’t much of a pattern. The only identifiable pattern or similarity is really shared between Belize and Jamaica. They fluctuate in dramatic ups and downs but even still, they are not truly similar enough to be an interesting pattern.\
I can appreciate the fact that almost all countries start with or are headed towards more economic equality as economic equality is always amazing. However, an interesting deviation from that trend would be Belize. In Belize’s data, you can truly see how they started with a steep slope of economic inequality. Historically, Belize was invaded and occupied by British colonial rulers and greedy timber corporations that came to steal resources from Belize, hence the bad head start as depicted. The big three contributing factors post-research I would say are: how land was cut up disproportionately to satisfy the timber corporations' needs, most of the population being stuck in low-wage jobs, as well as having a singular resource export-driven industry.
Something I did not like in this visualization was the lack of data. It was a little disappointing to not have as much data to work with. Another thing that I did not enjoy was not being able to figure out how to make the unsmoothed points larger in the spirit of better depicting and differentiating them from the data points of smoothed countries as shown. I think it can get a little confusing when looking at it because some points are too close to one another. The singular or dual-pointed data is the easiest to miss due to data points being aesthetically similar in both color and size.

## Notes/Commentary:
1. Reiterating the points made in the description before this, one of the elements that I personally did not enjoy about this visualization is the lack of data despite honing in on a more specific grouping of countries from the dataset.
2. It does, however, offer the space to provide more nuanced and specific information, just like with Belize and the aforementioned issues that were associated with the high levels of inequality before the eventual leveling out.
3. The countries that did not provide enough unsmoothed points are essentially indistinguishable in terms of color and size.
4. Not only are the points almost indistinguishable in color and size, they are also very close to the other points, which combined makes it impossible to pick them apart.

### The visualization has made major improvements in comparison to the first iteration. The information itself has been condensed down but still suffers from inadequate visual aspects that can be worked on.
___
## RStudio Code for Second Attempt:

gini <-read.csv('shared/gini.csv')
> This loads the gini coefficient dataset into RStudio.

View(gini)
> Displays the dataset as a table in a separate window within RStudio.

gini <- gini[, colSums(is.na(gini)) != nrow(gini)]
> Removes the columns that are full of N/A's

library(tidyr)
> Loads a new package into RStudio.

long_gini <- gini %>% pivot_longer(cols = starts_with('X'),names_to = 'Year',values_to = 'Gini_Coeff')
> Converts the dataset from wide to long format by creating a new separate spreadsheet called "long_gini".

View(long_gini)
> Displays the dataset as a table in a separate window within RStudio.

long_gini$Indicator.Code <- NULL
> Deletes the "Indicator Code" column that contains irrelevant information.

long_gini$Indicator.Name <- NULL
> Deletes the "Indicator Name" column that contains irrelevant information.

long_gini$Country.Code <- NULL
> Deletes the "Country Code" column that contains irrelevant information.

long_gini <- long_gini %>% filter(!is.na(Gini_Coeff))
> This deletes all the N/A rows in the "Gini_Coeff" column.

long_gini$Year_Numerical <- substr(long_gini$Year, nchar(long_gini$Year) - 3, nchar(long_gini$Year))
> This code extracts all the values from the "Year" column in the "long_gini" dataset and saves it as a new column named "Year_Numerical".

long_gini$Year_Numerical <- as.numeric(long_gini$Year_Numerical)
> The code that was copied into the "Year_Numerical column gets converted into strictly numerical values by excluding the "x" variable that we originally started with.

caribbean_gini <- filter(long_gini, Country.Name=='Barbados' | Country.Name=='Belize' | Country.Name=='Dominican Republic' | Country.Name=='Guyana' | Country.Name=='Haiti' | Country.Name=='Jamaica' | Country.Name=='Suriname' | Country.Name=='Trinidad and Tobago')
> I reverse-engineered this line of code from the classroom exercise code provided:\
> us_canada_gini = filter(long_gini, Country.Name=='United States' | Country.Name == 'Canada')\
> What this code essentially does is hand-select all of the desired countries by separating them out of the "long_gini" dataset and creating a new dataset named "caribbean_gini".

View(caribbean_gini)
> Displays the dataset as a table in a separate window within RStudio.

mplot(caribbean_gini)
> This asks the software to plot the data as a visualization. It then prompts you with the following:

1: 1-variable (histogram, density plot, etc.)\
2: 2-variable (scatter, boxplot, etc.)
> Select one by entering a value for the visualization you would like to create.

Selection: 2
> I chose the second value to produce a scatterplot.

Once I enter the desired values in the "Manipulate" pop-up using the gear icon, the expression of the visualization is as follows:
> `geom_smooth()` using method = 'loess'\

gf_point(Gini_Coeff ~ Year_Numerical, data = caribbean_gini, color = ~ Country.Name) |>\
  gf_smooth() |>\
  gf_theme(legend.position = "right") |>\
  gf_labs(title = "", caption = "")\
`geom_smooth()` using method = 'loess'

# **Visualization 3: Final Attempt**
![Visualization 3](/gini3.png)

## The image shows the Gini coefficients for all of the Caribbean countries included in the dataset at certain numerical years. It has also been color-coded by individual country.

For visualization three, I chose a smoothed scatterplot. In this visualization, the information that is depicted is the numerical year on the x-axis, the Gini coefficient on the y-axis, all color-coded by country as depicted by the guide. Here I focused on Caribbean countries to make the country list shorter, but to also selfishly discover more unique information about the area of the world that I come from.\
In the visualization, you can really see which countries lacked data, as those were not smoothed and only had one or two data points. As for the data that was able to be smoothed, there isn’t much of a pattern. The only identifiable pattern or similarity is really shared between Belize and Jamaica. They fluctuate in dramatic ups and downs but even still, they are not truly similar enough to be an interesting pattern.\
I can appreciate the fact that almost all countries start with or are headed towards more economic equality as economic equality is always amazing. However, an interesting deviation from that trend would be Belize. In Belize’s data, you can truly see how they started with a steep slope of economic inequality. Historically, Belize was invaded and occupied by British colonial rulers and greedy timber corporations that came to steal resources from Belize, hence the bad head start as depicted. The big three contributing factors post-research I would say are: how land was cut up disproportionately to satisfy the timber corporations' needs, most of the population being stuck in low-wage jobs, as well as having a singular resource export-driven industry.
Something I did not like in this visualization was the lack of data. It was a little disappointing to not have as much data to work with. Another thing that I did not enjoy was not being able to figure out how to make the unsmoothed points larger in the spirit of better depicting and differentiating them from the data points of smoothed countries as shown. I think it can get a little confusing when looking at it because some points are too close to one another. The singular or dual-pointed data is the easiest to miss due to data points being aesthetically similar in both color and size.

## Notes/Commentary:
1. Reiterating the points made in the description before this, one of the elements that I personally did not enjoy about this visualization is the lack of data despite honing in on a more specific grouping of countries from the dataset.
2. It does, however, offer the space to provide more nuanced and specific information, just like with Belize and the aforementioned issues that were associated with the high levels of inequality before the eventual leveling out.
3. The countries that did not provide enough unsmoothed points are essentially indistinguishable in terms of color and size.
4. Not only are the points almost indistinguishable in color and size, they are also very close to the other points, which combined makes it impossible to pick them apart.

### The visualization has made major improvements in comparison to the first iteration. The information itself has been condensed down but still suffers from inadequate visual aspects that can be worked on.
___
## RStudio Code for Second Attempt:

gini <-read.csv('shared/gini.csv')
> This loads the gini coefficient dataset into RStudio.

View(gini)
> Displays the dataset as a table in a separate window within RStudio.

gini <- gini[, colSums(is.na(gini)) != nrow(gini)]
> Removes the columns that are full of N/A's

library(tidyr)
> Loads a new package into RStudio.

long_gini <- gini %>% pivot_longer(cols = starts_with('X'),names_to = 'Year',values_to = 'Gini_Coeff')
> Converts the dataset from wide to long format by creating a new separate spreadsheet called "long_gini".

View(long_gini)
> Displays the dataset as a table in a separate window within RStudio.

long_gini$Indicator.Code <- NULL
> Deletes the "Indicator Code" column that contains irrelevant information.

long_gini$Indicator.Name <- NULL
> Deletes the "Indicator Name" column that contains irrelevant information.

long_gini$Country.Code <- NULL
> Deletes the "Country Code" column that contains irrelevant information.

long_gini <- long_gini %>% filter(!is.na(Gini_Coeff))
> This deletes all the N/A rows in the "Gini_Coeff" column.

long_gini$Year_Numerical <- substr(long_gini$Year, nchar(long_gini$Year) - 3, nchar(long_gini$Year))
> This code extracts all the values from the "Year" column in the "long_gini" dataset and saves it as a new column named "Year_Numerical".

long_gini$Year_Numerical <- as.numeric(long_gini$Year_Numerical)
> The code that was copied into the "Year_Numerical column gets converted into strictly numerical values by excluding the "x" variable that we originally started with.

caribbean_gini <- filter(long_gini, Country.Name=='Barbados' | Country.Name=='Belize' | Country.Name=='Dominican Republic' | Country.Name=='Guyana' | Country.Name=='Haiti' | Country.Name=='Jamaica' | Country.Name=='Suriname' | Country.Name=='Trinidad and Tobago')
> I reverse-engineered this line of code from the classroom exercise code provided:\
> us_canada_gini = filter(long_gini, Country.Name=='United States' | Country.Name == 'Canada')\
> What this code essentially does is hand-select all of the desired countries by separating them out of the "long_gini" dataset and creating a new dataset named "caribbean_gini".

View(caribbean_gini)
> Displays the dataset as a table in a separate window within RStudio.

mplot(caribbean_gini)
> This asks the software to plot the data as a visualization. It then prompts you with the following:

1: 1-variable (histogram, density plot, etc.)\
2: 2-variable (scatter, boxplot, etc.)
> Select one by entering a value for the visualization you would like to create.

Selection: 2
> I chose the second value to produce a scatterplot.

Once I enter the desired values in the "Manipulate" pop-up using the gear icon, the expression of the visualization is as follows:
> `geom_smooth()` using method = 'loess'\

gf_point(Gini_Coeff ~ Year_Numerical, data = caribbean_gini, color = ~ Country.Name) |>\
  gf_smooth() |>\
  gf_theme(legend.position = "right") |>\
  gf_labs(title = "", caption = "")\
`geom_smooth()` using method = 'loess'

# Directory:

### [Go Back Home](https://portfoliognat.github.io/Home/)

# Dataset Projects:

[MPG (Miles Per Gallon) Dataset](https://portfoliognat.github.io/MPG/)\
[Map Datasets](https://portfoliognat.github.io/Maps/)
