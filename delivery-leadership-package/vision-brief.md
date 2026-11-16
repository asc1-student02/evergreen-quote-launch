# Evergreen Quote: Vision Brief

> Copy this file into `delivery-leadership-package/vision-brief.md` in your repo and fill it in. Target length: 1 page (~300 words). Write for a Liberty Mutual VP who has 90 seconds.

## Product
**Name:** Evergreen Insurance Quote (the launch: full-stack delivery)
**Delivery week:** Final
**Delivery Lead:** Angela Jeske (solo)
**Engineering team (represented by):** [link to evergreen-quote-launch repo on GitHub]
**GitHub Project board:** [link to Project board]

## Who is the customer?
The first-time insurance shopper: someone comparing options on their phone, often in a single sitting, who wants a believable monthly price without creating an account or sitting through a phone call. Today their alternative is a competitor's quote tool, and they will leave the moment ours feels slow, vague, or forgetful. Behind them are the partner pilot team, who query quotes over GraphQL, and the operations team, who need the service containerized, tested, and runnable on our cluster platform.

## What pain does Evergreen Quote remove?
"I got a number, and then it vanished." Until now, our page could estimate but not remember, and our service could remember but had no one to serve. A shopper who refreshed, came back tomorrow, or switched devices lost their quote. Wiring the two together turns a throwaway estimate into a saved quote that is still there tomorrow, shows the same price the estimate promised, and is backed by one source of truth. For the business, that means a customer who can return to finish, instead of one who starts over somewhere else.

## What does "good" look like at end of the week?
- A quote saved in the browser is still there after a reload, served from the database.
- The estimate on screen and the saved premium match for the same inputs (for example, auto, age 35, $50,000 coverage reads $450.00 in both places).
- The API runs as `evergreen-quote-api:2.0` on the local cluster with three replicas, and the unchanged app saves quotes into it.
- The launch merges to `main` in one reviewed pull request, with both CI jobs (API tests, client type-check and build) green.
- The five-minute Friday showcase tells the story from marketing page to saved quote to cluster, in plain language for managers who watched none of the build.

## What are we explicitly NOT doing this week?
- No authentication or user accounts.
- No payments or checkout.
- No real rate engine; rates remain simple per-coverage values, with the API as the source of truth.
- No required cloud spend; the demo of record runs on the local cluster (any Amazon EKS pass is gated by the sponsor and comes down the same day).
- No rewriting the provided pieces; we assemble and configure, we do not re-author.

## How will we know if it worked?
- **Persistence:** 100% of quotes saved in the demo survive a page reload (target: 3 of 3 test saves).
- **Consistency:** 0 mismatches between the estimate shown and the premium saved for the same inputs.
- **Pipeline health:** 2 of 2 CI jobs green on the merged `main`, and the Friday demo completes within 5 minutes.
