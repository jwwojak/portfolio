---
title: "Writing Sample: Understanding Budget Distribution and Update Cycles"
description: "How update cycles affect budget distribution in an ad serving system."
---

Five key components—the budget allocator, MySQL, Watson, Vertica, and the bidders—collaborate to manage and distribute budgets. Because the budget allocator and the bidders update data on separate schedules, their independent operations affect how and when budget data is distributed. 

## Budget distribution before updates

In **Backoffice**, a MySQL database stores budget cap information for each tactic. However, budgets are not immediately available to the bidders. Another system, the budget allocator, must run first to send bidder match rate data to Watson.

Match rates allow Watson to assign budget amounts to each bidder in proportion to how many bids they have matched, given the constraints set by a tactic. If the bidders do not have a budget, they simply send match rate data to Vertica, where it is passed on to the budget allocator. 

In the diagram below, the green circle illustrates how budget information is distributed before the budget allocator or the bidders update.

![Ad server budget before updates or distribution](../images/budget-distribution-1.png)

## Budget distribution after updates

Here is how budget data moves through the ad serving stack after an update:

**Budget allocator**
: At 10-minute intervals, the budget allocator checks Vertica for bidder match rate data. It applies a formula to this data to set the budget for each bidder based on performance. The budget allocator then sends match rate data to MySQL, where it is passed on to Watson.

**Watson**
: Watson is the authoritative source of budget information for the bidders. In this system, Watson:

    - Allocates budgets to the bidders.
    - Tracks expenditure.
    - Stops the bidders once they have exhausted their budget.

**Bidders**
: At 1-hour intervals, the bidders fetch and refresh all available campaign data from Watson. This ensures they have the latest budget and campaign data, taking bidder performance into account. As a result, the bidders receive budget amounts in proportion to their match rates; bidders that match a high volume of requests receive more budget than those with fewer bid requests. Finally, the bidders continue to send match rate data to Vertica, which is passed on to the budget allocator.

In the diagram below, the green circle illustrates how budget information is distributed after the budget allocator and the bidders update.

![Ad server budget after updates and distribution](../images/budget-distribution-2.png)

!!!note
    Update intervals can delay ad delivery from 10 minutes up to an hour. For more information about this delay and how to force an update, see [Budget Updates and Delivery Delays](budget-delay.md).