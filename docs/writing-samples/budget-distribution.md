---
title: "Writing Sample: Understanding Budget Distribution in Data Centers"
---

Each data center receives campaign budgets in direct proportion to the bid requests matched by its bidders. Within a data center, hardware differences between servers affect how much budget each bidder receives.

## Match rates affect budget distribution

Budget management is straightforward when operating a single data center, as the bidders simply receive all the available budget. However, modern architectures rely on multiple regional data centers. While this design makes the system fault-tolerant and highly responsive to bid requests, it exposes the limitations of distributing budgets evenly.

Applying an even budget distribution across multiple data centers is inefficient because bid request volume naturally fluctuates by region. An even distribution model risks stranding budgets in data centers that receive few or no bid requests, while starving regions with high demand.

To solve this problem, the ad serving system allocates budgets to each data center in direct proportion to its *match rate*. The match rate measures how often the bidders in a data center can fulfill a bid request, given the constraints set by each ad serving tactic. If a data center and its bidders match more bids, they receive a larger share of the available budget. This dynamic allocation method shifts resources between data centers and bidders in response to demand. 

In the ad serving technology stack, the budget allocator calculates the match rate, while Watson manages and distributes budgets to the bidders. For more information about how these systems work, see [Understanding Budget Distribution and Update Cycles](budget-distribution.md).

## Server hardware affects budget distribution between bidders

Hardware capabilities also affect budget distribution within a single data center. For example, bidders running on highly performant servers process requests faster, leading to better match rates than bidders on slower machines. Consequently, bidders on more powerful hardware naturally capture a larger share of the budget than those running on slower servers.
