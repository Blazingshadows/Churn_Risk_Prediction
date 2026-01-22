# Probabilistic Churn Risk Modeling for Multi-Platform Entertainment Subscriptions

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Churn Definition](#churn-definition)
- [Data Formulation](#data-formulation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Modeling Approach](#modeling-approach)
- [Evaluation Metrics](#evaluation-metrics)
- [Explainability](#explainability)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)

## Overview

Entertainment subscription services operate in a highly competitive and saturated market where users frequently maintain multiple subscriptions and switch platforms based on engagement, perceived value, pricing structures, and external contextual factors. Unlike traditional churn settings, subscription churn in entertainment platforms often manifests as gradual disengagement rather than abrupt cancellation.

This project focuses on building a **probabilistic churn prediction system** for multi-platform entertainment subscriptions. Instead of producing deterministic churn labels, the system:
- Estimates churn risk probabilities
- Maps them into actionable risk bands
- Interprets churn behavior through a time-aware and region-aware analytical framework

The project emphasizes **problem formulation**, **temporal feature design**, **explainability**, and **decision-oriented evaluation**, rather than model complexity alone.

## Problem Statement

### Objectives

The objective of this project is to predict whether a user is likely to churn from a given entertainment subscription platform within a fixed future time horizon, based on recent engagement and subscription behavior.

More specifically, the project aims to:

- Model churn as a probabilistic risk, not a binary verdict
- Identify behavioral and subscription-related drivers of churn
- Segment users into risk bands (low, medium, high) to support targeted intervention
- Analyze regional and temporal churn patterns in relation to external events using exploratory data analysis
- Frame churn prediction as an early-warning system, approximating time-to-churn through repeated short-horizon predictions

## Churn Definition

Churn is defined per **user–platform pair**.

A user is considered **churned** if, within the prediction window:
- The subscription is explicitly canceled, OR
- The user exhibits prolonged inactivity exceeding a predefined threshold

This definition allows the project to model both explicit cancellations and implicit disengagement, which are common in entertainment subscription services.

## Data Formulation

The dataset is structured in a **time-aware format**, where each row represents:
```
User × Platform × Time Window
```

### Components

- **Lookback Window**: Behavioral and subscription features aggregated over a recent fixed period (e.g., last 30 days)
- **Prediction Window**: Whether churn occurs in the subsequent fixed period (e.g., next 30 days)

This formulation avoids data leakage and aligns the model with real-world deployment scenarios.

## Exploratory Data Analysis

EDA is used to investigate observable behavioral patterns and correlational trends, **not to establish causality**.

### Key Analytical Themes

- Engagement decay and inactivity patterns preceding churn
- Price and plan-type sensitivity using observable proxies
- Impact of ad-supported vs ad-free subscription plans
- Cross-platform subscription behavior and substitution patterns
- Regional churn dynamics and temporal correlations with major external events

All findings are presented with explicit acknowledgment of limitations and confounding factors.

## Modeling Approach

### Core Task

Binary classification predicting the probability of churn within the prediction window.

### Models Used

#### Logistic Regression
- Interpretable baseline
- Directional insight into churn drivers

#### Gradient Boosted Trees (XGBoost / LightGBM)
- Primary predictive model
- Captures non-linear behavioral patterns and feature interactions

### Probabilistic Churn & Risk Bands

Rather than outputting a binary churn label, the model produces a **calibrated churn probability** for each user–platform instance.

These probabilities are mapped into risk bands:
- **Low risk**
- **Medium risk**
- **High risk**

Risk thresholds are selected based on precision–recall tradeoffs and business cost considerations, enabling actionable decision-making.

### Time-to-Churn Framing

Although the model predicts churn within a fixed horizon, repeated application over successive time windows allows churn risk to be tracked over time.

This enables:
- Approximate time-to-churn interpretation
- Visualization of churn risk trajectories for individual users
- Early identification of escalating churn risk

*Note: Formal survival analysis is acknowledged as a potential extension but is outside the scope of this project.*

## Evaluation Metrics

Model performance is evaluated using metrics aligned with churn economics:

- **Recall** – to minimize missed churners
- **Precision** – to limit unnecessary interventions
- **ROC-AUC** – overall discriminative ability
- **Precision–Recall AUC** – performance in imbalanced settings
- **Confusion matrix analysis** – cost-aware interpretation

*Note: Accuracy alone is not used as a primary metric.*

## Explainability

To ensure interpretability and trustworthiness, the project incorporates:

- **Global feature importance analysis** – What drives churn overall
- **Local, instance-level explanations using SHAP values** – Why a specific user is considered high-risk

## Tech Stack

### Programming & Environment
- Python 3.x
- Jupyter Notebook / JupyterLab

### Data Analysis & Visualization
- NumPy
- Pandas
- Matplotlib
- Seaborn

### Machine Learning
- scikit-learn
- XGBoost / LightGBM

### Explainability
- SHAP

### Version Control
- Git
- GitHub

## Project Structure

```
Churn Risk Prediction/
├── README.md
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_feature_engineering.ipynb
│   └── 03_modeling.ipynb
├── src/
│   ├── data_loader.py
│   ├── feature_engineering.py
│   └── model.py
├── data/
│   ├── raw/
│   └── processed/
├── models/
├── requirements.txt
└── .gitignore
```

---

**Project Status**: Active Development

For more information or questions, please refer to the project documentation or open an issue in the repository.
