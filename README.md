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

### `kasipa/us_debt_spiral_projection_2025_2036.csv`
- Primary context thread: https://old.reddit.com/r/Economics/comments/1r5tmu0/a_us_debt_spiral_could_start_soon_as_the_interest/
- Base source article: https://fortune.com/2026/02/14/us-debt-spiral-interest-rate-treasury-bond-yields-economic-growth-gdp/
- Macro source series (FRED):
  - Debt-to-GDP proxy: https://fred.stlouisfed.org/series/GFDEGDQ188S
  - Nominal GDP index: https://fred.stlouisfed.org/series/GDPC1
  - 10Y Treasury proxy: https://fred.stlouisfed.org/series/DGS10
- Notes:
  - Contains mixed historical rows (2000–2026 quarterly aggregates) and anchor projections from the article (debt-to-GDP and nominal growth/interest-rate assumptions).
  - Historical values are pulled as-is from FRED series CSV endpoints; projection points are manually aligned to article projections for charting context.

### `kasipa/pertussis_dtp1_dtp3_coverage_1980_2024.csv`
- Source endpoints (Our World in Data grapher, WHO/UNICEF 2025 and UN WPP 2024 variants):
  - DTP1 coverage: `https://ourworldindata.org/grapher/vaccination-coverage-who-unicef.csv?antigen=dtpcv1&metric=coverage`
  - DTP3 coverage: `https://ourworldindata.org/grapher/vaccination-coverage-who-unicef.csv?antigen=dtpcv3&metric=coverage`
- Purpose: compare first-dose and third-dose pertussis vaccine coverage over time.
- Post context to anchor the chart narrative: https://www.abc.net.au/news/2026-02-16/whooping-cough-cases-at-record-high-level-in-australia/106332954
- Notes: includes global/WHO-region and selected-country rows, plus `dtp3_minus_dtp1_pct_gap` to show completion gap.

### `kasipa/taklamakan_climate_monthly_2000_2025.csv`
- Primary source: NASA POWER MERRA-2 Monthly Point Data API
  - Endpoint: `https://power.larc.nasa.gov/api/temporal/monthly/point`
- Parameters used: `T2M` (2m temperature), `PRECTOTCORR` (precipitation), `EVPTRNS` (evapotranspiration)
- Point location used: Taklamakan Desert center (40.5°N, 84.9°E)
- Window: 2000–2025
- Notes: includes seasonal tagging (`Wet (Jul-Sep)` vs `Dry (Oct-Jun)`) for a climate-regime comparison tied to restoration timing discussion in the Taklamakan restoration literature.

### `kasipa/taklamakan_climate_seasonal_annual_2000_2025.csv`
- Derived from: `kasipa/taklamakan_climate_monthly_2000_2025.csv`
- Source API call example:
  - `https://power.larc.nasa.gov/api/temporal/monthly/point?parameters=T2M,PRECTOT,EVPTRNS&community=AG&longitude=84.9&latitude=40.5&start=2000&end=2025&format=JSON`
- Derived fields:
  - `wet_season_precip_mm_per_day`: mean monthly precip in Jul-Sep
  - `dry_season_precip_mm_per_day`: mean monthly precip in Oct-Jun
  - `wet_minus_dry_precip_mm_per_day`: seasonal contrast (wet-dry) for regime strength
- Angle: track whether the wet-season advantage has strengthened as a practical framing clue for afforestation feasibility.

### `kasipa/japan_growth_trade_fx_1990_2025.csv`
- Core sources (World Bank API, indicator endpoint):
  - GDP growth (annual %): `https://api.worldbank.org/v2/country/JPN;USA/indicator/NY.GDP.MKTP.KD.ZG?format=json`
  - Exports of goods and services (current US$): `https://api.worldbank.org/v2/country/JPN;USA/indicator/NE.EXP.GNFS.CD?format=json`
  - Official exchange rate (JPY per US$): `https://api.worldbank.org/v2/country/JPN/indicator/PA.NUS.FCRF?format=json`
- Country set: Japan (JPN) and United States (USA)
- Window: 1990–2025
- Notes: derived exports YoY growth for both Japan and U.S., plus JPY-per-USD to test the “Japan weak-growth + soft yen + export cooling” narrative from a macro lens.
- Posted context candidate: `https://old.reddit.com/r/Economics/comments/1r6afvv/japans_economy_barely_grows_in_the_last_quarter/`

