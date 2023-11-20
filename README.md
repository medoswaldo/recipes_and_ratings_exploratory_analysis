# Recipes and Ratings Exploratory Analysis
A small data analysis project regards recipes for a course called DSC80

By Oswaldo Medina Jr (omedinajr@ucsd.edu)

## Introductions:
With the internet era making it easier to find recipes online, it is challenging to understand peoples’ opinions towards these recipes. It is also difficult to know if these recipes are genuinely rated highly because of a generally intricate, well-thought-out or a recipe that is not entirely accurate in its rating. With understanding that recipes have different ratings according to other people, we also need to realize that recipes have many factors that lead them to be rated highly or lower. In this analysis, I’ll explore a dataset from food.com that contains two sub-datasets, one being targeted towards just having the recipes and the other being reviewing and rating those recipes. In the recipes dataset, there are 83782 (rows) unique recipes followed by 12  (columns)  distinct rows towards these recipes, and the rating data has over 731927 (rows) reviews and five columns towards these reviews.

In my analysis of this dataset, I’ll focus primarily on all recipes with a dessert tag and specifically around the question, Is there a correction between the number of ingredients in a dessert recipe and its rating within the dessert tags? This question is looking towards understanding if dessert needs to be complex to be enjoyed or if the complexity of ingredients doesn't matter. Its rating answers whether a dessert needs to have many ingredients to be appreciated more or if it doesn’t matter. For this analysis to answer this question, there are a few columns that are essential to answering the question: 
- `id`: The unique identification of each recipe
- `n_ingredients`: The number of ingredients the recipe requires
- `tags`: The tags that are used to describe the recipes
- `rating`: The rating of the recipe
- `rating_avg`: The average rating towards the recipes as a whole


## Cleaning and EDA
Before continuing with the analysis, the dataset isn’t completely clean in answering the question. We start with two raw datasets: recipes and ratings. 

### Checking Data Types:
Before performing the required action towards cleaning the dataset, I need to check the datatype to see if it seemed the best fit for the cleaned dataset and any required action that might be necessary.

**Raw Recipes dtypes**


|:---------------|:-------|
| name           | object |
| id             | int64  |
| minutes        | int64  |
| contributor_id | int64  |  
| submitted      | object |
| tags           | object |
| nutrition      | object |
| n_steps        | int64  |
| steps          | object |
| description    | object |
| ingredients    | object |
| n_ingredients  | int64  |


**Raw Interactions dtypes**

|:----------|:-------|
| user_id   | int64  |
| recipe_id | int64  |
| date      | object |
| rating    | int64  |
| review    | object |

### Merging Recipes and Interaction Dataset
There are two datasets, one with recipes and the other with multiple interactions, such as people's opinions towards the recipes. Merging the dataset was best to reflect the recipes as a whole. A left join was performed on their represented id: left data being on `id` and the other dataset being `recipe id`. The new merged dataset has 234429 rows and 23 columns.

### Adding Average Rating Per Recipe Column 
To add a new column towards adding the average rating per recipe, we first started with a change in all 0s in the rating columns column with np.nan. After filling in with 0, I group by the `id` columns to get each id or recipe average recipe and grab only the average rating column to perform a left join to the recipes data frame and rename the new column from the merage to rating_avg, so the main dataset has the rating_avg column. 

### Changing the time type column to DateTime 
Columns such as `submitted` and `date` were seen as object types, and I’ve changed them into a DateTime type.

### Nutrition Column
The nutrition column has many subparts involved in many nutritional values that could be split into their respective columns. The `nutrition` column was split into multiple lists and added into the recipe data frame as their repeated value, so, for example, the calories’ list was added to the data frame as `calories`. 

### Converting Object to List
Another problem I was having was that the object type containing an element, such as a string, was being presented as a string instead of a list. The three columns that had to switch into a list were `tags`, `steps`, and `ingredients`.

### Other Actions
Another step that was taken to ensure the analyst of the question I presented was the dataset needs only to be recipes that are categorized as a dessert. The way this is accomplished is to filter within the tags columns and only obtain the last that has the keyword dessert in them. After completing the filtering of only dessert recipes, the dataset was 34641 rows, meaning that only 14 percent of the dataset were recipes under the dessert tag. 

### Cleaned Results
The cleaned data frame’s datatype.

|:--------------------|:---------------|
| index               | int64          |
| name                | object         |
| id                  | int64          |
| minutes             | int64          |
| contributor_id      | int64          |
| submitted           | datetime64[ns] |
| tags                | object         |
| n_steps             | int64          |
| steps               | object         |
| description         | object         |
| ingredients         | object         |
| n_ingredients       | int64          |
| user_id             | float64        |
| date                | datetime64[ns] |
| rating              | float64        |
| review              | object         |
| rating_avg          | float64        |
| calories            | float64        |
| total fat (PDV)     | float64        |
| sugar (PDV)         | float64        |
| sodium (PDV)        | float64        |
| protein (PDV)       | float64        |
| saturated fat (PDV) | float64        |
| carbohydrates (PDV) | float64        |



