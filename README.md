# Energy Consumption Analysis System

A Python program that analyzes electricity consumption, cost, and usage patterns for a simulated set of Nigerian electricity customers, built using core Python fundamentals: variables, lists, dictionaries, loops, conditionals, functions, and nested while loops.

## Problem Statement

Africa faces a major electricity access and affordability gap. The IEA estimates around 600 million people in Africa still lack electricity access, and even where connections exist, affordability remains a major barrier. Nigeria illustrates this: substantial generation resources exist, yet availability and consumption don't always translate into reliable, affordable access for all users. Closing that gap depends partly on organizations being able to understand *how* electricity is actually being consumed: by whom, where, how much it costs, and which customers need attention. Many organizations collecting consumption data don't have a simple system for turning those records into decision-useful insight.  Without structured analysis, large volumes of consumption records remain individual data points rather than a clear picture of demand, customer segments, or cases needing further investigation.

## Project Objective

The major aim of this project is to develop a Python-based Energy Consumption Analysis System that analyzes structured electricity-consumption records and provides useful insights into consumption, electricity cost, customer groups, locations, and usage patterns.

Objectives:

1. Structure electricity-consumption records using Python lists and dictionaries.
2. Validate the dataset for missing IDs, invalid values, and inconsistent records.
3. Calculate total, average, maximum, and minimum consumption.
4. Analyze individual and overall electricity cost based on consumption and tariff.
5. Classify customers by consumption level and identify highest/lowest consumers.
6. Analyze consumption by location, customer type, and month.
7. Identify high-attention customers using defined analytical criteria.
8. Build an interactive menu system that runs until the user chooses to exit.
9. Demonstrate Python fundamentals applied to an industry problem, as a foundation for a future CSV/Pandas upgrade.

Basically, build a menu-driven Python system that takes electricity consumption records and answers practical analyst questions:

- Who is consuming electricity, and how much?
- How much does that consumption cost?
- Which locations and customer types consume the most?
- Which customers need further attention?
- How efficient or affordable is each customer's usage?

## Industry Context

Reliable electricity supports businesses, schools, hospitals, agriculture, and households — when it's unavailable, unreliable, or unaffordable, the effects extend beyond the electricity sector. Nigeria's Rural Electrification Agency and programs such as the Nigeria Electrification Programme and DARES are actively working to expand access through mini-grids and distributed solar. This project's industry relevance spans several areas: energy planning (understanding demand across locations and customer groups), energy efficiency (flagging unusually high consumption), renewable energy planning (finding high-demand customers with low renewable share), infrastructure and access planning, electricity cost and affordability, business intelligence for utilities, and evidence-based decision-making more broadly. Data analysis plays a supporting role in that effort: it's how organizations identify which customers or locations have unusually high consumption, low renewable share, or high electricity cost relative to income, and where energy-efficiency or renewable interventions would matter most.
 
## Dataset

- **20 simulated customer records**, each representing one customer's monthly electricity activity.
- Fields: `customer_id`, `customer_name`, `customer_type`, `location`, `month`, `consumption_kwh`, `tariff_per_kwh`, `peak_consumption_kwh`, `renewable_share`, `outage_hours`, `payment_status`.
- Customer types: Residential, SME, Industrial, Hospital, School, Agricultural.
- Locations: Lagos, Abuja, Ibadan.
- Months covered: January–June.
- **This is a simulated dataset**, embedded directly in the Python program as a list of dictionaries. It is not sourced from an official utility or regulator and should not be read as representing actual Nigerian electricity statistics.

### Data Dictionary

| Field | Type | Description |
|---|---|---|
| customer_id | String | Unique customer identifier |
| customer_name | String | Customer name/alias |
| customer_type | String | Customer category |
| location | String | Customer location |
| month | String | Month of observation |
| consumption_kwh | Integer | Electricity consumed |
| tariff_per_kwh | Integer | Cost per unit of electricity |
| peak_consumption_kwh | Integer | Consumption during peak period |
| renewable_share | Integer | Renewable-energy percentage |
| outage_hours | Integer | Recorded outage hours |
| payment_status | String | Payment status |

## Methodology

