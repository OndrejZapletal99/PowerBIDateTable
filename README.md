# PowerBIDateTable
Ultimate PowerBi date table with date, year, months, months numbers,calendar quarter, weeks, days, days numbers, fiscal year and fiscal quarter

- PowerBi:
  - Dax

---

- ## Table of content
  - [1. Introduction](#1-introduction)
  - [2. Insert of the data](#2-new-date-table)
    - [2.1. Presumptions](#21-presumptions)
## 1. Introduction
Ultimate PowerBi date table with date, year, months, months numbers, weeks, days, days numbers and fiscal year
## 2. New date table
1. Open your PowerBi file
2. Select table or model view 
3. Click on the "New table"
4. Insert Dax code
5. Edit as needed
6. Mark as date table


```
Date = 
VAR minDate = MINX(Appned_table,Appned_table[EndBranchprice.Date])
VAR maxDate = MAXX(Appned_table,Appned_table[EndBranchprice.Date])
RETURN
ADDCOLUMNS(
    CALENDAR(minDate,maxDate),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Month number", MONTH([Date]),
    "Calendar quarter", CONCATENATE("Q",QUARTER([Date])),
    "Calendar week", WEEKNUM([Date],2),
    "Day number", WEEKDAY([Date],2),
    "Day", FORMAT([Date],"DDD"),
    "Fiscal Year", SWITCH(
        TRUE,
        MONTH([Date])>=10,
        YEAR([Date])+1,
        YEAR([Date])),
    "Fiscal Quarter", SWITCH(
        TRUE,
        QUARTER([Date]) = 1, "Q2",
        QUARTER([Date]) = 2, "Q3",
        QUARTER([Date]) = 3, "Q4",
        "Q1")
        )
 ```
### 2.1 Presumptions
- "VAR minDate" and "VAR maxDate" from some exisitng table (e.g. table "Appned_table"", Column "EndBranchprice.Date")
- Week starts at monday-->Day number of Monday is 1 and Sunday is 7
- Fiscal year runs from 1.10.XXXX to 30.9.XXXX
