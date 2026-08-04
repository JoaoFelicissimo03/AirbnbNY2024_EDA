# 🗽 NYC Airbnb Market Analysis (2024)
### An End-to-End Exploratory Data Analysis Project in Python

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?style=flat&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Viz-3776AB?style=flat)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat)

> *A complete data cleaning and exploratory analysis of New York City's 2024 Airbnb listings — uncovering pricing patterns, borough-level trends, licensing compliance, and the factors that actually drive listing prices.*

---

## 📖 Table of Contents
- [Project Overview](#-project-overview)
- [Objectives](#-objectives)
- [Dataset](#-dataset)
- [Key Findings](#-key-findings)
- [Tech Stack](#-tech-stack)
- [Repository Structure](#-repository-structure)
- [Methodology](#-methodology)
- [How to Run](#-how-to-run)
- [Future Work](#-future-work)
- [Author](#-author)

---

## 🏙️ Project Overview

New York City is one of the largest and most competitive short-term rental markets in the world. This project performs a complete **Exploratory Data Analysis (EDA)** on a 2024 snapshot of NYC Airbnb listings (20,700+ records), covering the full pipeline from raw data cleaning to statistical, geospatial, and regulatory insights.

This project is a hands-on continuation of my data analytics learning path — building on a previous Python practice project (financial markets data via `yfinance`) — applying a full cleaning and analysis workflow to a real-world, business-oriented dataset.

## 🎯 Objectives

- Perform rigorous **data cleaning**: missing values, duplicate records, and inconsistent data types.
- Conduct **univariate analysis** to understand the distribution of key variables (price, availability).
- Identify and treat **outliers** using statistical visualization (boxplots).
- Apply **feature engineering** (`price_per_bed`, cleaned `rating`, license categorization) to unlock deeper insights.
- Perform **bivariate analysis** comparing price across boroughs, room types, and license status.
- Explore **geospatial patterns** in pricing and listing density across the city.
- Investigate the **regulatory landscape** (NYC Local Law 18) by categorizing listings as Licensed, Exempt, or Unlicensed.
- Build a **correlation matrix** to test which numerical variables actually relate to price.

## 📊 Dataset

| | |
|---|---|
| **Source** | New York City Airbnb Open Data (2024 snapshot) |
| **Size** | 20,770 rows × 22 columns (raw) → 20,724 rows after cleaning |
| **Format** | CSV |

Key columns used in the analysis:

| Column | Description |
|---|---|
| `neighbourhood_group` | Borough (Manhattan, Brooklyn, Queens, Bronx, Staten Island) |
| `neighbourhood` | Specific neighborhood |
| `latitude`, `longitude` | Geographic coordinates |
| `room_type` | Entire home/apt, private room, shared room, hotel room |
| `price` | Nightly price (USD) |
| `beds` | Number of beds (used to engineer `price_per_bed`) |
| `minimum_nights` | Minimum nights required per booking |
| `number_of_reviews`, `reviews_per_month` | Review volume metrics |
| `calculated_host_listings_count` | Number of listings per host |
| `availability_365` | Days available per year |
| `license` | Raw license field, cleaned into `license_category` (Licensed / Exempt / Unlicensed) |
| `rating` | Cleaned into `rating_clean` (numeric), ~18% missing (new/unreviewed listings) |

**Engineered features:** `price_per_bed`, `rating_clean`, `license_category`.

## 🔑 Key Findings

| Theme | Finding |
|---|---|
| **Data quality** | Only ~0.2% of rows were dropped during cleaning — a very clean source dataset. Extreme outliers were found and removed from `price` (up to $100,000/night) and `minimum_nights` (up to 1,250 nights). |
| **Price by borough** | Manhattan is by far the most expensive borough (**$138.71/bed** on average), nearly **double** Staten Island (**$67.73/bed**), the cheapest. |
| **Host concentration** | Average listings-per-host is 18.87, but with a very high standard deviation (70.92) — evidence of a small number of large-scale "power hosts" operating alongside many individual single-listing hosts. |
| **Licensing (Local Law 18)** | The **"Unlicensed"** category is by far the largest across all boroughs, suggesting a significant share of the market still operates without formal registration despite regulation. |
| **Ratings vs. price** | Correlation between `rating` and `price` is just **0.098** — essentially no relationship. Guests in this market do not pay a premium for higher-rated listings. |
| **General correlations** | No numerical feature (`beds`, `minimum_nights`, `availability_365`, etc.) shows a strong linear relationship with `price`. Price is driven mainly by **categorical factors** — location and room type — not by simple numerical property attributes. |

> **Executive summary:** This analysis of the 2024 NYC Airbnb market reveals a market highly segmented by location — Manhattan charges nearly double the price-per-bed of Staten Island — and marked by a significant presence of large-scale operators. Despite Local Law 18, a substantial share of listings appear to operate unlicensed. Contrary to expectations, neither guest ratings nor simple numerical property features show a meaningful relationship with price, reinforcing that location and listing type are the primary drivers of pricing in this market.

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.10+ |
| Data Manipulation | pandas, numpy |
| Data Visualization | matplotlib, seaborn |
| Geospatial Analysis | contextily, folium |
| Environment | Jupyter Notebook |
| Version Control | Git & GitHub |

## 📁 Repository Structure

```
nyc-airbnb-eda-2024/
│
├── data/
│   ├── raw/
│   │   └── airbnb_dataset.csv
│   └── processed/
│       └── airbnb_dataset_clean.csv
│
├── dashboard/
│   └── app.py                 # Streamlit dashboard (work in progress)
│
├── airbnb_NY2024.ipynb        # Main analysis notebook
├── cluster_airbnb_map.html    # Interactive Folium cluster map
└── README.md
```

## 🔍 Methodology

| Step | Stage | Description |
|---|---|---|
| 1 | **Setup** | Import pandas, numpy, matplotlib, seaborn |
| 2 | **Load Dataset** | Read the raw CSV into a pandas DataFrame |
| 3 | **Initial Exploration** | `.head()`, `.shape`, `.info()`, `.describe()` |
| 4 | **Data Cleaning** | Handle missing values, remove duplicates, fix data types, save cleaned dataset |
| 5 | **Data Analysis** | Univariate (distributions, outliers) → Feature Engineering (`price_per_bed`, `rating_clean`, `license_category`) → Bivariate (price by borough/room type/license, correlation matrix, pairplot) → Geospatial (static context maps + interactive cluster map) |

## ▶️ How to Run

```bash
# Clone the repository
git clone https://github.com/<your-username>/nyc-airbnb-eda-2024.git
cd nyc-airbnb-eda-2024

# Install dependencies
pip install pandas numpy matplotlib seaborn contextily folium jupyter

# Launch the notebook
jupyter notebook airbnb_NY2024.ipynb
```

## 🚧 Future Work

- **Interactive Streamlit dashboard** (`dashboard/app.py`): KPIs, interactive map, and borough price comparison — scaffolded, to be finished in a follow-up iteration.
- Clean `bedrooms` and `baths` (currently mixed text values) to unlock room-count-based price analysis.
- Time-based analysis using `last_review` to identify dormant vs. active listings.

---

## 👤 Author

**João Felicíssimo**
Data Analyst
📍 Portugal

