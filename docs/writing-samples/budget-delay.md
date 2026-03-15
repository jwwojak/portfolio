---
title: "Writing Sample: Budget Updates and Delivery Delays"
custom_toc_title: "Writing samples"
---

Asynchronous budget updates can delay tactic delivery by 10 minutes to an hour. However, you can force an immediate budget update by changing and saving any setting within a campaign or tactic.

## Budget updates and ad delivery

The budget allocator and the bidders update their budget information on different schedules. The budget allocator checks for new budgets at 10-minute intervals and distributes them to the bidders indirectly through a MySQL database and a system called Watson. 

The bidders then check Watson for these budgets at 1-hour intervals. A new tactic will only start delivering ads once the bidders receive their budget allocation. Because these update cycles operate independently, ad delivery depends entirely on where the allocator and bidders are in their respective schedules.

Depending on the timing, if the bidders check for a budget amount:

* **Before the budget allocator updates:** The tactic _may not_ deliver ads. The budget allocator hasn't had enough time to process and distribute the budget before the bidder's update cycle triggers.
* **After the budget allocator updates:** The tactic _may_ deliver ads. The budget allocator had sufficient time to update and distribute the budget before the bidder's cycle runs.

For more details on how these systems interact, see [Understanding Budget Distribution and Update Cycles](budget-updates.md).

## Forcing a budget update

You can force an out-of-cycle budget update if you need a tactic to start bidding right away. To do this, make a minor change to any campaign or tactic and save it. For example, simply add a space to a campaign's description field and click save. 

This save event immediately prompts the budget allocator and the bidders to check for new or changed budgets, bypassing their scheduled update intervals.