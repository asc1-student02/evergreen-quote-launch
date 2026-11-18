# Status Update


**To:** Priya Ramanathan, Project Sponsor
**From:** Angela Jeske
**Date:** Tuesday, November 17, 2026

## What shipped today

- The quote app now loads and saves quotes through the API, so a saved quote survives a reload. The type-check caught one defect at the seam; it was fixed and rates were aligned (estimate and saved row both read $450.00). GraphQL is mounted and verified.
- Launch title, banner, and both quote links are configured. I approve the life-first landing hero and will update it once marketing confirms wording.

## What slipped (and why)

- **Form default to life:** it lives in the client team's shared estimate hook, so I routed it to them with the launch date. If they cannot review and re-test it before Thursday, it becomes the first post-launch change.
- **Renters:** not in launch scope. It crosses two validation systems across five files. A working version is parked on its own branch for after launch.

## What's next (tomorrow)

- Containerize the API and demonstrate three API pods plus a database on the local `kind` cluster; enable the two-job CI pipeline.
- Demo plan (Friday, local only): my VM, `kind` cluster `evergreen`, `kubectl port-forward svc/evergreen-quote-api 3000:80`, client at `http://localhost:5173`, opened from the landing page at `http://localhost:8080`. I will save a demo quote into the cluster beforehand and keep screenshots as a fallback. Nothing needs the cloud.

## What I need from you

Marketing's confirmed hero wording by 10:30 Wednesday, and your sign-off on deferring renters.
