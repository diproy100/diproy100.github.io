---
title: "Why One Big Cube Isn't Always the Answer"
date: 2026-11-20
draft: false
tags: ["OneStream", "EPM", "Design", "Performance"]
summary: "A 45-minute consolidation on a client project, and how splitting one big Cube into several fixed it."
comments: true        # set to false to turn off comments on this post
ShowToc: false
---

Most of us start the same way: one application, one Cube, everything in it. It feels clean. Then one day a consolidation takes 45 minutes and nobody is sure why.

It happened to me on a client project. Here's the challenge we hit, how we tracked it down, and what we changed.

## First, a quick word on Data Units

OneStream does its heavy work (loading, calculating, consolidating, locking) one Data Unit at a time. A Data Unit is one slice of data: a single Cube, Entity, Parent, Consolidation member, Scenario and Time period.

Think of it as one page in a workbook. Each page holds the records for its slice. If the pages get too big, or there are too many of them, the server spends its time juggling pages instead of doing useful work.

How big can a page get? Roughly, multiply the number of Accounts by the members in your User-Defined dimensions. That gives you the possible intersections.

## The problem: a 45-minute consolidation

The client was a medium-sized company, and we had built everything in a single Cube. When we ran a performance test on the prototype, consolidation took 45 minutes. For the amount of data we had, that was far too long.

So we dug into the data and found two culprits:

1. **UD1 had very little overlap across the leaf Entities.** UD1 held the cost centers. Each Entity mostly used its own, but they all sat in one big member list inside one Cube.
2. **Our allocation calculations were creating a lot of detail nobody reported on.**

Together, these left the data at the top Entity far too dense.

## The fix

We took them one at a time.

**1. Rein in the allocation rule.** Limit where the rule runs, then ask whether all that allocated detail really needs to be consolidated. To see the impact, run the calculation with the rule and without it. A careful review of a rule like this usually pays off.

**2. Split the single Cube.** The bigger change: instead of one Cube holding every cost center, we grouped UD1 and gave each group its own Cube:

- **Corp:** corporate summary cost centers, by group
- **Hist:** historical cost centers that are no longer active
- **CC1, CC2 and so on:** logical groups of cost centers

Each Cube now holds only the cost centers its Entities need. Every Data Unit is smaller and faster to process, and users only see the cost centers that matter to them, so navigation got simpler too.

Smaller pages, less work. That's the whole idea.

If your project is bigger, a pattern worth knowing is a Detailed Cube (large dimensions, sparse data) next to a Summary Cube (fewer members, dense data). You keep the reporting detail, and the summary still aggregates quickly.

## What I took from it

- **Watch Data Unit size.** Accounts times User-Defined members tells you how big it can get. Anything over about 1 million records deserves a closer look.
- **Don't default to one Cube.** If a dimension's members barely overlap across Entities, that's a hint to split.
- **Review your rules.** Calculating data nobody reports on is expensive.
- **Test early.** We caught this in a prototype, not in production, and a quick prototype build (two to three days) is cheap insurance.
- **More Cubes means more upkeep.** The performance gains are worth it.

Have you seen a design hit a wall like this? I'd love to hear how you handled it. Feel free to leave a comment below!
