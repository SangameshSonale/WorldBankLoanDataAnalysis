# WorldBankLoanDataAnalysis
-- Query to analyze and rank countries based on the percentage of amount due relative to the disbursed amount
SELECT 
    Country, 
    SUM(Disbursed_Amount) AS Total_Disbursed_Amount, -- Total amount disbursed per country
    SUM(Due_to_IDA) AS Total_Due_to_IDA,             -- Total amount due to IDA per country
    ROUND((SUM(Due_to_IDA) / SUM(Disbursed_Amount) * 100), 2) AS Percentage_Due_to_IDA -- Percentage of due amount relative to disbursed amount, rounded to 2 decimals
FROM 
    banking_data
WHERE 
    Due_to_IDA != 0 -- Exclude records where no amount is due
GROUP BY 
    Country -- Group results by country
ORDER BY 
    Percentage_Due_to_IDA DESC; -- Sort results in descending order of percentage due
