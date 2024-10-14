Markdown
# Customer Data Analysis

This project analyzes customer data to identify the number of unique customers who meet specific criteria related to age, service usage, and service dates.

## Key Findings

*   A total of 1304 unique customers fit the criteria of being 25 years old or younger at the start of their service.
*   The distribution of unique customers across different offices is as follows:

   ![image](https://github.com/user-attachments/assets/50ae5ba9-d94c-49d2-a2e6-ba61243a3869)


*   Office 432 has the highest number of unique customers (107) meeting the criteria.
*   Offices 155 and 160 have the lowest number of unique customers (2 each) meeting the criteria.

## Analysis Details

*   The analysis was performed using Excel, with data organized in a table named "Table2".
*   Key formulas used: (=INT(([@[Service_start]]-[@DateOfBirth])/365),
*   =AND(
    [@[Service_start]] > DATE(2022,10,1),
    [@[Service_end]] < DATE(2024,2,1)
)
=IF(DATEDIF([@DateOfBirth], [@[Service_start]], "Y")<=25,1,0))

*  Limitations: Inconsistent or missing data for age, service start date, service end date, office code, or service type.
  Errors in data entry (incorrect dates and typos in office codes).
  Duplicate records for the same customer. Ambiguous definitions of "Youth" (e.g., based on age at service start, end, or current age).
  Unclear criteria for determining service start and end dates (e.g., based on service creation, completion, or other factors).
  Data in a non-standard format (e.g., text instead of date).

 ## SQL Code to Count Unique Customers Meeting Criteria

This SQL query retrieves the unique customers who meet the following criteria:

* Age: 25 years or younger at the start of service.
* Service dates: Started after 10/01/2022 and ended before 02/01/2024.
* Office: One of the specified offices: 425, 101, or 987.

```sql
SELECT Office_No, COUNT(DISTINCT Customer_ID) AS UniqueYouthCustomers
FROM service_table
WHERE Service_Code IN (425, 101, 987)
  AND Office_No IN (138, 139, 140, 141, 142, 147, 150, 155, 160, 162, 181, 262, 312, 432, 433)
  AND Service_start > '2022-10-01'
  AND Service_end < '2024-02-01'
  AND DATEDIFF(YEAR, Service_start, DateOfBirth) <= 25
GROUP BY Office_No;
