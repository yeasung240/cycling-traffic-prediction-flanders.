# Predicting Daily Cycling Traffic in Flanders
Predicting Cycling Traffic in Flanders

Modelling hourly cycling volumes using temporal, weather, and spatial features, with an interactive scenario dashboard.

This collaborative project was developed for the Modern Data Analytics course at KU Leuven. This repository presents my personal overview of the team's work, with a focus on my contributions to data preparation, feature engineering, and model testing.

Project repository · Dashboard linked in the report

Overview

Cycling counts show how traffic varies across locations and time. Our project investigated how well those variations can be predicted from temporal, meteorological, and spatial information.

The team combined cycling counts, weather observations, and public transport information to train a LightGBM model with a Poisson objective. A Streamlit dashboard allows users to explore predicted hourly traffic under different conditions.

Research question: To what extent can cycling traffic volumes across Flanders be predicted using temporal, meteorological, and spatial features?

Data

Source

Data used

Agentschap Wegen en Verkeer (AWV)

Cycling counts and counting-site locations

Royal Meteorological Institute of Belgium

Temperature, rainfall, and sunshine observations

De Lijn

Public transport stop locations

The report describes 1,200,616 prepared observations for 2024 and 1,237,175 for 2025. The prediction target is the number of bicycle passages per counting site per hour, aggregated from 15-minute intervals across both travel directions.

My Role

My main contribution was data preparation and feature engineering. I also supported the team's LightGBM experiments and evaluation.

Data cleaning and preparation: Cleaned and transformed the raw data into a consistent format for modelling.

Missing-data processing: Worked on handling missing observations during data preparation.

Feature engineering: Converted variables into suitable model inputs, including cyclical representations of time features.

Model testing: Helped test the LightGBM model with different hyperparameter settings and compare model performance.

Model development, interpretation, and the dashboard were collaborative project outputs; this section describes my own involvement rather than claiming sole ownership of the workflow.

Data Preparation and Feature Engineering

The team's preparation workflow included:

Combining monthly cycling records and aggregating counts to hourly observations.

Standardising date and hour formats for merging datasets.

Linking cycling sites to nearby weather stations, using the next-nearest stations when information from the closest station was missing.

Deriving temporal features, including season and weekend indicators.

Creating public transport features based on stops within one kilometre of each counting site.

Encoding hour and month with sine and cosine pairs to represent their cyclical structure.

Preparing categorical variables for LightGBM.

Cyclical encoding represents the wraparound in time: 23:00 and 00:00 are adjacent, as are December and January. This gives the model features that reflect those relationships.

Modelling and Evaluation

The team used LightGBM with a Poisson objective to predict non-negative cycling counts while allowing nonlinear relationships and interactions between features.

The reported workflow used 2024 observations for training and randomly divided the 2025 data into validation (20%) and test (80%) subsets. Experiments varied settings such as learning rate, number of leaves, feature fraction, minimum observations per leaf, and boosting rounds.

Performance was assessed using mean Poisson deviance, with a constant prediction based on the training mean as a baseline. Lower deviance indicates better performance.

Findings

The report shows substantially lower Poisson deviance for LightGBM than for the constant-mean baseline.

Counting-site identity and time of day were prominent predictors, although their ranking differed between split-based feature importance and SHAP analysis.

Temperature contributed to predictions, while public transport features had relatively low importance in the reported SHAP analysis.

These are predictive associations, not evidence that changing a feature causes a change in cycling activity.

Interactive Dashboard

The team's Streamlit and PyDeck dashboard presents predictions on a map and in a table. Users can adjust month, hour, weekday/weekend status, temperature, rainfall, and sunshine duration.

It compares the selected scenario with a reference scenario for each station, helping users explore variation in predicted cycling activity across the network.

Limitations and Next Steps

The report describes using test performance to select boosting rounds. A stronger future evaluation would select all settings on validation data and reserve a separate test period for the final assessment.

The report contains two different model test-deviance values. Exact headline metrics are omitted here pending reconciliation with the final experiment output.

Reliance on site identity limits confidence in predictions for previously unseen stations.

Extreme weather and unusual conditions may be poorly represented in the historical data.

Roadworks, public events, school holidays, and socioeconomic features could provide additional context.

Technology Stack

Area

Tools

Data preparation and numerical processing

Python, pandas, NumPy

Predictive modelling and evaluation

LightGBM, scikit-learn

Model interpretation

SHAP

Interactive dashboard

Streamlit, PyDeck

Collaboration

GitHub

Team and Acknowledgements

Completed by Junior Anyakudo, Anastasia De Bondt, Darya Lukashina, and Yea Sung Kim as Group 18 at KU Leuven.

The analysis, results, and dashboard are team outputs. This personal presentation is based on the project report dated 24 May 2026 and my own account of my contributions.

The report also identifies DayaLuna/MDA_course as a code repository. The links above are provided as project references; this presentation does not duplicate the full codebase.
