# Bank Telemarketing Subscription Analysis

## Overview
Exploratory analysis of 41,188 contacts from a bank's telemarketing campaigns, aimed at finding which client segments and contact strategies are associated with subscribing to a term deposit. The exploratory analysis is written in T-SQL and run in SQL Server Management Studio (SSMS). Predictive modelling will follow in Python, in a separate folder of the same repository.

**Questions explored**
1. What share of contacted clients subscribe, and where does that rate rise or fall?
2. Do previous-campaign outcome, contact channel, client age, job and call frequency matter?
3. Which apparent effects survive checks for confounding?

## Objectives
- Identify key drivers of customer subscription
- Analyze customer demographics and financial attributes
- Generate actionable business insights

## Dataset
- Source: UCI Machine Learning Repository
- Type: Bank marketing dataset

## Tools Used
- **SQL Server**, SSMS T-SQL techniques used: `BULK INSERT`, `GROUP BY` aggregation, `CASE` expressions, CTEs, window functions.

**Python:** Python, pandas, scikit-learn, Jupyter.

## Key findings

All rates are the share of contacts that subscribed. The overall baseline is **11.27%**.

### Previous campaign outcome

| Previous outcome | Contacts | Subscribed | Rate |
|---|---:|---:|---:|
| success | 1,373 | 894 | 65.11% |
| failure | 4,252 | 605 | 14.23% |
| nonexistent (no prior campaign) | 35,563 | 3,141 | 8.83% |

Clients who subscribed in an earlier campaign are about 3% of contacts but about 19% of all subscriptions.

### Contact channel

| Channel | Contacts | Rate |
|---|---:|---:|
| cellular | 26,144 | 14.74% |
| telephone | 15,044 | 5.23% |

Caveat: telephone calls were concentrated in periods with low overall response (see Limitations), so part of this gap may reflect timing.

### Age

| Age band | Contacts | Rate |
|---|---:|---:|
| under 25 | 1,068 | 23.97% |
| 25-34 | 13,686 | 12.17% |
| 35-44 | 13,500 | 8.65% |
| 45-54 | 8,704 | 8.65% |
| 55-64 | 3,567 | 13.57% |
| 65+ | 663 | 47.21% |

The pattern is U-shaped. The 65+ band is small (663 contacts), so it is a strong signal from a limited group.

### Job, and what survives an age control

Raw rates by job range from 6.89% (blue-collar) to 31.43% (student). Two headline groups were then tested against age:

- **Students respond better than people of the same age.** Under 25: 37.83% for students (378 contacts) against 16.40% for other clients (689). Ages 25-34: 27.94% (433) against 11.66% (13,245).
- **The retiree effect is an age effect.** Among clients aged 65+, retirees subscribe at 47.14% (560 contacts) and non-retirees at 47.57% (103 contacts), essentially the same.

Cells with fewer than about 50 contacts were ignored.

### Call intensity (contacts in the same campaign)

| Calls | Contacts | Subscribed | Rate |
|---|---:|---:|---:|
| 1 | 17,642 | 2,300 | 13.04% |
| 2 | 10,570 | 1,211 | 11.46% |
| 3 | 5,341 | 574 | 10.75% |
| 4-5 | 4,250 | 369 | 8.68% |
| 6+ | 3,385 | 186 | 5.49% |

The rate falls at every step. Clients contacted six or more times account for about 8% of all contacts but about 4% of subscriptions.

## Limitations

- **Calendar month is a weak signal on its own.** Rates by month range from 6.43% (May) to 50.55% (March). Month mixes different years with very different economic conditions: months with an average 3-month  interest rate between 0.83 and 1.36 had rates of 20.48% to 50.55%, while months with averages between 3.29 and 4.69 had 6.43% to 10.60%. The month effect also persists among clients with no previous campaign (March 47.41%, May 5.47%), so previous outcome does not explain it. Month and interest-rate figures are therefore **not** treated as findings about customer behaviour.
- **Associations, not causes.** Nothing here shows that changing a variable would change the outcome.
- **Call-intensity stopping rule.** Clients who say yes stop being called, so those reaching a sixth call are people who kept declining. The table shows that clients needing many calls were less likely to subscribe, not that a sixth call has a 5.5% chance of success.
- **Small groups.** Several segments (for example 65+ and students aged 35 and over) have small counts and should be read cautiously.
  
## Business Recommendations
- Target high-performing customer segments
- Focus marketing on responsive demographics
- Optimize communication channels
- Improve campaign targeting strategies

## Author
Boluwatife Falola  

