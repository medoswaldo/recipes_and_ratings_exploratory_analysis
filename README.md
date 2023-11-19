# Recipes and Ratings Exploratory Analysis
A small data analysis project regards recipes for a course called DSC80

By Oswaldo Medina Jr (omedinajr@ucsd.edu)

## Introductions:
With the internet era making it easier to find recipes online, it is challenging to understand peoples’ opinions towards these recipes. It is also difficult to know if these recipes are genuinely rated highly because of a generally intricate, well-thought-out or a recipe that is not entirely accurate in its rating. With understanding that recipes have different ratings according to other people, we also need to realize that recipes have many factors that lead them to be rated highly or lower. In this analysis, I’ll explore a dataset from food.com that contains two sub-datasets, one being targeted towards just having the recipes and the other being reviewing and rating those recipes. In the recipes dataset, there are 83782 (rows) unique recipes followed by 12  (columns)  distinct rows towards these recipes, and the rating data has over 731927 (rows) reviews and five columns towards these reviews.

In my analysis of this dataset, I’ll focus primarily on all recipes with a dessert tag and specifically around the question, Is there a correction between the number of ingredients in a dessert recipe and its rating within the dessert tags? This question is looking towards understanding if dessert needs to be complex to be enjoyed or if the complexity of ingredients doesn't matter. Its rating answers whether a dessert needs to have many ingredients to be appreciated more or if it doesn’t matter. For this analysis to answer this question, there are a few columns that are essential to answering the question: 
- ‘id’: The unique identification of each recipe
- ‘n_ingredients’: The number of ingredients the recipe requires
- ‘tags’: The tags that are used to describe the recipes
- ‘rating’: The rating of the recipe
- ‘Rating_avg’: The average rating towards the recipes as a whole

<iframe src="assets/dis_num_ing.html" width=800 height=600 frameBorder=0></iframe>