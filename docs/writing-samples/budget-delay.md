---
title: "Writing Sample: Budget Updates and Delivery Delays"
---

Asynchronous budget updates can delay tactic delivery by 10 minutes to an hour. However, you can force an immediate budget update by changing and saving any setting within a campaign or tactic.

## Budget updates and ad delivery

Budget allocators and bidders update their budget information on different schedules. Budget allocators check for new budgets at 10-minute intervals and distribute them to the bidders indirectly through a MySQL database and a system called Watson. 

The bidders then check Watson for these budgets at 1-hour intervals. A new tactic will only start delivering ads once the bidders receive their budget allocation. Because these update cycles operate independently, ad delivery depends entirely on where the allocators and bidders are in their respective schedules.

Depending on the timing, if the bidders check for a budget amount:

* **Before the budget allocator:** The tactics _may not_ deliver ads. The budget allocator likely hasn't had enough time to process and distribute the budget before the bidder's update cycle triggered.
* **After the budget allocator:** The tactics _may_ deliver ads. The budget allocator had sufficient time to update and distribute the budget before the bidder's cycle ran.

For more details on how these systems interact, see [Understanding Budget Distribution and Update Cycles](budget-distribution.md).

## Forcing a budget update

You can force an out-of-cycle budget update if you need a tactic to start bidding right away. To do this, make a minor change to any campaign or tactic and save it. For example, you could simply add a space to a campaign's description field and click save. 

This save event immediately prompts the budget allocators and the bidders to check for new or changed budgets, bypassing their scheduled update intervals.