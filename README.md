# 🏡 Nashville Housing Data Cleaning (SQL Project)

## 📋 Overview
This project focuses on cleaning and preparing the **Nashville Housing dataset** using **SQL**.  
The goal was to transform raw and inconsistent housing data into a structured, analysis-ready format through systematic data cleaning techniques.

---

## 🧰 Tools & Technologies
- SQL Server Management Studio (SSMS)
- SQL

---

## 🧹 Data Cleaning Tasks Performed
1. **Removed Duplicates** – Identified and deleted duplicate records to maintain data accuracy.  
2. **Standardized Date Formats** – Ensured all date columns followed a consistent format.  
3. **Handled Missing Values** – Replaced or removed null and incomplete data where necessary.  
4. **Split and Normalize Columns** – Broke down combined fields such as address into separate columns (street, city, state).  
5. **Trimmed and Formatted Text Fields** – Removed extra spaces and standardized casing for consistency.  
6. **Created New Columns** – Extracted additional information for improved data structure and analysis.

---

## 📊 Key Learnings
- Strengthened understanding of **SQL-based data cleaning**.  
- Enhanced ability to prepare real-world datasets for analysis.  
- Developed efficient query-writing and debugging skills.

---

## 📁 Dataset
The dataset used in this project is the **Nashville Housing Data**, publicly available for educational and analytical purposes.

---

## 🚀 How to Use
1. Clone or download this repository.  
2. Import the dataset into your **SQL Server Management Studio (SSMS)**.  
3. Run the SQL script file (`Nashville_Housing_Data_Cleaning.sql`).  
4. Verify results by querying cleaned tables.

---

## 🧠 Example SQL Snippets

```sql
-- Standardizing date format
UPDATE NashvilleHousing
SET SaleDate = CONVERT(Date, SaleDate);

-- Removing duplicates using CTE
WITH RowNumCTE AS (
  SELECT *,
         ROW_NUMBER() OVER (
           PARTITION BY ParcelID, PropertyAddress, SalePrice, SaleDate, LegalReference
           ORDER BY UniqueID
         ) AS row_num
  FROM NashvilleHousing
)
DELETE FROM RowNumCTE
WHERE row_num > 1;

-- Splitting address into individual columns
ALTER TABLE NashvilleHousing
ADD Street NVARCHAR(255), City NVARCHAR(255);

UPDATE NashvilleHousing
SET Street = SUBSTRING(PropertyAddress, 1, CHARINDEX(',', PropertyAddress) - 1),
    City = SUBSTRING(PropertyAddress, CHARINDEX(',', PropertyAddress) + 1, LEN(PropertyAddress));


📜 Author
Sai Deepak
📍 Visakhapatnam, India
💼 Aspiring Data Analyst | SQL | Power BI | Tableau | Excel | Python
