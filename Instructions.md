# Project Setup and Collaboration Guide

## Introduction

This document explains how to set up the project repository, work with environments, and collaborate effectively using GitHub.

The project involves predicting the prevalence of poor mental health in neighborhoods based on demographic, socioeconomic, and environmental factors.

## Step 1: Clone the GitHub Repository

1.  Go to the [GitHub repository](https://github.com/your-username/mental-health-prediction).
2.  Clone the repository to your local system using the following command:

```         
git clone https://github.com/your-username/mental-health-prediction.git 
cd mental-health-prediction
```

## Step 2: Work with Jupyter Notebooks

1.  Create a new notebook in the notebooks/ directory. For example, EDA.ipynb for Exploratory Data Analysis.
2.  Save your notebook and commit the changes:

```         
   git add notebooks/EDA.ipynb

   git commit -m "Added EDA notebook" git push origin main
```

## Step 3: Collaborating with the Team

### Branching

1.  Create a new branch for your task:

```         
git checkout -b feature/your-task-name
```

2.  After completing your work, push the branch:

```         
git push origin feature/your-task-name
```

### Merging Changes

1.  Create a pull request (PR) on GitHub to merge your branch into the main branch.
2.  Review the changes and merge the PR.

## Step 4: Handling Merge Conflicts in Notebooks

To avoid merge conflicts in Jupyter notebooks, it is recommended to use the **nbdime** tool:

1.  Install nbdime :

```         
pip install nbdime
```

2.  Enable Git integration for nbdime :

```         
nbdime config-git --enable
```

This will make it easier to resolve conflicts in notebooks.

## Step 5: Pull the changes from remote repo to local repo

There have been some changes in the main branch since you last worked on it. Run the code below to sync them into your local system.

```
git pull origin main
```

## Step 6: Use GitHub data remotely

See below example to use the data in data/data.csv remotely if you do not want to download it.

```python
import pandas as pd

# URL of the raw CSV file in your GitHub repository
url = "https://raw.githubusercontent.com/SodiumMan91/mental-health-prediction/refs/heads/main/data/data.csv"

df = pd.read_csv(url)
df = df.drop(['Unnamed: 0.1', 'Unnamed: 0', 'lon', 'lat', 'nearest_lat', 'nearest_lon'], axis = 1)
```
The url here refers to our actual data so there is no need to update it.



