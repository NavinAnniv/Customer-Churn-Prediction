# QuickBasket Customer Churn: Client Brief

Hi, I'm the Head of Growth at **QuickBasket**, a quick-commerce grocery delivery startup operating in six Indian cities. Here is what's going on and what I need from you. The data is in `quickbasket_customer_data.csv`.

## The situation

- We deliver groceries in about 30 minutes from dark stores (mini-warehouses) in Bengaluru, Mumbai, Delhi, Hyderabad, Chennai and Pune.
- Over the last two quarters, **customer churn has risen to roughly 1 in 4 customers** (no order within 60 days).
- Our marketing spend is up 35%, but net active customers are flat. We're paying to acquire people who then leave.
- The board has asked for a plan next month. Different teams blame different things:
  - Marketing says the product experience is bad.
  - Operations says marketing is bringing in low-quality customers.
  - Finance says our delivery fees are driving people away.
  - Support says they're overwhelmed.

I don't know who is right, and I don't want opinions. I want evidence.

## What I need from you

1. **Understand the problem.** Explore the data and tell me what is actually driving churn.
2. **Build a churn prediction model** that identifies customers likely to leave in the next 60 days. Tell me how well it works and how much I should trust it.
3. **Explain the drivers.** I need reasons, not just scores. Rank the factors, and tell me whether the problem is concentrated in specific segments, cities, warehouses or channels.
4. **Recommend actions.** For each finding, tell me what we should do, who should own it, and roughly what impact to expect. Include a retention strategy for customers flagged as high risk.
5. **Be honest about limitations**, such as data quality, bias and what the data can't tell us.

## Dataset

**File:** `quickbasket_customer_data.csv`
**Size:** 6,030 rows and 27 columns, one row per customer, captured as of 30 Sep 2026.
**Target:** `churned_next_60d`, which is 1 if the customer placed no order in the 60 days after that date.

| Column | Description |
|---|---|
| `customer_id` | Unique customer ID |
| `signup_date` | Date the customer joined |
| `city`, `warehouse_id` | Customer's city and the dark store that serves them |
| `age`, `gender` | Demographics |
| `acquisition_channel` | organic, search_ads, paid_social, referral, influencer_promo |
| `first_order_discount_pct` | Discount given on the first order |
| `membership_plan` | none, basic, premium |
| `tenure_days` | Days since signup |
| `orders_last_90d` | Number of orders in the last 90 days |
| `avg_order_value_inr` | Average basket value in ₹ |
| `avg_delivery_fee_inr` | Average delivery fee paid in ₹ |
| `avg_delivery_time_min` | Average delivery time in minutes |
| `late_delivery_pct` | % of orders delivered later than promised |
| `order_cancellation_pct` | % of orders cancelled |
| `missing_or_wrong_items_pct` | % of orders with missing or wrong items |
| `support_tickets_90d` | Support tickets raised in the last 90 days |
| `avg_ticket_resolution_hrs` | Average hours to resolve tickets (blank if no tickets) |
| `last_csat_score` | Last satisfaction score, 1 to 5 (about 35% blank, as many customers skip the survey) |
| `app_store_rating_given` | App store rating the customer gave, 1 to 5 (mostly blank) |
| `app_sessions_per_week` | Average weekly app sessions |
| `coupon_usage_pct` | % of orders where a coupon was used |
| `preferred_payment` | UPI, Credit Card, Debit Card, Wallet, Cash on Delivery |
| `top_category` | Most purchased category |
| `days_since_last_order` | Days since the last order as of 30 Sep 2026 |
| `churned_next_60d` | **Target.** 1 = churned, 0 = retained |

## Known data caveats

This is real-world data, so it isn't clean:

- Some missing values in `age`, `gender` and `avg_order_value_inr`, and the structural blanks described above.
- A few extreme outliers in order value that look like data-entry errors.
- A small number of duplicated customer rows.
- Churn is **imbalanced**, at roughly 23% churned and 77% retained.
- Several features are correlated with each other, so be careful interpreting them.

## Constraints and expectations

- **Business metrics:** Wrongly offering a ₹150 retention coupon to a customer who would have stayed costs us money. Missing a likely churner costs us their lifetime value, which is about ₹3,000. Please choose and justify your evaluation metric and decision threshold with that cost in mind.
- **Explainability:** I need to present this to non-technical executives, so explainability matters more than squeezing out the last 0.5% of accuracy.
- **Deliverables:**
  - A short written report with findings and recommendations.
  - Your notebook or code.
  - 3 to 5 key charts.
  - A one-page executive summary.

One caution: think about whether any feature might **leak** information about the target. I'd like to hear your reasoning on that.

I'll be available for questions while you work. When you're ready, present your findings and I'll tell you whether they match what I'm seeing on the ground.


===============================================================================
## Suggested ML approach (optional)

You're the expert, but you might consider:

- EDA and data cleaning
- Handling class imbalance
- Baseline logistic regression, then tree-based models (Random Forest, XGBoost or LightGBM)
- Cross-validation, ROC-AUC, PR-AUC, precision and recall
- Feature importance and SHAP
- Customer segmentation (for example, clustering)
- Threshold tuning against cost
