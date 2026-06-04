# ✈️ British Airways Reviews Dashboard — Tableau Project

An interactive Tableau dashboard analyzing British Airways customer reviews. The project joins two data sources, uses calculated fields and a dynamic parameter, and visualizes airline performance across multiple service categories, aircraft types, time periods, and global routes.

---

## 📁 File Structure

| File | Description |
|------|-------------|
| `project5.twbx` | Packaged Tableau workbook (includes embedded data) |
| `ba_reviews.csv` | Raw customer reviews data (embedded in the workbook) |
| `Countries.csv` | Country reference table with continent and region info (embedded) |

> `.twbx` is a **packaged workbook** — all data is bundled inside, so no external files are needed to open it.

---

## 🗂️ Data Sources

### `ba_reviews.csv` — Main Reviews Table

| Column | Type | Description |
|--------|------|-------------|
| header | String | Review title |
| author | String | Reviewer name |
| date | Date | Date review was posted |
| place | String | Reviewer's country |
| content | String | Full review text |
| aircraft | String | Aircraft type flown |
| traveller_type | String | Solo, Couple, Family, Business |
| seat_type | String | Economy, Business, First, Premium Economy |
| route | String | Flight route taken |
| date_flown | Date | Date of the actual flight |
| recommended | String | Yes / No |
| trip_verified | String | Whether the trip was verified |
| rating | Integer | Overall rating (1–10) |
| seat_comfort | Integer | Seat comfort score |
| cabin_staff_service | Integer | Cabin crew score |
| food_beverages | Integer | Food & drinks score |
| ground_service | Integer | Ground handling score |
| value_for_money | Integer | Value score |
| entertainment | Integer | In-flight entertainment score |

### `Countries.csv` — Reference Table

| Column | Description |
|--------|-------------|
| Country | Country name |
| Code | Country code |
| Continent | Continent name |
| Region | Geographic region |

---

## 🔗 Data Relationship

The two tables are **joined** on the `place` field from `ba_reviews.csv` matching the `Country` field in `Countries.csv`. This enriches each review with continent and region data, enabling geographic filtering on the map.

---

## 🔧 Calculated Fields & Parameters

### Parameter — `Pick a Metric`
A dynamic **string parameter** that lets the user switch the metric displayed across all charts:

| Option |
|--------|
| Overall Rating |
| Cabin Staff Service |
| Entertainment |
| Food & Beverages |
| Ground Service |
| Seat Comfort |
| Value for Money |

### Calculated Field — `Metric Selected`
Drives the parameter by mapping the user's selection to the corresponding data column using a **CASE statement**:

```tableau
CASE [Parameter 1]
  WHEN 'Overall rating'      THEN [rating]
  WHEN 'Cabin Staff service' THEN [cabin_staff_service]
  WHEN 'Entertainment'       THEN [entertainment]
  WHEN 'Food'                THEN [food_beverages]
  WHEN 'ground Service'      THEN [ground_service]
  WHEN 'Seat comfort'        THEN [seat_comfort]
  WHEN 'Value'               THEN [value_for_money]
END
```

This single calculated field powers all four worksheets dynamically — changing the parameter updates every chart simultaneously.

---

## 📊 Worksheets

| Sheet | Chart Type | Description |
|-------|------------|-------------|
| `Summary` | Line / Bar | Average selected metric over time (by month/year) |
| `Map` | Geographic Map | Average metric by country — bubble/color intensity |
| `Aircraft` | Bar Chart | Average metric broken down by aircraft type |
| `Month` | Area / Line | Review volume and metric trend over time |

---

## 📈 Dashboard — `Dashboard 1`

All four worksheets are combined into one interactive dashboard featuring:

- **Line chart** — metric trend over time
- **World map** — geographic distribution of ratings by reviewer country
- **Bar chart** — performance comparison across aircraft types
- **Filters** for slicing by:
  - Traveller Type (Solo, Couple, Family, Business)
  - Seat Type (Economy, Business, First, Premium Economy)
  - Aircraft Type
  - Date range
  - Continent / Region
- **Parameter control** — `Pick a Metric` dropdown updates all charts at once

---

## 🚀 How to Open

1. Download and install **Tableau Public** (free) or **Tableau Desktop**
2. Open `project5.twbx` — data is already embedded, no CSV files needed
3. Navigate to **Dashboard 1**
4. Use the **"Pick a Metric"** dropdown to switch between rating categories
5. Use filters to drill into specific traveller types, seat classes, or regions

---

## 📋 Requirements

- Tableau Public 2024.1+ or Tableau Desktop
- No additional data files required (data is packaged inside `.twbx`)

---

## 📂 Dataset Overview

- **Source:** British Airways customer reviews (scraped/collected data)
- **Coverage:** Global reviewers across multiple continents
- **Metrics tracked:** 7 service categories rated on a numeric scale
- **Use case:** Identifying service strengths and weaknesses across aircraft types, routes, and passenger segments
