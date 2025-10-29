Banking Transactions
Banks need to monitor customer transactions, account activities, and customer demographics to detect patterns, measure account performance, and identify inactive or high-value customers.
This Power BI dashboard helps the banking team analyze key performance indicators such as:

Total and average account balances

Monthly transaction volumes

Transaction distribution by type (Credit/Debit)

Top performing customers by transaction value

Customer demographic distribution (age, gender, location)

Inactive accounts (no transactions in the last 90 days)

Through these insights, the bank can optimize operations, detect anomalies, and enhance customer engagement strategies.

🧠 Objectives

Analyze customer behavior using demographics and transaction activity.

Identify top customers and inactive accounts.

Visualize account balances and transaction trends over time.

Provide interactive filtering by customer type, account type, and gender.

🪜 Steps Followed
Step 1: Data Loading

Imported three CSV files generated from SQL Server tables:

Customers

Accounts

Transactions

Combined and cleaned them in Power BI Power Query into one unified model (CombinedBankingDataset).

Step 2: Data Cleaning (Power Query)

Enabled Column Distribution, Column Quality, and Column Profile in Power Query.

Handled mixed date formats and null values.

Converted date fields (DateOfBirth, OpenDate, TransactionDate) to Date type.

Fixed inconsistent text casing for columns such as Account Type, Currency, and Transaction Type.

Removed duplicate records and handled invalid foreign key references (e.g., missing CustomerID in Accounts).

Step 3: Data Modeling

Created relationships between tables:

Customers[CustomerID] → Accounts[CustomerID]

Accounts[AccountID] → Transactions[AccountID]

Ensured cardinality (1 → ∞) and cross-filter direction from Customers → Accounts → Transactions.

Step 4: Data Transformation

Created calculated columns in Power BI for better analysis:

Customer Age = DATEDIFF(CombinedBankingDataset[DateOfBirth], TODAY(), YEAR)

Customer Age Group = 
SWITCH(TRUE(),
    [Customer Age] <= 25, "≤25",
    [Customer Age] <= 35, "26-35",
    [Customer Age] <= 50, "36-50",
    "51+"
)
