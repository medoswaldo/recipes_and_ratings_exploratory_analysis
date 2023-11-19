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

|                | 0      |
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

|           | 0      |
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

|                     | 0              |
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






<!-- <iframe src="assests/dis_num_ing.html" width=800 height=600 frameBorder=0></iframe> -->