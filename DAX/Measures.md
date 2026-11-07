
# DAX Measures

This document contains the main DAX measures used in the Banking Performance Dashboard.

## 1. Total Customers

Counts all unique customers from the Customers table.

```dax
Total Customers =
DISTINCTCOUNT(Customers[CustomerID])
```

## 2. Total Transactions

Counts all transactions.

```dax
Total Transactions =
COUNTROWS(Transactions)
```

## 3. Total Deposits

Calculates completed deposit amounts only.

```dax
Total Deposits =
CALCULATE(
    SUM(Transactions[Amount_JOD]),
    Transactions[Status] = "Completed",
    Transactions[TransactionType] = "Deposit"
)
```

## 4. Total Withdrawals

Calculates completed withdrawal amounts only.

```dax
Total Withdrawals =
CALCULATE(
    SUM(Transactions[Amount_JOD]),
    Transactions[Status] = "Completed",
    Transactions[TransactionType] = "Withdrawal"
)
```

## 5. Net Cash Flow

Calculates deposits minus withdrawals. Transfers are excluded.

```dax
Net Cash Flow =
[Total Deposits] - [Total Withdrawals]
```

## 6. Average Transaction Amount

Calculates the average amount of completed transactions.

```dax
Average Transaction Amount =
CALCULATE(
    AVERAGE(Transactions[Amount_JOD]),
    Transactions[Status] = "Completed"
)
```

## 7. Completed Transactions

Counts completed transactions only.

```dax
Completed Transactions =
CALCULATE(
    COUNTROWS(Transactions),
    Transactions[Status] = "Completed"
)
```

## 8. Completion Rate

Calculates completed transactions as a percentage of all transactions.

```dax
Completion Rate =
DIVIDE(
    [Completed Transactions],
    [Total Transactions],
    0
)
```

## 9. Total Transaction Amount

Calculates the total amount of completed transactions.

```dax
Total Transaction Amount =
CALCULATE(
    SUM(Transactions[Amount_JOD]),
    Transactions[Status] = "Completed"
)
```

## Additional Customer Measure

```dax
Customers with Transactions =
DISTINCTCOUNT(Transactions[CustomerID])
```