### `kasipa/china_new_home_prices_70cities_jan2026_snapshot.csv`
- Primary monthly aggregate source (NBS series mirror):
  - TradingEconomics China housing index page: `https://tradingeconomics.com/china/housing-index`
- Official release summary source (tier-level January MoM moves):
  - SCIO/Xinhua summary: `http://english.scio.gov.cn/pressroom/2026-02/13/content_118333097.html`
  - China.org mirror: `http://www.china.org.cn/2026-02/13/content_118333030.shtml`
- City-level January YoY examples + breadth signal source references:
  - TradingEconomics news text block on the same indicator page (Guangzhou, Shenzhen, Chongqing, Tianjin, Beijing, Shanghai)
  - Reuters report URL (for 62/70 vs 58/70 breadth context): `https://www.reuters.com/world/asia-pacific/chinas-new-home-prices-extend-decline-january-2026-02-13/`
- Notes:
  - This is a compact snapshot dataset for fast visualization, not a full official 70-city January table export.
  - Includes national aggregate, selected major-city YoY points, tier-level January MoM, and a market-breadth count.

### `kasipa/china_new_home_prices_2025_only.csv`
- Primary monthly aggregate source (NBS series mirror):
  - TradingEconomics China housing index page: `https://tradingeconomics.com/china/housing-index`
- City-level Dec 2025 YoY examples:
  - TradingEconomics indicator news text on the same page (Guangzhou, Shenzhen, Tianjin, Chongqing, Beijing, Shanghai)
- Market breadth context (Dec 2025):
  - Reuters report URL (58 of 70 cities declining): `https://www.reuters.com/world/asia-pacific/chinas-new-home-prices-extend-decline-january-2026-02-13/`
- Notes:
  - Strictly 2025 values only (December snapshot).
  - Compact dataset intended for quick Kasipa charting.

### `kasipa/china_new_home_prices_nbs_dec2025_selected_cities.csv`
- Official NBS source (primary):
  - National Bureau of Statistics of China, Press Release (English):
  - `https://www.stats.gov.cn/english/PressRelease/202601/t20260119_1962346.html`
- Extraction basis:
  - Table I: "Sales Price Indices of Newly Constructed Commercial Residential Buildings in 70 Large and Medium-Sized Cities"
- Notes:
  - Uses official NBS index values for Dec 2025 (`Last Month=100` and `Same Month Last Year=100`) for selected cities.
  - Includes derived percent changes (`mom_change_percent`, `yoy_change_percent`) computed as index minus 100.

### `kasipa/china_new_home_prices_nbs_dec2025_all_70_cities.csv`
- Official NBS source (primary):
  - National Bureau of Statistics of China, Press Release (English):
  - `https://www.stats.gov.cn/english/PressRelease/202601/t20260119_1962346.html`
- Extraction basis:
  - Table I: "Sales Price Indices of Newly Constructed Commercial Residential Buildings in 70 Large and Medium-Sized Cities"
- Notes:
  - Full 70-city Dec 2025 coverage from official NBS table values.
  - Columns include NBS indices (`mom_index_last_month_100`, `yoy_index_same_month_last_year_100`, `avg_index_jan_dec_last_year_100`) and derived percentage-point deltas vs 100 (`mom_change_percent`, `yoy_change_percent`).
  - Includes one extra aggregate row: `China (simple average across 70 cities)` computed directly from NBS Table I city indices (unweighted mean; clearly labeled as derived, not an official NBS weighted national headline index).

### `kasipa/china_new_home_prices_nbs_dec2025_all_70_cities_with_population_2020_census.csv`
- Base housing source:
  - NBS Table I (same as file above): `https://www.stats.gov.cn/english/PressRelease/202601/t20260119_1962346.html`
- Population source (2020 census basis):
  - China Seventh National Census city-level urban aggregates as compiled on CityPopulation (explicitly citing NBS census web tables): `https://www.citypopulation.de/en/china/cities/`
- Notes:
  - Adds `population_2020_census` to the 70-city housing rows.
  - 4 cities currently have blank population due absence in the cited urban-aggregate table cutoff: `Anqing`, `Beihai`, `Sanya`, `Dali`.

### `kasipa/cost_wmt_tgt_indexed_1y_daily.csv`
- Price history source (Stooq CSV endpoints):
  - Costco (COST): `https://stooq.com/q/d/l/?s=cost.us&i=d`
  - Walmart (WMT): `https://stooq.com/q/d/l/?s=wmt.us&i=d`
  - Target (TGT): `https://stooq.com/q/d/l/?s=tgt.us&i=d`
