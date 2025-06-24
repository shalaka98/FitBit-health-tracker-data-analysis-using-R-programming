# Fitbit Health Tracker Data Analysis

## Introduction
In this project, fitbit heath tracker data is analyzed with R programming and A graphical representation is made illustrating the correlation between daily walking exercise and the resulting calories expenditure in the body, demonstrating the impact of physical activity on metabolic expenditure.

## Data Source
Path: `/kaggle/input/fitbit`

## Package Loading
```r
install.packages("tidyverse")
library(tidyverse)
```

## data uploded
```r
dailyactivity <- read.csv("/kaggle/input/dailyactivity/dailyactivity_merged _original.csv")
View(dailyactivity)
```

## Cleaning the Data
#### Select Relevant Columns
```r
steps_vs_calories <- dailyactivity %>% select(Id, TotalSteps, Calories, ActivityDate)

steps_vs_calories
```

#### Check for Missing Ids
```r
steps_vs_calories %>% summarize(sum(is.na(Id)))

steps_vs_calories
```


#### Filter Out Missing Steps
```r
filtered_steps_vs_calories <- steps_vs_calories %>% filter(!is.na(TotalSteps))
```

#### Group by ID and Compute Averages
```r
final_steps_vs_calories <- filtered_steps_vs_calories %>% 
  group_by(Id) %>% 
  summarise(total_cal = mean(Calories), total_steps = mean(TotalSteps)) 
head(final_steps_vs_calories)
```

#### Total Steps Comparison (Optional)
```r
sum(final_steps_vs_calories$total_steps)
```

#### Graphical Illustration
```r
p <- final_steps_vs_calories %>% 
  ggplot(aes(x = total_steps, y = total_cal)) +
  geom_point() +
  geom_smooth(method = "lm", color = "blue") +
 geom_text(aes(label = Id)) +
 labs(title = "Average Steps vs Calories Expenditure", 
       subtitle = "from 12/04/16 to 12/05/16", 
       x = "Average Steps", 
       y = "Calories Expenditure")
```

## Conclusion
This analysis reveals a clear correlation between daily walking exercise and calories burned, emphasizing the importance of physical activity for metabolic health. Increasing daily steps can lead to greater calorie expenditure, supporting fitness and weight management. Regular exercise should be part of a healthy routine for improved well-being