- **Data structure:** the dataset is a list of dictionaries (`energy_data`), with no CSV or Pandas dependency at this stage.
- **Totals and averages** (consumption, cost) were computed by looping through the list and accumulating values in running variables.
- **Extremes** (highest/lowest consumer) were found by initializing a reference record and comparing every other record against it.
- **Grouped analysis** (by location, customer type, month) used a pre-populated dictionary of categories, with each customer's consumption added to the matching key inside a loop — a group-accumulate-compare pattern applied consistently across all three breakdowns.
- **Classification** split customers into Low (<500 kWh), Medium (500–999 kWh), and High (≥1,000 kWh) bands using `if/elif/else`.
- **High-Attention flag** combined two conditions with `and`: consumption ≥1,000 kWh **and** renewable share below 15%.
- **Data validation** checks for duplicate customer IDs, missing fields, negative consumption, and out-of-range renewable share before analysis runs.
- **Program structure:** all calculations are wrapped in functions and driven by a `while`-loop menu that runs until the user selects Exit. A nested `while` loop powers a location → customer-type sub-menu, so an analyst can investigate combinations like Lagos + SME without returning to the main menu each time.
- **Extended analysis** (challenge tasks): an Efficiency Score (0–100, based on consumption band, renewable share, and outage exposure), a Top 10 customers ranking built with a bubble sort, a consumption-vs-outage comparison, and an energy affordability model (electricity cost as a percentage of an assumed ₦150,000 monthly income).

## Analysis & Key Findings

**Overall:** 20 customers, 24,240 kWh total consumption, 1,212 kWh average per customer, ₦2,920,000 total electricity cost.

1. **Industrial customers account for the largest share of consumption** — 9,600 of 24,240 kWh (about 40%) from just 3 records. The top 3 spots in the Top-10 ranking are all Industrial accounts.
2. **Consumption volume and attention risk aren't the same thing.** 9 of 20 customers fall into the High classification band, but only 4 are flagged High-Attention (Prime Plastics, Lakeside Hotel, Naija Foods Ltd, Industrial Works Ltd) — all Industrial or SME, all pairing high consumption with renewable share below 15%.
3. **Lagos consumes the most by location, but not by a wide margin** — Lagos 9,760 kWh, Abuja 8,090 kWh, Ibadan 6,390 kWh. Demand is fairly distributed rather than concentrated in one location.
4. **Higher outage exposure corresponds with lower recorded consumption.** Customers with fewer than 10 outage hours averaged 2,152 kWh, versus 898.67 kWh for customers with 10 or more outage hours.
5. **Electricity cost is a heavy burden for a meaningful share of customers.** Using an assumed ₦150,000 monthly income, 7 of 20 records (35%) fall into the "High Burden" affordability category (cost above 100% of assumed income) — including all 3 Industrial records.
6. **Monthly totals don't show a clean trend** (Jan 2,580 → Feb 1,940 → Mar 6,050 → Apr 2,200 → May 3,750 → Jun 7,720). Since each customer appears in only one month, this reflects which customers were sampled that month rather than real seasonal demand.

## Business Recommendations

1. Promote energy-efficiency practices among high-consuming customers, encouraging adoption of efficient equipment to reduce unnecessary use and cost.
2. Prioritize the 4 flagged High-Attention customers for detailed energy-efficiency or renewable-integration review, since they combine the highest consumption with the lowest renewable share.
3. Promote energy-efficiency practices among high-consuming customers, encouraging adoption of efficient equipment to reduce unnecessary use and cost.
4. Investigate why Industrial customers show such low renewable share relative to their consumption volume — this is where renewable-energy or solar interventions would likely have the most impact.
5. Since High-classified customers (9) outnumber High-Attention flagged customers (4) by more than double, consider whether the attention rule should also catch large non-industrial consumers, such as hospitals, which are high-consumption but currently exempt because of their renewable share.
6. Expand the location and customer-type breakdown into a cost view, not just a consumption view, to show whether high-consumption groups are also the highest-cost groups.
7. Improve the dataset for future analysis — use a larger, more representative dataset covering a longer period, more customer records, and additional variables.
8. Investigate the outage-consumption relationship further before drawing conclusions — lower recorded consumption during high-outage periods could reflect suppressed demand rather than genuinely lower need.
9. Use the Efficiency Score, not just the consumption ranking, to prioritize interventions — it also accounts for renewable share and outage exposure, which the Top-10 list alone does not.
10. Revisit the affordability model before using it operationally: applying one flat ₦150,000 income assumption to Industrial and commercial accounts (which are billed as businesses, not households) overstates their affordability burden.

## Limitations

