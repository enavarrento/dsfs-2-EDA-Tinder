# Project Tinder - Exploratory Data Analysis (EDA)

## Context & Objective 🎯
Tinder's marketing team is experiencing a decrease in the number of matches and requires data-driven insights to understand **what makes people interested in each other**. 

This project performs an Exploratory Data Analysis (EDA) on an experimental speed-dating dataset. The goal is to analyze participant demographics, in-the-moment ratings, and stated preference surveys to identify the true drivers of a "match" and a second date.

## Data Source 📇
The analysis is based on data gathered from experimental speed dating events conducted between 2002 and 2004. 
* Attendees had 4-minute "first dates" with other participants.
* Decisions (`dec`) and target matches (`match`) were recorded.
* Participants rated partners on six attributes: Attractiveness, Sincerity, Intelligence, Fun, Ambition, and Shared Interests.
* Surveys were conducted to capture stated preferences and self-perception.

**Original Assets:**
* [Speed Dating Dataset (.csv)](https://full-stack-assets.s3.eu-west-3.amazonaws.com/M03-EDA/Speed+Dating+Data.csv)
* [Dataset Description / Key (.doc)](https://full-stack-assets.s3.eu-west-3.amazonaws.com/M03-EDA/Speed+Dating+Data+Key.doc)

## Approach & Methodology 🚧

An iterative, MVP-focused workflow was adopted. The data engineering phase revealed critical structural nuances in the dataset, leading to a specific cleansing approach:

### The Wave Scale Challenge & Two-Track Cleansing
During the data discovery phase, a severe methodological inconsistency was identified:
* Participants in **waves 6-9** were asked to rate the importance of attributes on a **1-10 scale**.
* Participants in **all other waves** were asked to distribute **100 points** among the attributes.

Mixing these scales invalidates comparative statistics. Normalizing a 1-10 scale to a 100-point scale introduces behavioral artifacts, as allocating 100 points forces trade-offs, whereas a 1-10 scale does not. To maintain maximum statistical power while ensuring mathematical validity, the dataset was split into two distinct tracks:

1. **Track 1: Behavioral Data (All Waves)**: Used for analyzing actual decisions and in-the-moment 1-10 partner ratings, which remained consistent across the entire experiment.
2. **Track 2: Preferences Data (Waves 6-9 Excluded)**: Used exclusively for analyzing the stated preference surveys, ensuring the 100-point allocation scale remains mathematically pure.

### Analytical Disclaimer: Stated vs. Revealed Preferences
The final analysis compares "Stated Preferences" (100-point scale) against "Revealed Behaviors" (calculated via correlation coefficients normalized to a percentage). This comparison must be interpreted with a grain of salt. While it highly effectively illustrates the directional behavioral gap between what people say and what they do, it merges two fundamentally different measurement methodologies.

## Repository Structure 📁

```text
├── assets/                                 # Exported figures
│   ├── html/                               # .html interactive charts (Bxx for Behavior, Pxx for Preferences)
│   └── png/                                # .png charts
├── data/
│   ├── raw/                                # Original speed_dating_data.csv (Immutable)
│   └── processed/                          # Cleaned checkpoints (Track 1 and Track 2 csv files)
├── notebooks/
│   ├── 00-Sandbox.ipynb                    # Initial explorations and discovery for cleansing strategy
│   ├── 01-Cleansing.ipynb                  # Data processing pipeline and checkpoint generation
│   └── 02-Analysis.ipynb                   # EDA visuals, correlations, and business insights
├── README.md                               # Project documentation
└── requirements.txt                        # Environment dependencies