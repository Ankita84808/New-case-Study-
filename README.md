# Employee Compensation Forecast Tool

A data-driven tool to analyze, filter, and forecast employee compensation using Python, SQLite, and a lightweight HTML/JS interface.

---

##  Tools Used

- **Python (Flask)**: Backend API for filtering, forecasting, and exporting employee data.
- **SQLite**: Lightweight relational database storing employees, ratings, and industry compensation data.
- **MySQL Workbench**: Used for initial ER diagram and schema planning.
- **Excel**: Data cleaning (typos, outliers, consistency issues).
- **HTML + JavaScript**: Optional prototype frontend interface for interacting with the backend.
- **DB Browser for SQLite**: For querying and verifying data.

---

##  Data Cleaning

### Issues Fixed:
- **Typos**:  
  `"Senir Associate"` → `"Senior Associate"`  
  `"Banglore"` → `"Bangalore"`

- **Outliers**:  
  Removed or adjusted 5 records ±40% from industry average compensation.

- **Inconsistencies**:  
  Fixed 7 records with mismatched `is_active` status and `last_working_day`.

### Example SQL Cleaning:
```sql
UPDATE employees  
SET role = 'Senior Associate'  
WHERE role LIKE 'Senir%';
# New-case-Study-
