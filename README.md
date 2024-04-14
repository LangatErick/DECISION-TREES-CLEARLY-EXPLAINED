# DECISION-TREES-CLEARLY-EXPLAINED
Decision trees are a popular machine learning technique for classification and regression analysis. They are particularly useful for data analysis because they can help identify the most important variables in a dataset and uncover patterns that may be hidden in the data.
---
title: "DECISION TREE: IRIS DATASET"
author: "Langat Erick"
output: pdf_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(
 warning = FALSE,
 message = FALSE,
 echo = TRUE)
```

##### **Decision trees are a popular machine learning technique for classification and regression analysis. They are particularly useful for data analysis because they can help *identify the most important variables in a dataset*** **and uncover patterns that may be hidden in the data.**

##### Here's an example of how to conduct a decision tree analysis in R programming:

First, we need to load the necessary libraries. In this example, we will be using the **`rpart`** library for decision trees:

```{r}
library(rpart)
library(timetk)
library(tidymodels)
library(rpart.plot)
library(report)
```

Next, let's load a data-set to work with. In this example, we will be using the **`iris`** data-set, which is included in R. This data-set contains measurements for the sepal length, sepal width, petal length, and petal width of 150 iris flowers, along with their species (*setosa, versicolor, or virginica*):

```{r}
data(iris)
colnames(iris)
```

Now, let's split the data-set into training and testing sets. We will use the training set to build our decision tree model, and the testing set to evaluate its accuracy:

```{r}
set.seed(123)
# train_index <- sample(1:nrow(iris), nrow(iris)*0.7)
split <- initial_split(iris, prop = 0.7)
split
```

```{r}
train_data <- training(split)
test_data <- testing(split)
```

Next, we will build our decision tree model using the **`rpart()`** function. In this example, we will be using the sepal length, sepal width, petal length, and petal width as predictor variables, and the iris species as the response variable:

```{r}
tree_model <- rpart(Species ~ ., data = train_data, method = "class")
summary(tree_model)
```

We can visualize the decision tree using the **`plot()`** function:

```{r}
# plot(tree_model)
rpart.plot(tree_model,col=rainbow(2))
```

Finally, we can evaluate the accuracy of our decision tree model using the testing data:

```{r}
predicted_species <- predict(tree_model, test_data, type = "class")
predicted_species
```

```{r}
accuracy <- sum(predicted_species == test_data$Species)/nrow(test_data)
accuracy
```

**This will give us the accuracy of our model on the testing data.**

In summary, the above example demonstrates how to build a decision tree model using the **`rpart`** library in R programming. The decision tree helps us to identify the most important variables in a data-set and uncover patterns that may be hidden in the data. The model's accuracy can be evaluated using testing data, which allows us to see how well the model can generalize to new data.
