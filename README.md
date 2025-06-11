# FIFA World Cup Analysis - 2018

**Author:** Sergio E. Sagastume 

**Repository:** [fifa-world-cup-analysis](https://github.com/ssagastume11/fifa-world-cup-analysis)

---

## 📌 Introduction
This project analyzes player-level data from the 2018 FIFA World Cup. It focuses on understanding trends in player age, experience (appearances and goals), and position distribution across national teams.

## 🌍 Scenario
I'm a junior data analyst working on a portfolio project to improve my skills in R and data storytelling. I chose the 2018 FIFA World Cup dataset to explore patterns in player attributes such as age, club affiliation, and nationality.

---

## ❓ Ask
**Business Task:** Analyze squad compositions at the 2018 FIFA World Cup to identify trends in player age, experience, and positions across different national teams.

---

## 📦 Prepare
**Dataset:** 2018 FIFA World Cup Squads

**Source:** [2018 FIFA World Cup Squads Dataset](https://www.kaggle.com/datasets/cclayford/2018-fifa-world-cup-squads)

```{r}
# Load libraries
library(tidyverse)
library(ggplot2)

# Read dataset
squads <- read_csv("2018 FIFA World Cup Analysis/2018 FIFA World Cup Squads.csv")

```

---

## 🧹 Process

Data cleaning included:
- Renaming column headers
- Cleaning inconsistent strings
- Extracting features like player age
- Removing missing and irrelevant rows

```{r}
# Clean column names
squads <- squads %>%
  rename_all(~ str_replace_all(., " ", "_")) %>%
  filter(!is.na(Age))

```

## 📊 Analyze

![Age distributuion](https://raw.githubusercontent.com/ssagastume11/fifa-world-cup-analysis/refs/heads/main/team_age_exp.png)
```{r}
# Age distribution
ggplot(squads, aes(x = Age)) +
  geom_histogram(binwidth = 1, fill = "skyblue", color = "black") +
  labs(title = "Distribution of Player Ages in 2018 World Cup",
       x = "Player Age", y = "Count of Players",
       caption = "Source: 2018 FIFA World Cup Squad Data (CSV)") +
  theme_minimal()

```

---

## 📣 Share
This analysis was compiled using RMarkdown and includes visualizations and summaries to help sports enthusiasts and data students understand player distribution and team patterns during the 2018 tournament.

---

## ✅ Act
Results translated into useful results for readers:
```{r}
# Identify youngest and oldest teams
team_ages <- squads %>%
  group_by(Country) %>%
  summarise(avg_age = mean(Age, na.rm = TRUE)) %>%
  arrange(desc(avg_age))

print(team_ages)

```
This result helps compare the average ages of teams, which is useful for coaches, fans, and analysts who want to understand how age influences team strategy or tournament performance.

---

## 💡 Recommendations
1. **Explore Club Representation**: Analyze which clubs contributed the most players to the tournament.
2. **Extend to Match Stats**: Combine this with performance data to assess how age or club affiliation affects match outcomes.
3. **Visualize Geography**: Trace player nationality to see global patterns.
4. **Compare Across Tournaments**: Expand the dataset to include other FIFA World Cup years.
5. **Build Interactive Dashboard**: Use Shiny or Tableau for dynamic team and player exploration.
