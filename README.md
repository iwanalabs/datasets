# datasets

## Kasipa datasets

### `kasipa/ai_software_selloff_credit_risk_context.csv`
- Nasdaq Composite (FRED): https://fred.stlouisfed.org/series/NASDAQCOM
- Baa minus 10Y spread (FRED): https://fred.stlouisfed.org/series/BAA10Y
- ICE BofA US High Yield OAS (FRED): https://fred.stlouisfed.org/series/BAMLH0A0HYM2
- Post context: https://old.reddit.com/r/news/comments/1r4lflq/ailed_software_selloff_may_pose_risk_for_15/

### `kasipa/us_health_agency_trust_signals_2024_2026.csv`
- Primary report (AP): https://apnews.com/article/rfk-jr-kennedy-cdc-covid-health-trust-7ef5f0e2c6f91ce6d908cb58f9e2fcb2
- Poll references cited in report: KFF, Gallup, Annenberg Public Policy Center
- Post context: https://old.reddit.com/r/news/comments/1r4p039/trust_in_us_health_agencies_is_eroding_under_rfk/

### `kasipa/kff_federal_health_agency_confidence_jan2026.csv`
- Primary source (full wave topline): https://files.kff.org/attachment/topline-kff-health-tracking-poll-jan-2026.pdf
- Context explainer: https://www.kff.org/health-information-trust/trust-in-cdc-and-views-of-federal-childhood-vaccine-schedule-changes/
- This file includes the full “confidence in federal health agencies responsibilities” question battery reported for Jan 2026.

### `kasipa/heineken_headcount_revenue_productivity_2015_2026.csv`
- Revenue series source: https://www.macrotrends.net/stocks/charts/HEINY/heineken/revenue
- Employee count source: https://www.macrotrends.net/stocks/charts/HEINY/heineken/number-of-employees
- Post context: https://old.reddit.com/r/technology/comments/1r4p4hr/heineken_to_slash_up_to_6000_jobs_in_ai/
- Notes: historical rows use annual reported values (2015–2024). 2026 row is an event/scenario marker reflecting the announced "up to 6,000 jobs" cut.

### `kasipa/ai_selloff_credit_stress_windows_2023_2026.csv`
- Base market/credit series:
  - Nasdaq Composite (FRED): https://fred.stlouisfed.org/series/NASDAQCOM
  - Baa minus 10Y spread (FRED): https://fred.stlouisfed.org/series/BAA10Y
  - ICE BofA US High Yield OAS (FRED): https://fred.stlouisfed.org/series/BAMLH0A0HYM2
- Post context: https://old.reddit.com/r/news/comments/1r4lflq/ailed_software_selloff_may_pose_risk_for_15/
- Notes: derived 21-trading-day windows from daily data. Includes Nasdaq 21d return and simultaneous credit spread changes to classify risk-off vs mixed vs risk-on periods.

### `kasipa/ai_credit_regime_share_by_quarter_2023_2026.csv`
- Derived from: `kasipa/ai_selloff_credit_stress_windows_2023_2026.csv`
- Post context: https://old.reddit.com/r/news/comments/1r4lflq/ailed_software_selloff_may_pose_risk_for_15/
- Notes: quarterly share (%) of windows classified as Risk-off stress, Risk-on relief, and Mixed/neutral.
