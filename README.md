# Week 3 Project — Python & Data Wrangling

## Dataset
A synthetic "messy" e-commerce sales dataset (`raw_sales_data.csv`, 310 rows)
was generated to include the typical real-world problems this assignment
asks you to fix:
- Missing values in `Region`, `Quantity`, `UnitPrice`, `CustomerAge`
- Invalid values (`Quantity <= 0`, `CustomerAge` of -5 or 150)
- Duplicate rows
- Inconsistent text casing/whitespace in `Category` and `Region`
- Dates stored as plain strings

## What `week3_project.py` does

1. **Load & inspect** the raw CSV, print shape, dtypes, missing-value counts,
   and duplicate count.
2. **Clean text fields** — strip whitespace and standardize casing
   (`.str.strip().str.title()`).
3. **Drop duplicate rows** (`drop_duplicates()`).
4. **Handle missing values**:
   - `Region` → filled with `"Unknown"` (keeps the row, flags the gap)
   - `Quantity` → filled with the median quantity
   - `UnitPrice` → filled with the mean price *per category* (more accurate
     than a single global average)
   - `CustomerAge` → invalid ages (outside 18–100) reset to NaN, then filled
     with the median age
5. **Filter invalid rows** — removes rows where `Quantity <= 0`, since a
   negative or zero quantity isn't a real order; drops rows with an
   unparseable date.
6. **Create new columns**:
   - `TotalSale` = `Quantity * UnitPrice`
   - `Month` — extracted from `OrderDate` for trend analysis
   - `AgeGroup` — bucket (18-24 / 25-34 / 35-49 / 50+) from `CustomerAge`
7. **Visualize** with Matplotlib & Seaborn:
   - Bar chart — total sales by category
   - Histogram — distribution of sale amounts
   - Heatmap — sales by region vs. age group
   - Line chart — monthly sales trend

## Files in this delivery
| File | Description |
|---|---|
| `raw_sales_data.csv` | The original messy dataset |
| `cleaned_sales_data.csv` | Cleaned & enriched dataset |
| `week3_project.py` | Full cleaning + visualization script |
| `chart_sales_by_category.png` | Bar chart |
| `chart_sales_distribution.png` | Histogram |
| `chart_region_agegroup_heatmap.png` | Heatmap |
| `chart_monthly_trend.png` | Line chart |

## How to run it yourself
```bash
pip install pandas matplotlib seaborn
python3 week3_project.py
```
This regenerates `cleaned_sales_data.csv` and all four PNG charts from
`raw_sales_data.csv`.

> Note: the Google Drive link included in the assignment slide wasn't
> reachable from this environment, so a realistic messy sales dataset with
> the same kinds of problems (missing values, duplicates, invalid entries,
> inconsistent text) was generated to complete the assignment end-to-end.
> Swap in your own CSV at the top of the script if you'd like the exact
> same cleaning steps applied to your provided data instead.
