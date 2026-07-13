Level 1 (Basic) — Data Import, Cleaning & EDA
Imported and validated the Iris dataset (zero missing values, balanced classes).
Descriptive statistics and a petal-length vs. petal-width scatter plot confirmed clear species separability using petal measurements.
Level 1–2 — Data Modeling & Regression (Housing)
Correlation analysis identified RM (rooms) and LSTAT (% lower-status population) as the strongest drivers of home value.
A linear regression model reached R² = 0.67 and MAE ≈ $3,190 on a held-out test set.
 Level 2 (Intermediate) — Data Modeling, Relationships & DAX
Built a star-schema model: DimState, DimDate, DimPlatform → FactChurn, FactHousing, FactSentiment (one-to-many relationships).
Core DAX measures: Total Customers, Churn Rate, Avg Likes per Post, plus YTD/MTD/QTD time-intelligence measures on the Sentiment fact table.
Dax
Churn Rate = DIVIDE([Churned Customers], [Total Customers], 0)
Level 2 — Business Analytics: Customer Churn
Merged the 80/20 churn split into a single 3,333-record dataset.
International-plan customers churn at 3.5× the rate of those without one; churn rises sharply after 4+ customer service calls.
A Random Forest classifier reached 95.2% accuracy; top predictors were total day minutes, total day charge, and customer service calls.
Level 3 (Advanced) — Advanced DAX
Dax
State Churn Rank = RANKX(ALL(FactChurn[State]), [Churn Rate], , DESC, Dense)

Churn Risk Category =
VAR CurrentRate = [Churn Rate]
RETURN
    SWITCH(
        TRUE(),
        CurrentRate >= 0.30, "High Risk",
        CurrentRate >= 0.15, "Medium Risk",
        "Low Risk"
    )
Level 3 — Row-Level Security (RLS)
Static role example: Regional Manager restricted to [State] IN {"NY","NJ","MA","CT"}.
Dynamic role using USERNAME() mapped through a UserRegion table so one rule serves every manager.
Validated with Power BI Desktop's "View as Role" before publishing.
Level 3 — Automation
Since this project was developed and validated in Power BI Desktop (no Pro/Premium workspace to publish to), the automation concept was designed around a file-based trigger instead of a published dataset:
A Power Automate cloud flow watches the source CSV/Excel file in OneDrive/SharePoint (When a file is modified).
On change, it re-checks churn rate and posts a Microsoft Teams / email alert to the Retention Team.
Locally, the same idea is demoed with the Power Automate visual inside the .pbix, triggered on a button click rather than a schedule.
Level 3 — Sentiment Analysis
Instagram posts had the highest average engagement (~45 likes/post) vs. ~42 for Twitter and Facebook.
Positive-sentiment posts consistently out-performed neutral/negative posts on engagement across all platforms.
# PowerBI #CodvedaJourney #CodvedaExperience #FutureWithCodveda
internship project