1. The dataset is simulated for this analysis purposes and does not represent official Nigerian electricity statistics.
2. Only 20 records span 6 months, with each customer appearing in a single month — this rules out any genuine month-over-month trend analysis for an individual customer.
3. The attention-flag rule is a single fixed threshold (consumption ≥1,000 kWh and renewable share <15%), a reasonable starting rule but not validated against real utility risk criteria.
4. The affordability model assumes one flat monthly income (₦150,000) applied uniformly across all customer types, including commercial and industrial accounts, which does not reflect real income or billing structures.
5. The outage-consumption comparison is based on a small sample (20 records split into two groups), which limits confidence in the conclusion.
   


## Conclusion

The Energy Consumption Analysis System successfully demonstrated how Python can be used to organize, process, and analyze electricity consumption data. Using a structured dataset of 20 customer records, the system calculated total and average electricity consumption, identified high- and low-consuming customers, classified customers by consumption level, compared consumption across locations and customer types, examined monthly consumption patterns, analyzed electricity cost, and identified customers requiring higher attention. Although developed using a small simulated dataset and basic Python programming concepts, the project demonstrates the value of data analysis in understanding energy-consumption patterns, and provides a foundation that can be expanded with larger datasets, additional variables, and more advanced analytical techniques.

## Future Improvements

1. Upgrade to a file-based version that reads consumption records from CSV, then migrate to Pandas for larger-scale analysis and visualization.
2. Expand the dataset to 100–300+ records with repeated monthly readings per customer to support real trend analysis.
3. Separate the affordability model into household-income and business-revenue variants instead of one flat assumption.
4. Integrate real smart-meter or NERC-published data once file handling and data-cleaning techniques have been covered.

## System Features

- Menu-driven interface (13 options): view records, total/average consumption, highest/lowest consumer, electricity cost, classification, location analysis, customer-type analysis, monthly analysis, high-attention customers, and a full summary report.
- Nested while-loop sub-menu for location + customer-type investigation.
- Built-in data validation (duplicate IDs, missing fields, negative values, out-of-range values).
- Efficiency Score, Top 10 customers (bubble sort), outage-vs-consumption comparison, and affordability classification as extended analyses.

 ## Extended Analysis 

The notebook also includes exploratory analyses built on the same 20-record dataset. These are flagged separatel for better explanation

Efficiency Score (0–100): a composite score based on consumption band, renewable share, and outage exposure.
Top 10 Customers: ranked by consumption using a bubble sort. The top 3 spots are all Industrial accounts, reinforcing Finding #1 above.
Outage vs. Consumption: customers with fewer than 10 outage hours averaged 2,152 kWh, versus 898.67 kWh for customers with 10 or more outage hours — higher outage exposure corresponds with lower recorded consumption.
Affordability Model: electricity cost as a percentage of an assumed ₦150,000 monthly income. 7 of 20 records (35%) fall into a "High Burden" category (cost above 100% of assumed income), including all 3 Industrial records.

Notes on these results:

The outage-consumption relationship is based on a small sample (20 records split into two groups) — worth investigating further before concluding it reflects suppressed demand rather than genuinely lower need.
The affordability model applies one flat income assumption across all customer types, including Industrial and commercial accounts billed as businesses rather than households — this overstates their affordability burden and should be revisited (e.g. separate household-income and business-revenue variants) before being used operationally.
System Features
Menu-driven interface (13 options): view records, total/average consumption, highest/lowest consumer, electricity cost, classification, location analysis, customer-type analysis, monthly analysis, high-attention customers, and a full summary report.
Nested while-loop sub-menu for location + customer-type investigation.
Built-in data validation (duplicate IDs, missing fields, negative values, out-of-range values).
Extended: Efficiency Score, Top 10 customers (bubble sort), outage-vs-consumption comparison, and affordability classification.

## Tech Stack

- Python 3 (standard library only — no external packages)
- Jupyter Notebook

## Project Structure

Energy_Consumption_Analysis_System/
│
├── README.md
└── Energy_Consumption_Analysis_System.ipynb

## How to Run

1. Open `Energy_Consumption_Analysis_System.ipynb` in Jupyter Notebook or JupyterLab.
2. Run all cells in order.
3. Interact with the menu system through the input prompts to explore each analysis option.

## Author

Vivian Moyosore Gomes — Geoscientist | Python Study Group, Group A Team Captain| SmartBizCrux
Collaborators
Oseni Latifat
Ismaila Ainoko Aminu
Ositadinma Chigozie
