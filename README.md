# Customer Churn Prediction Pipeline

An end-to-end machine learning pipeline that predicts which active subscription service customers are likely to churn in the next 30 days, enabling retention teams to proactively engage at-risk customers.

## 📋 Overview

This project builds a production-ready churn prediction system using synthetic subscription service data. The pipeline:

- **Generates realistic event-level data** with multiple event types (logins, usage, payments, support tickets)
- **Defines churn** based on subscription cancellations within a prediction window
- **Engineers features** from customer activity patterns before a cutoff date
- **Trains and evaluates** machine learning models to identify churners
- **Provides actionable insights** for the retention team on which customers to target

## 🎯 Key Features

### Data Generation
- **5,000 synthetic users** with realistic signup patterns (Jan 2024 - May 2025)
- **Three subscription tiers**: Basic ($10), Standard ($20), Premium ($35)
- **~10% churn rate** with activity patterns that reflect real behavior
- **Event-level tracking**: logins, usage, payments, and support tickets (~1.2M events)
- **Realistic activity decay**: Activity drops significantly before cancellation

### Churn Definition
- **Prediction window**: 30 days (June 1-30, 2025)
- **Cutoff date**: June 1, 2025
- **Features derived**: From events before the cutoff date
- **Label**: Whether customer cancelled during the prediction window

### Machine Learning
- **Feature engineering** from event-level aggregations
- **Model training and evaluation** with appropriate metrics for imbalanced data
- **Retention team metrics**: Precision, recall, and business impact analysis

## 📊 Dataset Structure

### Subscriptions Table
| Column | Type | Description |
|--------|------|-------------|
| user_id | int | Unique customer identifier |
| Signup_dates | datetime | Account creation date |
| Plans | string | Plan tier (Basic/Standard/Premium) |
| monthly_price | int | Monthly subscription cost |
| cancel_date | datetime | Cancellation date (NULL if active) |
| label | int | Target variable (1=churn, 0=retained) |

### Events Table
| Column | Type | Description |
|--------|------|-------------|
| user_id | int | Unique customer identifier |
| timestamp | datetime | Event occurrence time |
| event_type | string | Type of event (login, usage, payment, support_ticket) |

### Event Distribution
- **Login events**: 573,197 (46%)
- **Usage events**: 571,194 (46%)
- **Payment events**: 77,281 (6%)
- **Support tickets**: 23,001 (2%)

## 🔧 Usage

### Prerequisites
```bash
python >= 3.8
pandas
numpy
scikit-learn
jupyter
```

### Running the Pipeline

1. **Open the notebook**:
   ```bash
   jupyter notebook customer_churn_prediction_pipeline.ipynb
   ```

2. **Execute cells sequentially**:
   - Data generation (subscriptions and events)
   - Feature engineering from event-level data
   - Train/test split
   - Model training
   - Evaluation and metrics

3. **Interpret results**:
   - Model performance metrics (accuracy, precision, recall, F1)
   - Feature importance analysis
   - Business recommendations for retention outreach

## 📈 Expected Results

The pipeline typically achieves:
- **Recall (sensitivity)**: Identifies ~70-80% of customers who will churn
- **Precision**: ~15-25% of flagged customers actually churn (baseline 1.5%)
- **Business impact**: 10-15x lift over random selection for retention campaigns

## 🔑 Key Insights

### Churn Signals
The model identifies these patterns as strong churn indicators:
- **Declining login frequency** in the 60+ days before cancellation
- **Reduced platform usage** compared to historical baseline
- **Payment issues** or failed transactions
- **Support ticket escalations** without resolution
- **Inactive periods** lasting 30+ days

### Retention Strategy
Use model predictions to:
1. **Segment customers** by churn risk (high/medium/low)
2. **Prioritize outreach** to high-risk, high-value customers
3. **Personalize interventions** based on churn drivers
4. **Track engagement metrics** to measure campaign effectiveness

## 📁 Files

- **`customer_churn_prediction_pipeline.ipynb`** - Complete Jupyter notebook with data generation, feature engineering, model training, and evaluation
- **`README.md`** - This documentation
- **`LICENSE`** - Apache 2.0 license

## 🚀 Extension Ideas

- **Real data integration**: Replace synthetic data with production customer events
- **Incremental learning**: Retrain models weekly/monthly with recent data
- **Feature store**: Build a feature engineering pipeline with scheduled recomputation
- **A/B testing**: Test different retention strategies with holdout cohorts
- **Explainability**: Add SHAP or LIME for per-customer prediction explanations
- **Production deployment**: REST API for batch predictions and real-time scoring

## 📚 Methodology

### Feature Engineering
Features are aggregated from events in the 30-90 day window before the cutoff date:
- **Frequency metrics**: Total logins, usage events, payments
- **Recency metrics**: Days since last activity
- **Temporal patterns**: Activity variance and trends
- **Engagement score**: Composite measure of platform usage

### Model Training
- **Algorithm**: Logistic Regression, Random Forest, or Gradient Boosting
- **Class balancing**: Handle 1.5% churn rate with class weights or resampling
- **Cross-validation**: Stratified K-fold to preserve class distribution
- **Hyperparameter tuning**: Grid/random search with evaluation metrics

## 💡 Business Context

This pipeline solves a real retention problem: identifying customers at risk of cancellation before they leave. Unlike reactive churn analysis, this predictive approach enables:
- **Proactive engagement** with at-risk customers
- **Resource optimization** by targeting high-value customers
- **Trend detection** to identify systemic product issues
- **ROI measurement** for retention campaigns

## 📝 License

Apache License 2.0 - See LICENSE file for details

## 👤 Author

Created by Kiran Karakalli

## 📧 Questions or Feedback?

Feel free to open an issue or reach out with suggestions for improving the pipeline.

---

**Last Updated**: July 2026
