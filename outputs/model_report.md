# FlyRank Refresh Opportunity Model Report

This report is generated from the bundled anonymized starter dataset (`data/raw/content_refresh_anonymized.csv`).
The model ranks existing content for refresh review. It does not use titles, URLs, client names, domains, or keywords.

## Data

- Rows scored: 30,000
- Declining-label rows: 16,262
- Declining-label rate: 0.542
- Split strategy used for validation: client_holdout
- Target: `is_declining_label`

## Model Comparison

Best model: `random_forest` selected by `precision_at_50`.

| Model | ROC AUC | Avg precision | Precision@50 | Recall | F1 |
|---|---:|---:|---:|---:|---:|
| decision_tree | 0.742 | 0.575 | 0.620 | 0.716 | 0.634 |
| logistic_regression | 0.700 | 0.522 | 0.400 | 0.567 | 0.566 |
| random_forest | 0.747 | 0.610 | 0.680 | 0.741 | 0.638 |
| baseline_rules | 0.627 | 0.468 | 0.240 | - | - |

## Final Queue

- High-confidence items: 3,576
- Medium-confidence items: 11,424
- Low-confidence items: 15,000
- `monitor` items: 13,069
- `refresh` items: 8,207
- `refresh_and_review_ctr` items: 6,655
- `refresh_and_review_engagement` items: 1,987
- `expand_and_refresh` items: 82

## Top Features

- `days_with_impressions`: 0.1606
- `log_impressions_90d`: 0.1285
- `avg_position`: 0.1084
- `content_age_days`: 0.0950
- `word_count`: 0.0412
- `char_count`: 0.0398
- `ctr`: 0.0332
- `log_clicks_90d`: 0.0325
- `scroll_rate`: 0.0309
- `days_with_sessions`: 0.0299

## Top 10 Queue Preview

| Rank | Score | Model probability | Action | Reasons | Impressions | Sessions | Trend |
|---:|---:|---:|---|---|---:|---:|---|
| 1 | 81.9 | 0.786 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, low_engagement_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate, engagement_review_candidate | 12834 | 66 | down |
| 2 | 81.7 | 0.792 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 8064 | 23 | down |
| 3 | 81.6 | 0.850 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 2498 | 9 | down |
| 4 | 80.8 | 0.814 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 3393 | 5 | down |
| 5 | 80.8 | 0.771 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 13790 | 27 | down |
| 6 | 80.8 | 0.848 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 1622 | 20 | down |
| 7 | 80.6 | 0.794 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 5811 | 14 | down |
| 8 | 80.4 | 0.828 | refresh | declining_with_demand, model_decline_risk, visible_model_opportunity | 4366 | 8 | down |
| 9 | 80.2 | 0.824 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, low_engagement_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate, engagement_review_candidate | 2655 | 92 | down |
| 10 | 80.1 | 0.831 | refresh_and_review_ctr | declining_with_demand, low_ctr_visible_page, model_decline_risk, visible_model_opportunity, ctr_review_candidate | 2621 | 10 | down |

## Generated Files

- `outputs/refresh_queue.csv`
- `outputs/model_results.json`
- `outputs/summary.json`
- `outputs/charts/action_mix.svg`
- `outputs/charts/confidence_mix.svg`
- `outputs/charts/top_reason_codes.svg`
- `outputs/charts/top_feature_importance.svg`
- `outputs/charts/trend_distribution.svg`

## Practical Use

Use the ranked queue as a reviewer aid, not as an automatic publishing decision.
The safest first production use is to inspect high-confidence rows, verify the page manually, and compare the recommendation against editorial context.