- Context thread:
  - `https://old.reddit.com/r/Economics/comments/1r7bmug/costco_defied_trumps_dei_directive_as_target_and/`
- Notes:
  - Daily intersection of trading dates across all three tickers.
  - Includes raw close (`*_close_usd`) and normalized series (`*_indexed_100`) using the first date in the 1-year window as base=100.

### `kasipa/cost_wmt_tgt_indexed_1y_summary.csv`
- Derived from: `kasipa/cost_wmt_tgt_indexed_1y_daily.csv`
- Notes:
  - Compact per-ticker return summary over the same normalized window (`indexed_return_pct`).

### `kasipa/prediction_markets_cross_platform_top_markets_snapshot.csv`
- Platform API sources:
  - Polymarket Gamma API: `https://gamma-api.polymarket.com/markets?closed=false&limit=500`
  - Manifold Markets API: `https://api.manifold.markets/v0/markets?limit=1000`
- Context thread:
  - `https://old.reddit.com/r/worldnews/comments/1r71uvi/new_zealand_declares_prediction_markets_are/`
- Notes:
  - Snapshot file (single pull timestamp) with top markets by sampled volume from each platform.
  - Includes standardized columns: `volume_usd`, `liquidity_usd`, resolution state, and market URL.

### `kasipa/prediction_markets_cross_platform_activity_summary_snapshot.csv`
- Derived from: `kasipa/prediction_markets_cross_platform_top_markets_snapshot.csv` (same snapshot run)
- Notes:
  - Platform-level aggregate sample metrics (`sample_total_volume_usd`, `sample_total_liquidity_usd`, median volume, markets sampled).

### `kasipa/us_import_price_vs_cpi_monthly_2018_2026.csv`
- Primary source (FRED combined CSV endpoint):
  - `https://fred.stlouisfed.org/graph/fredgraph.csv?id=IR14200,CPIAUCSL`
- Underlying series pages:
  - U.S. Import Price Index: All Commodities (`IR14200`): `https://fred.stlouisfed.org/series/IR14200`
  - CPI for All Urban Consumers: All Items (`CPIAUCSL`): `https://fred.stlouisfed.org/series/CPIAUCSL`
- Notes:
  - Monthly rows filtered to `2018-01-01` onward where both series are present.
  - Includes derived fields:
    - `import_price_yoy_pct`
    - `cpi_yoy_pct`
    - `gap_import_minus_cpi_yoy_pp`

### `kasipa/us_customs_duties_vs_imports_quarterly_1990_2026.csv`
- Primary source (FRED combined CSV endpoint):
  - `https://fred.stlouisfed.org/graph/fredgraph.csv?id=B235RC1Q027SBEA,IMPGS`
- Underlying series pages:
  - Federal government current tax receipts: customs duties (`B235RC1Q027SBEA`): `https://fred.stlouisfed.org/series/B235RC1Q027SBEA`
  - Imports of goods and services (`IMPGS`): `https://fred.stlouisfed.org/series/IMPGS`
- Context thread:
  - `https://old.reddit.com/r/news/comments/1r9xrq7/supreme_court_strikes_down_most_of_trumps_tariffs/`
- Notes:
  - Quarterly rows filtered to `1990-01-01` onward where both series are present.
  - Includes derived fields:
    - `customs_duties_to_imports_pct`
    - `customs_duties_yoy_pct`
    - `imports_yoy_pct`
    - `duty_intensity_yoy_change_pp`

### `kasipa/tesla_recalls_ota_share_by_model_year_2020_2026.csv`
- Primary source (NHTSA recalls API):
  - Endpoint template: `https://api.nhtsa.gov/recalls/recallsByVehicle?make=TESLA&model={MODEL}&modelYear={YEAR}`
  - Example: `https://api.nhtsa.gov/recalls/recallsByVehicle?make=TESLA&model=MODEL%20Y&modelYear=2025`
- Context thread:
  - `https://old.reddit.com/r/technology/comments/1ra7jkz/youtuber_mkbhd_says_tesla_stopped_talking_to_me/`
- Notes:
  - Covers Tesla models `MODEL Y`, `MODEL 3`, `MODEL S`, `MODEL X`, and `CYBERTRUCK` for model years 2020–2026.
  - Includes derived fields:
    - `ota_recall_count`
    - `ota_share_pct`
  - Some model-year combinations are not valid in NHTSA API and return HTTP 400; those rows are retained with zero counts and a `query_error` value for transparency.
