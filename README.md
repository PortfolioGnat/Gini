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
5. It could have used its own title defining and further depicting/explaining what the visual is pertaining to.

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
> This creates a new column that differentiates between USA and "Other Countries" by utilizing if/else statements./
Exmaple: If USA = TRUE, Else = Other Countries.

1: 1-variable (histogram, density plot, etc.)\
2: 2-variable (scatter, boxplot, etc.)
> Select one by entering a value for the visualization you would like to create.

Selection: 2
> I chose the second value to produce a scatterplot

Once I enter the desired values in the "Manipulate" pop-up using the gear icon, the expression of the visualization is as follows:
> gf_point(hwy ~ displ, data = mpg) |>\
>   gf_facet_wrap(~ class, ncol = 4) |>\
>   gf_labs(title = "", caption = "")

# Directory:

### [Go Back Home](https://portfoliognat.github.io/Home/)

# Dataset Projects:

[MPG (Miles Per Gallon) Dataset](https://portfoliognat.github.io/MPG/)\
[Map Datasets](https://portfoliognat.github.io/Maps/)
