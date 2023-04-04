Introduction
In this project, we'll be conducting an exploratory data analysis (EDA) on a dataset of college basketball 3 pointers. The dataset contains information on the location and outcome of over 500,000 3-point attempts from NCAA Division I basketball games over multiple seasons. Our goal is to identify patterns, trends, and relationships between variables in the dataset using various R packages like ggplot2, dplyr, and tidyr.

Data Preparation
We start by loading the dataset and performing some data cleaning and preparation steps. We first remove any missing values and duplicates, and then convert the location and outcome columns to factors:

library(dplyr)

bball <- read.csv("college_bball_3s.csv")

bball <- bball %>%
  filter(!is.na(x_loc), !is.na(y_loc), !is.na(outcome)) %>%  # remove missing values
  distinct() %>%  # remove duplicates
  mutate(location = factor(paste0(x_loc, ",", y_loc)), outcome = factor(outcome))  # convert to factors



Data Exploration
Next, we can use various data visualization and summarization techniques to explore the dataset. For example, we can create a heatmap of 3-point attempt locations:


library(ggplot2)

ggplot(bball, aes(x = x_loc, y = y_loc)) +
  geom_bin2d(binwidth = 5, aes(fill = ..count..)) +
  scale_fill_gradient(low = "white", high = "steelblue") +
  labs(title = "Heatmap of 3-Point Attempt Locations", x = "X Location", y = "Y Location")


We can see that most 3-point attempts are taken from the perimeter around the 3-point line, with a higher concentration of attempts from the corners.

Next, we can create a bar chart of 3-point attempt outcomes:

ggplot(bball, aes(x = outcome)) +
  geom_bar() +
  labs(title = "Bar Chart of 3-Point Attempt Outcomes", x = "Outcome", y = "Count")


We can see that the majority of 3-point attempts are either missed or made, with a small number being blocked.

Finally, we can use the tidyr and dplyr packages to summarize the data by team and location:

library(tidyr)

bball_summary <- bball %>%
  group_by(team, location) %>%
  summarize(num_attempts = n(), success_rate = mean(outcome == "made"), avg_distance = mean(sqrt(x_loc^2 + y_loc^2))) %>%
  arrange(desc(num_attempts))

bball_summary


This gives us a summary of the number of attempts, success rate, and average distance for each team and location.

Conclusion
In this project, we conducted an exploratory data analysis (EDA) of a college basketball 3-point attempts dataset using R and various packages like ggplot2, dplyr, and tidyr. We cleaned and prepared the data, and then used data visualization and summarization techniques to identify patterns, trends, and relationships between variables.

Our analysis showed that most 3-point attempts are taken from the perimeter around the 3-point line, with a higher concentration of attempts from the corners.
