![](https://i.imgur.com/RPrC7KE.png)
![](https://i.imgur.com/UJ9SdXF.png)
```
//Credit Card Excel File
// Load data from credit card statement tables



LOAD
    "Transaction ID",
    "Purchase Date",
    YEAR("Purchase Date") as "Year",
    "Merchant ID",
    Amount
FROM [lib://My data connection/Credit Card Statement.xlsx]
(ooxml, embedded labels, table is [Purchase Data]);

LOAD
    "Merchant ID",
    "Merchant Name" AS Merchant,
    "Category ID"
FROM [lib://My data connection/Credit Card Statement.xlsx]
(ooxml, embedded labels, table is [Merchant Data]);

//Category Data

LOAD
    "Category ID",
    "Purchase Category"
FROM [lib://My data connection/Category Data.txt]
(txt, codepage is 28591, embedded labels, delimiter is '\t', msq);

LOAD
    "Category ID",
    "Budgeted Amount",
    "Spent Amount",
    NUM("Budgeted Amount"-"Spent Amount",'#,##0')  as "Remainin Amount"
FROM [lib://My data connection/Category Budgets.xlsx]
(ooxml, embedded labels, table is [Category Budgets]);

//Merchant Rating

LOAD
    "Merchant ID",
    "Merchant Rating" as "MyRating"
FROM [lib://My data connection/Merchant Rating.xlsx]
(ooxml, embedded labels, table is [My Merchant Rating]);






```
