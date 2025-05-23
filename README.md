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
Table Structure:
Employees Table:
        CREATE TABLE Employees (
            EmployeeID INT PRIMARY KEY,
            FirstName VARCHAR(255),
            LastName VARCHAR(255),
            RoleID INT,
            LocationID INT,
            BaseSalary DECIMAL(18, 2),
            IsActive BIT,
            DateHired DATETIME
        );
Roles Table
        CREATE TABLE Roles (
            RoleID INT PRIMARY KEY,
            RoleName VARCHAR(255)
        );
Locations Table
        CREATE TABLE Locations (
            LocationID INT PRIMARY KEY,
            LocationName VARCHAR(255)
        );
Stored Procedures:
    -- Stored Procedure to get Employees by Role and Location
    CREATE PROCEDURE GetEmployeesByRoleAndLocation
    @RoleID INT,
    @LocationID INT,
    @IncludeInactive BIT = 0
    AS
    BEGIN
        SELECT
            e.EmployeeID,
            e.FirstName,
            e.LastName,
            r.RoleName,
            l.LocationName,
            e.BaseSalary,
            e.IsActive
        FROM
            Employees e
        JOIN
            Roles r ON e.RoleID = r.RoleID
        JOIN
            Locations l ON e.LocationID = l.LocationID
        WHERE
            e.RoleID = @RoleID AND e.LocationID = @LocationID AND e.IsActive = @IncludeInactive
    END;

    -- Stored Procedure to calculate Average Compensation by Location
    CREATE PROCEDURE GetAverageCompensationByLocation
    @LocationID INT
    AS
    BEGIN
        SELECT
            AVG(BaseSalary) AS AverageCompensation
        FROM
            Employees
        WHERE
            LocationID = @LocationID;
    END;
