## Decision Memo


**Date:** Tuesday, November 17, 2026
**Author:** Angela Jeske
**Decision area:** Day 2 tradeoffs: where the price calculation should live

## Context

When we connected the quote page to the saved-quote service for the first time, the same customer inputs showed two different prices: $425.00 in the live estimate and $450.00 on the saved quote. Nothing was broken. The page and the service each carried their own copy of the rate table, and the page's copy was older. Until Tuesday the two never appeared side by side. Now they do, and a customer could see them.

## Options considered

1. **Option A: Keep two calculators, aligned.** The page estimates instantly using its own rates, and the service calculates the official price when the quote is saved. Pros: the estimate updates as the customer types, with no waiting. Cons: two copies of the rates must be kept identical, and they can drift again.
2. **Option B: Make every estimate ask the service.** One calculator, one set of rates, so the numbers can never disagree. Pros: a single source of truth. Cons: every keystroke becomes a network request, so the estimate gets slower and stops working if the service is down.
3. **Option C: Hide the estimate until save.** Pros: the customer only ever sees the official price. Cons: loses the "instant quote" promise that is the product's main appeal.

## Recommendation

Choose Option A. We aligned the page's rates to the service (auto 90, home 135, life 70) as the sponsor directed, and we treat the service as the source of truth. Any rate change is made in both places and checked with one standard quote before every demo.

## Why

Customers came for a fast, believable number on their phone, and a delay or an outage would cost us more than a small maintenance chore. The risk of drifting rates is real, but it is visible, cheap to check, and owned by a named team in our risk register.

## What would change my mind

If the rates drift apart a second time before Friday's demo, or if the business starts changing rates weekly, I would revisit Option B and move all calculation to the service.
