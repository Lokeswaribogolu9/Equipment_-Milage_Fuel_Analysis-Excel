# Equipment Mileage & Fuel Cost Analysis (Excel Dashboard)

This project analyzes **equipment mileage and fuel consumption** using Excel.  
It is based on a synthetic dataset of ~200–300 records representing daily usage of plant equipment (forklifts, bobcats, loaders, etc.) with odometer readings and fuel data.

The goal is to:

- Track how far each equipment travels  
- Calculate fuel usage and cost  
- Measure efficiency (km per liter)  
- Summarize performance by month, equipment, and department  
- Build an interactive **dashboard** using PivotTables, charts, and slicers

---

## 📁 Files

- `Equipment_Mileage_Fuel_Analysis.xlsx`  
  *(Rename in this README if your filename is different.)*

---

## 📊 Dataset Structure

All raw data lives in the **`Data`** sheet as an Excel **Table** named `MileageTable`.

Columns include:

- `Date` – date of the trip  
- `Equipment_Name` – e.g., Forklift, Bobcat, Front End Loader  
- `Equipment_ID` – unique ID for each machine (e.g., F7(217595AH))  
- `Department` – Operations, Yard, Maintenance  
- `Odometer_Start` – odometer reading at start  
- `Odometer_End` – odometer reading at end  
- `Distance` – calculated as `Odometer_End - Odometer_Start`  
- `Fuel_Liters` – liters of fuel consumed  
- `Fuel_Cost_per_Liter` – unit fuel price (e.g. $3.20–$3.80)  
- `Fuel_Cost_Total` – calculated as `Fuel_Liters × Fuel_Cost_per_Liter`  
- `Driver_Name` – driver/operator name  
- `Month` – formatted as `YYYY-MM` from the Date  
- `Year` – year extracted from Date  
- `Km_per_Liter` – efficiency, calculated as `Distance / Fuel_Liters`

A separate **`Lists`** sheet stores lookup lists for equipment, IDs, departments, and drivers, used during data generation (with formulas like `INDEX`, `XLOOKUP`, and `RANDBETWEEN`).

---

## 🔧 Excel Operations / Formulas Used

This project intentionally uses multiple Excel features to simulate real analysis work:

### Calculated Columns

- `Distance = Odometer_End - Odometer_Start`  
- `Fuel_Cost_Total = Fuel_Liters × Fuel_Cost_per_Liter`  
- `Month = TEXT(Date,"yyyy-mm")`  
- `Year = YEAR(Date)`  
- `Km_per_Liter = Distance / Fuel_Liters`

### Lookup & Helper Logic

- `XLOOKUP` for mapping `Equipment_Name` → `Equipment_ID` from the `Lists` sheet  
- `INDEX + RANDBETWEEN` for simulating random equipment, department, and driver assignments  
- A helper classification column (optional) such as:
  - `Usage_Category` = IF(Distance < 20, "Short", IF(Distance <= 50, "Medium","Long"))

### Summary Functions

On summary sheets (`Monthly_Summary`, `Equipment_Summary`, `Quick_Analysis`), the project uses:

- `SUMIFS` – totals by month or equipment  
- `AVERAGEIFS` – average km/liter by equipment  
- `COUNTIFS` – number of trips by equipment  
- Data Validation (dropdown) to select an equipment and view its stats

### Conditional Formatting

On the `Data` sheet, **conditional formatting** highlights trips where `Km_per_Liter` falls below a threshold (e.g. < 5 km/l), making low-efficiency trips easy to spot.

---

## 📊 PivotTables

Several PivotTables are built from `MileageTable`, including:

1. **Distance by Equipment**  
   - Rows: Equipment_Name  
   - Values: Sum of Distance  

2. **Fuel Cost by Month**  
   - Rows: Month  
   - Values: Sum of Fuel_Cost_Total  

3. **Average Km per Liter by Equipment**  
   - Rows: Equipment_Name  
   - Values: Average of Km_per_Liter  

4. **Distance by Department**  
   - Rows: Department  
   - Values: Sum of Distance  

These PivotTables serve as the source for the dashboard charts.

---

## 📈 Dashboard

The **`Dashboard`** sheet brings everything together into a simple but meaningful view:

### KPIs

- **Total Distance** (sum of all Distance)  
- **Total Fuel Cost** (sum of Fuel_Cost_Total)  
- **Average Km per Liter** (average efficiency across all equipment)

### Charts

- **Distance by Equipment** (column chart)  
- **Average Km per Liter by Equipment** (column chart)  
- **Fuel Cost by Month** (line chart)  
- *(Optional)* **Distance by Department** (pie or column chart)

### Interactivity

- A **slicer** for `Equipment_Name` allows the viewer to filter all PivotTables and charts by a specific piece of equipment and instantly see updated KPIs and visuals.

---

## 🧠 Skills Practiced

- Data cleaning and structuring in Excel Tables  
- Calculated columns & helper fields  
- Lookup functions (`XLOOKUP`, `INDEX`)  
- Conditional logic (`IF`, nested IF)  
- Summary formulas (`SUMIFS`, `AVERAGEIFS`, `COUNTIFS`)  
- Data Validation (dropdown-driven summaries)  
- PivotTables (Rows, Values, grouping, field settings)  
- Chart creation (column, line, pie)  
- Dashboard layout design (KPIs, charts, slicers)

---

## 🚀 Possible Extensions

- Export the `MileageTable` to Power BI for a more advanced dashboard  
- Add maintenance cost and combine **fuel + maintenance** into total running cost per equipment  
- Introduce targets (e.g. minimum expected km/liter) and compare actual vs target

---

## 📌 Notes

- All data in this workbook is **synthetic** and created for learning/practice purposes.  
- The project is meant to demonstrate Excel skills for **data analysis, reporting, and dashboarding**, especially in an operations / equipment / fleet context.
