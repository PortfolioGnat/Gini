# Gini
___
# Gini Coefficient Dataset
Below you will find different examples of visualizations that pull from a dataset called Gini. But...What is the Gini Coefficient?\
In economics, the [Gini Coefficient](https://en.wikipedia.org/wiki/Gini_coefficient), also known as the Gini Index or Gini Ratio, measures income, wealth, or consumption inequality within a particular nation or social group.

# **Visualization 1: Initial Attempt**
![Visualization 1](/gini1.png)

## The image shows the Gini coefficient at a certain numerical year. It has also been color-coded based on whether or not it is the USA or "Other Countries".

I decided to create a scatterplot. This scatterplot shows the Gini coefficient in the USA against the rest of the world. For the USA, wealth inequality started lower and then rose by about 10%.\
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

# Directory:

### [Go Back Home](https://portfoliognat.github.io/Home/)

# Dataset Projects:

[MPG (Miles Per Gallon) Dataset](https://portfoliognat.github.io/MPG/)\
[Map Datasets](https://portfoliognat.github.io/Maps/)
