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

### Here are the key aspects you can analyze from this query:
* Identify the countries with the highest percentage of disbursed amounts still owed.
* Compare the total amounts disbursed across countries.
* Understand how much each country owes to IDA in absolute terms.
* Analyze repayment patterns by observing the percentage of disbursed amounts still owed.
* Pinpoint countries with high percentages due, indicating potential repayment challenges.
* Detect which regions or countries received the largest loans.
* easure the reliance of countries on external financing by analyzing disbursed vs. owed ratios.
* Use this data to determine which countries require focused repayment follow-ups.

### Querie 1
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
```
### Query 2
```sql
SELECT 
    Country, 
    COUNT(Repayment_ID) AS Count_Of_Repays -- Total number of repayments per country
FROM 
    repayment_data -- Replace with your table name
GROUP BY 
    Country
ORDER BY 
    Count_Of_Repays DESC; -- Sort countries by repayment count in descending order
```





## Top Insights
* India has the highest number of repayments (33,325), which could indicate, A significant number of loans disbursed to India. Strong repayment practices or a large population involved in loan activities.
* Bangladesh (20,339) and Pakistan (14,792) are ranked second and third in the number of repayments. These countries might also have substantial loan programs but at a smaller scale compared to India.
* The dataset includes countries from South Asia (India, Bangladesh, Pakistan, Sri Lanka, Nepal) and other regions such as Yemen, China, Kenya, Vietnam, and Indonesia. This highlights the global nature of the loan disbursement and repayment process.
* Yemen (12,872) and Kenya (11,129) have considerable repayment counts, possibly indicating significant loan activities in these developing countries.
* Vietnam (7,535) and Indonesia (6,907) have lower repayment counts, which could point to Different economic conditions or financial policies.
* Zimbabwe's dues exceed the total disbursed amount at 104.51%, indicating a critical financial strain, likely due to high interest or penalties.
* These countries have percentages close to 100% (99.5%, 99.32%, and 98.86%, respectively), highlighting their significant repayment burdens.
* Ukraine (98.37%) and Cape Verde (98.23%) are approaching full repayment obligations, raising concerns about their financial stability.
* Both Sudan (95.62%) and Uzbekistan (95.06%) also face substantial liabilities, indicating repayment challenges.