A few rows from the cleaned DataFrame with the columsn that are relevvant to answering our question.

|    | name                                 |     id |   n_steps |   n_ingredients |   rating |   rating_avg |
|---:|:-------------------------------------|-------:|----------:|----------------:|---------:|-------------:|
|  0 | 1 brownies in the world    best ever | 333281 |        10 |               9 |        4 |      4       |
|  1 | millionaire pound cake               | 286009 |         7 |               7 |        5 |      5       |
|  2 | honey  i m peanuts about you   cake  | 293225 |        39 |              16 |        5 |      5       |
|  3 | honey  i m peanuts about you   cake  | 293225 |        39 |              16 |        5 |      5       |
|  4 | puddingkuchen   custard bake         | 353171 |         6 |               6 |        4 |      4.33333 |



## Exploratory Data Analysis
### Univariate Analysis:
In the Univaovatoes Analysis, I seek to explore the number of recipes for each number of ingredients in both my dessert dataset compared to the overall and the distribution of the number of steps.

<iframe src="assests/dis_num_of_ing.html" width=800 height=600 frameBorder=0></iframe>
This shows the distribution of several ingredients in the dataset with only desserts. Around most recipes, 5 to 10 ingredients, with the average being around eight ingredients. 


<iframe src="assests/dis_num_of_ing_all.html" width=800 height=600 frameBorder=0></iframe>
This is the distribution of the number of ingredients for the entire dataset instead of just desserts. It still has the same right-skewed shape and averages around eight ingredients. 

<iframe src="assests/steps_dis.html" width=800 height=600 frameBorder=0></iframe>
The distribution of several steps has the same right-skewed distraction as the number of ingredients. This could be from a correlation between the number of ingredients and the number of steps. 

### Bivariate Analysis
The bivariate analysis uses the number of ingredients and other factors, such as the number of steps and the rating.

<iframe src="assests/bi_any_is.html" width=800 height=600 frameBorder=0></iframe>
This is the bivariate analysis between the number of ingredients and number of steps. They seem to follow what I initially thought of correlating them, but many recipes don’t have an absolute correlation.

<iframe src="assests/n_r_bian.html" width=800 height=600 frameBorder=0></iframe>
As you could be, the number of ingredients doesn't correlate much to the average rating, but it’s noticeable that the rating doesn’t change until it is over 15. A rating goes up and down in rating and worst in 24. What this could mean is that there are fewer recipes, and it has an effect on the average rating. 

### Interesting Aggregates
In the aggregates analysis, I wanted to look at the number of ingredients and their average rating towards the number of ingredients. The reason behind this would be to understand, at a basic level, if the number of ingredients impacts the rating for the dessert recipes. Also, we could observe many things, such as the last few ingredients having a relatively high average, but this could be because of limited recipes with that amount of recipes. 

|   n_ingredients |   rating |
|----------------:|---------:|
|               1 |     4.57 |
|               2 |     4.63 |
|               3 |     4.7  |
|               4 |     4.67 |
|               5 |     4.63 |
|               6 |     4.61 |
|               7 |     4.56 |
|               8 |     4.57 |
|               9 |     4.59 |
|              10 |     4.62 |
|              11 |     4.64 |
|              12 |     4.64 |
|              13 |     4.66 |
|              14 |     4.62 |
|              15 |     4.62 |
|              16 |     4.68 |
|              17 |     4.53 |
|              18 |     4.53 |
|              19 |     4.72 |
|              20 |     4.71 |
|              21 |     4.78 |
|              22 |     4.52 |
|              23 |     5    |
|              24 |     3    |
|              25 |     4.5  |
|              26 |     4.5  |
|              27 |     5    |

## Hypothesis Testing 
The question that started this analysis was: Is there a correction between the number of ingredients in a dessert recipe and its rating within the dessert tags? 

For this, we want to see that a recipe with an above-average number of ingredients has a higher rating than usual, and our ingredient threshold will be above the average of 8.

Null Hypothesis (H0): There’s no difference in rating based on a recipe's number of ingredients 

Alternative Hypothesis (H1): Desserts with more ingredients tend to be rated higher than average.

To perform the testing, I first obtained the columns that seemed most helpful for this, the rating and number of ingredients. From there, I created a new column called ingedient_heavy, a boolean-only column that is True if the number of elements exceeds eight and False otherwise. 

Test Statistic: The difference in means from comparing the mean of the average of recipes with eight or more ingredients compared to recipes with fewer.

P-value cutoff: We’ll use the standard cutoff of 0.05 to determine the probability of seeing the following result, at least as observed. 

The observed difference in the mean is 0.017056668063809788

The Empirical Distribution from the Hypothesis Test:

<iframe src="assests/final_fig.html" width=800 height=600 frameBorder=0></iframe>

The p-value from the Hypothesis test was 0.0388, less than the p-value cutoff of 0.05, meaning we can reject the null hypothesis. This indicates a 3.88% chance of observing the observed difference in means or a more extreme difference. This also means that there’s typically a high rating for recipes with eight or more ingredients,
