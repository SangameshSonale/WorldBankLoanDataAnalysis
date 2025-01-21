# WorldBankLoanDataAnalysis
# Country Financial Analysis Project

This project analyzes and ranks countries based on the percentage of the amount due relative to the total disbursed amount. The SQL query calculates:
- Total disbursed amount for each country.
- Total amount due for each country.
- Percentage of the amount due, rounded to 2 decimal places.

## Files
- `query.sql`: The SQL query used for analysis.
- `data_description.txt`: Explanation of the dataset (if applicable).

## How to Use
1. Run the SQL query in your preferred database environment.
2. Replace `banking_data` with your actual table name.

## Query
```sql
SELECT 
    Country, 
    SUM(Disbursed_Amount) AS Total_Disbursed_Amount, 
    SUM(Due_to_IDA) AS Total_Due_to_IDA, 
    ROUND((SUM(Due_to_IDA) / SUM(Disbursed_Amount) * 100), 2) AS Percentage_Due_to_IDA
FROM 
    banking_data
WHERE 
    Due_to_IDA != 0
GROUP BY 
    Country
ORDER BY 
    Percentage_Due_to_IDA DESC;
