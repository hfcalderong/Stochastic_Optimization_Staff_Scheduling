# Stochastic Optimization - Staff Scheduling
Creates a labor schedule for a retailer that minimizes total cost while preserving a given service level target.

## Background

Brick-and-mortar retail stores employ about 15% of the American workforce. In retail, variable schedules are the norms where schedules typically change every day and every week with three to seven days’ notice of next week’s schedule. 2​ ​Researchers have found that matching labor to incoming traffic is a key driver of retail profitability. Most retailers operate under the assumption that stabilizing employees’ schedules would hurt the stores’ financial performance. 3​ ​Numerous studies have also found that variable schedules have deleterious effects on employees’ well-beings and thus incur invisible expenses, such as, inefficiency at work, etc.
3​ ​A few leading retailers have made the attempts to adopt more data-driven approaches for scheduling and been able to capture between 4 and 12 % in cost savings among other facets of store operations. S​table and consistent retail staffing scheduling that is able to meet the store traffic demand is likely to benefit both the employees and employers.

## Problem Statement

​Current solutions and softwares used by majority of the retailers produce only generic schedules that fail to account for store-specific factors and workload fluctuations, and they disregard the impacts of scheduling on the service level and staffs’ overall well-beings. These solutions have led to undesired results including:
● Overstaffing leads to high labor cost
● Understaffing that would hurt the stores’ profitability
● Inconsistency schedules lower the staffs’ satisfactions
​In this project, we intend to help solve the above three pressing issues in retail workforce scheduling by developing effective retail workforce scheduling models that will:
● ensure the number of staffs will match the store customer traffic
● minimize the total staffing cost
● improve the employees’ satisfactions and well-beings
● help managers make better staff scheduling decisions based on staffing cost and the
impact of staffing on the store’s service level which is correlated to the store revenues in most scenarios

## Model

During the first stage, the Sales Response Model forecasts the expected hourly sales based on the store traffic, average price of the product, number of sales staff, etc. Using this model, we are able to find the optimal number of staff that will maximize the expected profit in any given hour. The output from stage 1 is used as the input for the second stage where each employee is assigned to different shifts throughout the week with a mixed integer program. We further develop upon the stage 2 MIP model by adding service level and consistency constraints which will be discussed in more details in later sections.


