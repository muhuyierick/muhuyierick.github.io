---
layout: post
title: "Netflix Data Wrangling in Python"
date: 2025-10-05
categories: [kaggle, datawrangling python, data-exploration, data-validation]
author: "Muhuyi Erick"
---

## Introduction

In this post, I explain a Kaggle-based assignment I completed as part of the Data and AI coursework. The post walks through each step I followed in plain English: where I got the data, how I inspected and prepared it, what analyses or models I ran, and the conclusions I drew. I also include clear placeholders where you can add the Kaggle dataset link and the raw data source so the post will be ready for publication on GitHub Pages.

---

## Project scope and goals

The dataset contains Netflix titles (movies and TV shows) with fields such as title, director, cast, country, date_added, release_year, rating, duration, and categories. My objectives were:

- Understand the raw data structure and quality.
- Standardize and type-convert fields (dates, numeric durations, categories).
- Handle missing values and duplicates in a repeatable way.
- Create derived columns to simplify later analysis (for example, separate duration value/unit and split multi-category fields).
- Validate the cleaned data using simple business rules (for example, no date_added earlier than Netflix launch).
- Export a cleaned CSV that can be shared or used for visualization and analysis.

---

## Step 1 — Environment and Data Load

I started by importing pandas and confirming the working environment (this is especially important on Kaggle, where inputs are mounted under `/kaggle/input`). I then loaded the dataset directly from the input path used on Kaggle:

`/kaggle/input/netflix-shows/netflix_titles.csv`

After loading, I printed the dataset shape and previewed the first few rows to confirm that the file was read correctly. This quick check avoids wasted work later on caused by bad paths or encoding issues.

---

## Step 2 — Discovery (Data Overview and Quality Checks)

Before changing anything, I inspected the dataset using `df.info()`, `df.columns`, `df.dtypes`, `df.isnull().sum()`, and `df.duplicated().sum()`. These commands helped me quickly answer key questions:

- How many rows and columns do I have?
- Which columns are missing values and how many?
- Are there duplicate rows to remove?
- Are data types appropriate (e.g., dates as strings)?

This discovery phase guided the cleaning decisions I made next.

---

## Step 3 — Structuring and Parsing

Two fields required structural parsing:

1. `date_added` — converted to pandas `datetime`. I used `pd.to_datetime(..., errors='coerce')` to convert values and mark unparseable items as `NaT` for later handling.

2. `duration` — this field mixes numbers and units (e.g., "90 min" or "2 Seasons"). I extracted two new columns, `duration_value` and `duration_unit`, using a regular-expression extraction. Then I converted `duration_value` to numeric to allow numeric filtering and aggregation.

These structural transformations make downstream analysis simpler (for example, comparing runtimes or filtering by number of seasons).

---

## Step 4 — Cleaning Missing Values and Duplicates

Cleaning choices were made conservatively and recorded in the notebook so the process is reproducible.

- I removed duplicate rows with `df.drop_duplicates()`.
- I dropped the `description` column (it was not needed for this analysis) and removed rows/columns that had excessive missingness.
- For important categorical fields like `director`, `cast`, `country`, and `rating`, I filled obvious blanks with a placeholder string (`'Unknown'`) where appropriate. This avoids mixing types and makes downstream grouping consistent.
- For some missing `director` values, I used an imputation heuristic: I built a combined `dir_cast` key and, where consistent director–cast pairs occurred frequently, I used those relationships to infer missing director values. This is a pragmatic, domain-aware imputation intended to preserve useful structure when the same cast tends to work with the same director.
- After the imputation attempts, any remaining `director` or `country` blanks were set to `'Not Given'` so the dataset does not contain silent nulls.

I logged `df.isnull().sum()` after each major step to confirm progress and ensure the notebook is auditable.

---

## Step 5 — Correcting Inconsistencies and Business-Rule Checks

I applied business logic to detect and correct logical inconsistencies. Two checks I ran were:

- `date_added` vs `release_year`: I counted and displayed records where `date_added` occurred before `release_year`, which is unlikely and usually indicates data issues. I examined sample records and fixed or removed problematic entries as appropriate.
- `date_added` before Netflix launch: Netflix launched in 1997, so I checked for `date_added` values before 1997 and flagged any anomalies for review.

These validation checks assured that the cleaned dataset respects simple real-world constraints.

---

## Step 6 — Data Transformation and Feature Extraction

To make the analysis easier, I split some multi-valued fields and created new columns:

- `listed_in` (categories): this field can contain multiple comma-separated categories. I split it into `listed_in_1`, `listed_in_2`, and `listed_in_3` based on the observed maximum number of categories per record. This allows straightforward grouping by primary category and keeps the original values available.
- `duration` was already split into numeric and unit components as described earlier.

I also checked the unique values for `type` and `rating` to confirm expected levels.

---

## Step 7 — Final Validation and Exporting

Before exporting, I removed temporary helper columns used during imputation, verified data types (`date_added` is datetime and `duration_value` is numeric), and sampled rows to inspect final results. I also reset the index to produce a neat CSV.

Finally, I saved the cleaned dataset to an output CSV so it can be used in later analyses or visualizations:

`/kaggle/working/cleaned_netflix.csv`

---

## Key takeaways

- Start with discovery: basic inspections (`info`, `isnull`, `describe`) drive the cleaning plan.
- Record every transformation: saving the logic in the notebook makes the pipeline reproducible and easier to review.
- Use simple, defensible imputation rules: prefer domain-aware rules where possible, and fall back to explicit placeholders like `'Unknown'` when inference is unreliable.
- Validate with business rules: basic checks (dates, ranges) catch subtle data corruption that simple null checks miss.
- Split multi-valued fields: separating categories or combined strings into columns simplifies grouping and aggregation.

---

## What I learned from doing this assignment

- Practical experience with common data-wrangling tasks: parsing dates, extracting values from strings, handling duplicates, and filling missing values.
- How to apply domain logic (for example, date constraints) to validate data.
- The importance of keeping the cleaning steps readable and reproducible so others can follow the reasoning and re-run the pipeline.

---

## summary of the steps

I built a reproducible data-wrangling pipeline for the Netflix titles dataset: I inspected and profiled the raw data, standardized dates and duration fields, imputed missing categorical fields using pragmatic rules, split multi-value category fields, validated the dataset against simple business rules, and exported a cleaned CSV for analysis. The cleaned dataset supports exploration and visualization and is ready for downstream tasks.

---

## Reproducibility and documentation

All steps are implemented in the Kaggle notebook with short comments explaining the intent of each cell. Keeping transformations and imputation steps in line in the notebook means another reader can re-run the pipeline on Kaggle or adapt it for similar datasets. For productionizing this workflow, I would extract the cleaning steps into a script or functions and add unit tests for the validation rules.

## Interactive Colab Notebook

- I wrote and executed the full pipeline inside a Kaggle notebook. You can view the original notebook and raw files on Kaggle here:
[Open the Kaggle notebook](https://www.kaggle.com/code/muhuyierick/muhuyi-erick-cs-da02-25088-data-wrangling)


## Data sources

- Netflix Dataset on Kaggle
[Netflix dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows)

---

This post is part of the assignments for the "Data and AI" program by Cyber Shujaa. The course guided the hands-on steps I followed and helped me develop practical data skills.
