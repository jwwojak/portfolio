---
title: "Writing Sample: Budget Updates and Delivery Delays"
description: "How changing settings can force a budget update to start ad delivery."
---

Asynchronous budget updates can delay tactic delivery by 10 minutes to an hour. However, you can force an immediate budget update by changing and saving any setting within a campaign or tactic.

## Forcing a budget update

You can force an out-of-cycle budget update if you need a tactic to start bidding right away. To do this, make a minor change to any campaign or tactic and save it. For example, simply add a space to a campaign's **Description** field and click **Save**. 

This save event immediately prompts the budget allocator and the bidders to check for new or changed budgets, bypassing their scheduled update intervals.

## Budget updates and ad delivery

The budget allocator and the bidders update their budget information on different schedules. The budget allocator checks for new budgets at 10-minute intervals and distributes them to the bidders via a MySQL database and a system called Watson. 

The bidders then check Watson for these budgets at 1-hour intervals. A new tactic will only start delivering ads once the bidders receive their budget allocation. Because these update cycles operate independently, ad delivery depends entirely on where the allocator and bidders are in their respective schedules.

The timing of the bidders' check determines the result:

* **Before the budget allocator updates:** The tactic _may not_ deliver ads. The budget allocator has not yet processed and distributed the budget before the bidders' update cycle triggers.
* **After the budget allocator updates:** The tactic _may_ deliver ads. The budget allocator had sufficient time to update and distribute the budget before the bidders' cycle runs.

For more details on how these systems interact, see [Understanding Budget Distribution and Update Cycles](budget-updates.md).