DAX Formulay

1. AgeGroup = SWITCH(
    TRUE(),
     'public cust_detail'[customer_age] < 30, "20-30",
     'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
     'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
     'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
     'public cust_detail'[customer_age] >= 60, "60+",
     "unknown"
)

2. IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)

3. Week_num2 = WEEKNUM('public cc_detail'[week_start_date]) 

4. Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

5. Current_Week_Revenue = CALCULATE(
     SUM('public cc_detail'[Revenue]),
     FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[Week_num2] = MAX('public cc_detail'[Week_num2])))

6. Previous_Week_Revenue = CALCULATE(
     SUM('public cc_detail'[Revenue]),
     FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[Week_num2] = MAX('public cc_detail'[Week_num2])))

7. WOW_Revenue = DIVIDE(([Current_Week_Revenue] - [Previous_Week_Revenue]),[Previous_Week_Revenue]) 
