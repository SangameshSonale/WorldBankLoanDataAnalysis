# SQL Query: Analyze Total Disbursed Amount and Percentage Due to IDA by Country

### Why I Did This Project
This project was undertaken to analyze the financial obligations of countries and their repayment behaviors by calculating the percentage of dues relative to disbursed amounts. The goal was to identify patterns, highlight countries under financial strain, and provide actionable insights for policymakers and analysts while enhancing my data analysis and SQL skills.This query calculates the total disbursed amount, the total amount due to IDA, and the percentage of the disbursed amount that each country still owes. It lists the top 10 countries with the highest percentage due.

### You should read this to:

* Identify countries with high financial risk due to outstanding balances.
* Gain insights for better financial decision-making.
* Learn practical SQL techniques for advanced data analysis.
* Extract actionable metrics like repayment efficiency.

### What & Where is Dataset From
The dataset contains loan data from the World Bank, including information on the total disbursed amounts, amounts due, and repayment details for various countries. It highlights the financial obligations and repayment behaviors of countries receiving loans.
The dataset is sourced from the World Bank's publicly available financial datasets, which track global loan disbursements and repayments.

### Queries
```sql
SELECT 
    Country, 
    SUM(Disbursed_Amount) AS Total_Disbursed_Amount, -- Sum of Disbursed Amount by Country
    SUM(Due_to_IDA) AS Total_Due_to_IDA,            -- Sum of Due Amount by Country
    ROUND((SUM(Due_to_IDA) / SUM(Disbursed_Amount) * 100), 2) AS Percentage_Due_to_IDA
    -- Percentage of Disbursed Amount that is still owed
FROM 
    banking_data
WHERE 
    Due_to_IDA != 0 -- Exclude records where there is no due
GROUP BY 
    Country
ORDER BY 
    Percentage_Due_to_IDA DESC
LIMIT 10;
