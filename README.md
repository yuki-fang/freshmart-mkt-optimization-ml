# FreshMart Growth Playbook: Optimizing Pricing, Marketing Spend, & Seasonality

This project analyzes FreshMart’s sales data to optimize pricing, marketing spend, and campaign timing. Using OLS, Ridge, and Lasso regressions with stepwise selection, I identified price sensitivity, effective marketing channels, and multicollinearity effects. Seasonal modeling with LOESS, B-splines, and GAM revealed optimal timing for TikTok influencer activations to boost peaks and smooth sales valleys.

---

## Project Motivation
Understanding the drivers of sales fluctuations and marketing effectiveness helps FreshMart allocate resources efficiently, set optimal prices, and schedule campaigns to maximize revenue and engagement.

---

## Dataset
| Dataset | Description |
|---------|-------------|
| `FreshMart_sales_data_sample.csv` | Sample of FreshMart’s sales data including prices, marketing spend, campaign info, and daily sales |

### Key Variables
| Variable | Description |
|----------|-------------|
| `sales` | Daily sales revenue (target variable) |
| `product_price` | Price of FreshMart’s meal kits ($k) |
| `competitor_price` | Competitor’s meal kit price ($k) |
| `tv_ad_spend` | Daily TV ad spend ($k) |
| `email_marketing` | Daily email campaign budget ($k) |
| `social_media_spend` | Daily Instagram/Facebook ad spend ($k) |
| `is_holiday` | Indicator variable (1 = public holiday, 0 = otherwise) |
| `day_of_year` | Day of the year (for seasonality modeling) |
| `viral_campaign` | Indicator for TikTok influencer campaigns |

---

## Analysis Approach

### Part 1: Pricing Strategy
- OLS regression: `product_price`, `competitor_price`, `tv_ad_spend`, `is_holiday`  
- Ridge regression (`cv.glmnet`, 10-fold CV) to address multicollinearity  

### Part 2: Marketing Spend Optimization
- Lasso regression (`cv.glmnet`, 10-fold CV) to identify effective channels  
- Stepwise/backward OLS as alternative feature selection  
- Compare results: Lasso vs. stepwise  

### Part 3: Seasonality & TikTok Influencer Impact
- LOESS plots of `sales` vs. `day_of_year` (span 0.1–0.6)  
- B-splines (manual knots: 100, 150, 250) + controls  
- GAM with `s(day_of_year)` for automatic smoothing  
- Compare models via AIC; plot smooth terms  
- Extend best model with `viral_campaign` + interaction  
- Evaluate campaign significance & sales lift timing  

---

## Key Findings
- Price sensitivity varies across product categories, with some highly elastic items  
- Marketing effectiveness differs by channel, with social media and influencer campaigns showing strong impact  
- Seasonal modeling highlights peak periods and optimal timing for influencer activations to smooth sales valleys  

---

## Key Methods & Tools
| Category | Details |
|----------|---------|
| Methods  | OLS, Ridge, Lasso regression, Stepwise/backward feature selection, LOESS, B-splines, Generalized Additive Models (GAM), Model comparison with AIC and cross-validation |
| Tools    | RStudio (packages: *glmnet*, *splines*, *mgcv*, *stats*, *ggplot2*, *dplyr*) |

---

## How to Run
1. Clone the repository:  
```bash
git clone https://github.com/YOUR_USERNAME/freshmart-growth-ml.git
