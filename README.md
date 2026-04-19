# 🌾 Maji Ndogo Agricultural Data Analysis

**Author:** Oluwatobi Victoria Babalola | MSc Data Science  
**Portfolio:** [bbt-portfolio.vercel.app](https://bbt-portfolio.vercel.app) | **LinkedIn:** [oluwatobi-babalola-victoria](https://www.linkedin.com/in/oluwatobi-babalola-victoria/)

---

## 📌 Project Summary

A full end-to-end data analytics pipeline on a real agricultural survey database from Maji Ndogo — a diverse farming region seeking to automate crop production through data-driven decisions.

This project demonstrates production-quality data engineering: ingesting relational data via SQL, cleaning it with Pandas, building reusable analytical functions, and surfacing actionable agricultural insights.

---

## 🎯 Objectives

- Ingest and join multi-table agricultural survey data from an SQLite database using SQL
- Clean and validate the dataset (fix column swaps, spelling errors, invalid values)
- Analyse crop distribution, soil fertility, and climate-geography relationships
- Identify top-performing crops and their ideal growing conditions
- Build reusable, well-documented Python functions and an OOP data pipeline class

---

## 🗃️ Dataset

The `Maji_Ndogo_farm_survey_small.db` SQLite database contains **four tables**, all joined on `Field_ID`:

| Table | Key Features |
|-------|--------------|
| `geographic_features` | Elevation, Latitude, Longitude, Location, Slope |
| `weather_features` | Rainfall, Min/Max/Ave Temperature |
| `soil_and_crop_features` | Soil fertility, Soil type, pH |
| `farm_management_features` | Pollution level, Plot size, Crop type, Annual yield, Standard yield |

**Crop types covered:** cassava, tea, wheat, potato, banana, coffee, rice, maize

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Python 3.10 | Core language |
| Pandas | Data manipulation & analysis |
| SQLAlchemy | Database engine & SQL execution |
| SQLite | Source database |
| Matplotlib / Seaborn | Visualisation |
| Logging | Runtime diagnostics |
| OOP (Classes) | Reusable `FieldDataProcessor` pipeline |

---

## 📁 Repository Structure

```
maji-ndogo-agricultural-analysis/
├── maji_ndogo_agricultural_analysis.ipynb   ← Main analysis notebook
├── data_ingestion.py                        ← DB engine + SQL query utilities
├── field_data_processor.py                  ← OOP data pipeline class
├── validate_data.py                         ← Automated data quality tests
├── Maji_Ndogo_farm_survey_small.db          ← SQLite source database
└── README.md                                ← This file
```

---

## 🔍 Key Analyses

### 1. SQL Multi-Table Join
```python
sql_query = """
SELECT *
FROM geographic_features    AS g
JOIN weather_features       AS w ON g.Field_ID = w.Field_ID
JOIN soil_and_crop_features AS s ON g.Field_ID = s.Field_ID
JOIN farm_management_features AS f ON g.Field_ID = f.Field_ID
"""
```

### 2. Data Cleaning
- Fixed transposed column names (`Rainfall` ↔ `Min_temperature_C`)
- Standardised 8 crop types (removed spelling variants)
- Corrected negative elevation values using `.abs()`

### 3. Reusable Analytical Functions
- `explore_crop_distribution(df, crop)` — mean rainfall & elevation per crop
- `analyse_soil_fertility(df)` — fertility by soil type
- `climate_geography_influence(df, column)` — climate summary by grouping
- `find_ideal_fields(df)` — top-performing crop identification
- `find_good_conditions(df, crop)` — optimal field filtering

### 4. Production OOP Module
`FieldDataProcessor` class in `field_data_processor.py` wraps the full pipeline:

```python
from field_data_processor import FieldDataProcessor

config_params = {
    'db_path':            'sqlite:///Maji_Ndogo_farm_survey_small.db',
    'sql_query':          'SELECT * FROM geographic_features',
    'columns_to_rename':  {'Rainfall': 'Min_temperature_C'},
    'values_to_rename':   {'cassaval': 'cassava', 'teaa': 'tea'},
    'weather_mapping_csv': 'https://url/to/weather_data.csv'
}
processor = FieldDataProcessor(config_params, logging_level='INFO')
processor.process()
df_clean = processor.df
```

---

## 💡 Key Findings

| Finding | Detail |
|---------|--------|
| 🏆 Top-performing crop | Most fields with above-average yield |
| 🌱 Best soil type | Silt and Volcanic soils outperform others |
| ☔ Tea requirements | Elevation ~775m, Rainfall ~1,535mm |
| ⚠️ Pollution impact | Strongest negative predictor of Standard_yield |
| 💧 Low-yield zones | High-pollution fields underperform across all crop types |

---

## 👩‍💻 Author

**Oluwatobi Victoria Babalola**  
📧 bablotobi@gmail.com  
🌐 [bbt-portfolio.vercel.app](https://bbt-portfolio.vercel.app)  
💼 [LinkedIn](https://www.linkedin.com/in/oluwatobi-babalola-victoria/)  
🐙 [GitHub](https://github.com/TechieBbt)
