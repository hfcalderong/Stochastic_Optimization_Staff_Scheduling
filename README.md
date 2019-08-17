# Stochastic Optimization - Staff Scheduling
Creates a labor schedule for a retailer that minimizes total cost while preserving a given service level target. The schedule is built using Python v. 3.7.1 + Gurobi v. 8.1.1 to solve the Mixed Integer Programming problem with probability constraints.

## Table of Content

* [Background](#Background)
* [Models](#Models)
* [Results](#Results)

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

## Models

During the first stage, the Sales Response Model forecasts the expected hourly sales based on the store traffic, average price of the product, number of sales staff, etc. Using this model, we are able to find the optimal number of staff that will maximize the expected profit in any given hour. The output from stage 1 is used as the input for the second stage where each employee is assigned to different shifts throughout the week with a mixed integer program. We further develop upon the stage 2 MIP model by adding service level and consistency constraints which will be discussed in more details in later sections.

## Stochastic Optimization

One of the main disadvantages of the original model is that it only takes into account the operational impact of the staffing policy. With an increasing competition and the pressure to create unique experiences in brick-and-mortar stores, retailers depend heavily on the service level they provide to their customers to thrive and survive financially. One indicator they use is the service availability, defined as the number of customers that each staff member can assist. For this retailer, and only as illustration, we have defined a target of 10. If we use the expected store traffic then we can easily calculate the hourly requirement for staff

​Basically, this is done in the original model, where we obtain an optimal cost of $8,655. This approximation might be reasonable in scenarios where there is not high variability, however if store traffic fluctuates over a long range of values then this approximation is no longer justifiable. We shall then include our service level as probability constraints.
​Probability constraints arise naturally in many different applications and there has been an increasing number of research papers that explain how to solve these problems. We have divided the planning horizon (1 week) in 1-hour increments and within each interval we assume the arrival process follows a homogeneous poisson process. The following figure illustrates the different arrival rates for a typical week.

​There are two different ways to write the probability constraints, i.e. individual probability constraints or joint probability constraints,
​Consider first the individual probability constraints. These constraints are written as follow, ​Dentcheva D. [4] shows that for separable functions, this constraint can be equivalently be
expressed as a single linear constraint, as shown next
​This implies that min staff ≥ p − percentile of poisson distribution. We have one such constraint for every hour, and we can solve the increased LP with any standard solver such as Gurobi. Figure 5 shows the impact of the parameter ​p​ on the total staffing cost. We observe that when the probability of meeting the target service is very low (around 0.5) the cost is basically the minimum cost without any probability constraint. As we increase the service level the cost goes up and it can be as high as $11,000 and the team grows from 20 people to 27 people. For our simulations we used p = 0.95 , and the final result is denoted with a red dot. The optimal cost that we obtain is $10,290 which is about 20% larger that the minimum cost obtained using the expected value.

Consider now the joint probability constraint,
​This is a much more stringent constraint and it is usually more difficult to solve because there is no percentile for multivariate probability distributions. Nonetheless, it has been shown that this constraint can be replaced by a set of constraints that contain the feasible region with high probability [5]. This method is known as Scenario Approximation, and it’s similar in nature to the Sample Average Approximation (SAA) that is used to estimate the expected value in the objective function. With the Scenario Approximation you simulate N values, Zi , from the multivariate probability distributions and add N constraints to the problem of the following form
gj(x, Zi) ≤ 0
​The set of constraints above will produce a feasible solution with probability δ and ε is the probability of not meeting the service availability target. Additionally, a lower bound on the number of scenarios required is given by [5].
​For a problem of our size we would need at least 86,000 scenarios. Figure 6 shows the result of the three different methods. If we use the expected store traffic you would need a team of 20 people and there is a probability of 40% of not meeting the target service availability, but if you use the individual constraints this probability drops to 6% and the team grows to 24 people. Finally, if you use the joint probability constraint, the probability of not meeting the target is 0.001%, however the team grows to 34 people and the staffing cost goes up to $13,395 (+54%). Clearly, the decision of which constraints to add have a great impact in the optimal cost and the decision should be based on market research, strategic analysis, customer insights or from what the competitors are doing. This constraints show clearly the tradeoff of a better service and the staffic cost.

## Results
