# Probabilistic Churn Risk Modeling for Entertainment Subscription Services

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

## Overview

Entertainment subscription services face persistent customer churn driven not only by explicit cancellations but also by gradual disengagement, declining usage, and contextual factors such as pricing structures and external events. Unlike transactional churn settings, churn in streaming platforms is often preceded by behavioral decay over time, making early detection critical.

This project develops a **probabilistic churn risk modeling framework** using a single publicly available subscription dataset as a representative proxy for entertainment streaming services. The goal is not platform-specific prediction, but to:
- Analyze churn dynamics
- Quantify churn risk
- Design an early-warning system that can inform retention strategies

The emphasis of this project is on **problem formulation**, **temporal modeling**, **interpretability**, and **decision-oriented evaluation**, rather than on dataset breadth or model complexity.

## Problem Statement

The objective of this project is to predict the likelihood that a subscriber will churn within a fixed future time horizon based on recent engagement and subscription behavior.

### Objectives

Specifically, the project aims to:

- Estimate probabilistic churn risk instead of deterministic churn labels
- Segment users into actionable churn risk bands
- Identify behavioral and subscription-related drivers of churn
- Frame churn prediction as an early-warning system through time-aware modeling
- Explore regional and temporal churn patterns using exploratory data analysis while avoiding causal claims

## Churn Definition

Churn is defined at the **user level**.

A user is considered **churned** if, within the prediction window:

- The subscription is explicitly canceled, OR
- The user exhibits prolonged inactivity exceeding a predefined threshold

This definition captures both explicit churn and implicit disengagement, which are common in entertainment subscription services.

## Data Formulation

The dataset is structured in a **time-aware format**, where each observation represents:

```
User × Time Window
```

### Components

- **Lookback Window**: Aggregated behavioral and subscription features from a recent fixed period (e.g., last 30 days)
- **Prediction Window**: Whether churn occurs in the subsequent fixed period (e.g., next 30 days)

### Key Properties

This formulation ensures:

- No data leakage
- Realistic deployment alignment
- Meaningful early churn detection

The dataset is treated as representative of entertainment subscription behavior, consistent with standard academic practice.

## Exploratory Data Analysis

EDA focuses on identifying observable behavioral patterns and correlational trends, **not causal relationships**.

### Key Analytical Themes

- Engagement decay and inactivity patterns preceding churn
- Sensitivity to pricing and subscription plan types using observable proxies
- Impact of ad-supported versus ad-free plans (where applicable)
- Tenure-based churn dynamics
- Regional churn pattern variation and temporal correlations with major external events

All EDA findings explicitly acknowledge data limitations and potential confounding factors.

## Modeling Approach

### Core Task

**Binary classification** predicting the probability of churn within the prediction window.

### Models Used

#### Logistic Regression
- Interpretable baseline
- Directional insight into churn drivers

#### Gradient Boosted Trees (XGBoost / LightGBM)
- Primary predictive model
- Captures non-linear engagement decay and feature interactions

*Note: Deep learning sequence models are intentionally excluded to maintain interpretability and scope control.*

### Probabilistic Churn & Risk Band Segmentation

Rather than outputting a binary churn decision, the model produces a **calibrated churn probability** for each user.

These probabilities are mapped into risk bands:
- **Low risk**
- **Medium risk**
- **High risk**

Risk thresholds are selected using precision–recall tradeoffs and business cost considerations, enabling targeted retention actions.

### Time-to-Churn Framing

Although the model predicts churn within a fixed horizon, repeated application across successive time windows allows churn risk to be tracked longitudinally.

This enables:
- Approximate time-to-churn interpretation
- Visualization of churn risk trajectories
- Identification of accelerating disengagement patterns

*Note: Formal survival analysis is acknowledged as a potential extension but is outside the scope of this project.*

## Evaluation Metrics

Model performance is evaluated using **churn-appropriate metrics**:

- **Recall** – Minimizing missed churners
- **Precision** – Avoiding unnecessary interventions
- **ROC-AUC** – Overall discriminative ability
- **Precision–Recall AUC** – Performance in imbalanced settings
- **Confusion matrix analysis** – Cost-aware interpretation

*Note: Accuracy is not used as a primary metric due to class imbalance and asymmetric error costs.*

## Explainability

To ensure transparency and trustworthiness:

- **Global feature importance analysis** is conducted
- **Local, instance-level explanations** are generated using SHAP values

This enables understanding both:
- Overall churn drivers
- Individual-level churn risk explanations

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

---

**Status**: Active Development  
**Last Updated**: January 2026