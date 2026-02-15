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

### `kasipa/china_imports_from_africa_2023.csv`
- Primary data source: TrendEconomy data explorer (annual trade by country, HS)
  - Page: https://trendeconomy.com/data/h2/China/TOTAL
  - Backend endpoint used for extraction: `https://trendeconomy.com/te.rest.web/json/key_family`
- Build parameters used:
  - reporter = China
  - trade_flow = Import
  - indicator = Trade Value (TV)
  - commodity = TOTAL
  - time_period = 2023
- Notes: filtered to African partner countries from the returned partner-country rows.

### `kasipa/china_imports_from_africa_2023_with_country_tariff_proxy.csv`
- Base trade dataset: `kasipa/china_imports_from_africa_2023.csv`
- Tariff proxy source: World Bank indicator API
  - Indicator: `TM.TAX.MRCH.WM.AR.ZS` (Tariff rate, applied, weighted mean, all products, %)
  - API docs root: https://api.worldbank.org/
  - Example endpoint format: `https://api.worldbank.org/v2/country/{ISO3}/indicator/TM.TAX.MRCH.WM.AR.ZS?format=json`
- Notes:
  - Adds latest available country-level tariff value/year per country.
  - This is a country-level proxy and not a China bilateral HS-line tariff schedule.

### `kasipa/china_zero_tariff_opportunity_2023.csv`
- Built from: `kasipa/china_imports_africa_tariff_quadrant.csv`
- Upstream raw/indicator sources used in parent dataset:
  - China import values by African partner (TrendEconomy):
    - Page: https://trendeconomy.com/data/h2/China/TOTAL
    - Backend endpoint: `https://trendeconomy.com/te.rest.web/json/key_family`
  - Tariff proxy (World Bank):
    - Indicator: `TM.TAX.MRCH.WM.AR.ZS`
    - API root: https://api.worldbank.org/
  - Export dependency proxy (World Bank):
    - Indicator: `NE.EXP.GNFS.CD`
    - API root: https://api.worldbank.org/
- Post context:
  - https://old.reddit.com/r/Economics/comments/1r549cv/china_to_implement_zero_tariffs_on_imports_from/
- Notes:
  - Adds derived fields for opportunity framing:
    - `estimated_tariff_cost_usd_billion`
    - `estimated_tariff_cost_usd`
    - `opportunity_score`

### `kasipa/global_ewaste_monitor_2024_country_2022.csv`
- Primary source report:
  - Global E-waste Monitor 2024 (UNITAR/ITU), Annex 2 country table
  - PDF: https://ewastemonitor.info/wp-content/uploads/2024/12/GEM_2024_EN_11_NOV-web.pdf
  - Landing page: https://ewastemonitor.info/the-global-e-waste-monitor-2024/
- Additional joined source:
  - World Bank GDP per capita (current US$), indicator `NY.GDP.PCAP.CD`
  - API root: https://api.worldbank.org/
- Notes:
  - Extracted from Annex 2 Table A2.4 (country-level key e-waste statistics, reference year 2022).
  - Includes: generated total (million kg), generated per-capita (kg), documented formally collected/recycled (million kg, when available), region, plus `gdp_per_capita_usd` and `gdp_per_capita_year`.

### `kasipa/atus_a8_2024_waking_hours_selected_characteristics.csv`
- Primary source:
  - U.S. Bureau of Labor Statistics (BLS), American Time Use Survey (ATUS)
  - Table A-8: Waking hours spent alone or with others, by selected characteristics, 2024 annual averages
  - PDF: https://www.bls.gov/tus/tables/a8-2024.pdf
  - Tables index: https://www.bls.gov/tus/tables.htm
- Notes:
  - Manually transcribed from the A-8 table values in the source PDF.
  - Contains selected rows for age, sex, race/ethnicity, employment status, household-children status, marital status, day type, and education.

### `kasipa/china_imports_all_african_countries_2023_double_checked.csv`
- Base import source:
  - TrendEconomy China imports (reporter=China, trade_flow=Import, indicator=TV, commodity=TOTAL, time_period=2023)
  - Page: https://trendeconomy.com/data/h2/China/TOTAL
  - Backend endpoint used: `https://trendeconomy.com/te.rest.web/json/key_family`
- Tariff context source (proxy):
  - World Bank indicator `TM.TAX.MRCH.WM.AR.ZS` (country applied weighted mean tariff, all products)
  - API root: https://api.worldbank.org/
- Notes:
  - Covers all 54 African Union member states with ISO3.
  - Import values are China imports from each country in 2023; countries with no observed value in source are set to 0.
  - Tariff column is a country-level proxy and **not** a China bilateral tariff schedule by partner/product line.
