# Delivery Goal: Evergreen Quote

## Goal

> By Thursday end of day, a quote saved in the Evergreen Quote app will survive a reload at the price the estimate promised, and the launch will be running on our cluster and merged to main with both CI jobs green.

## "Done" looks like

- The quote page loads its recent quotes from the API, and a saved quote survives a reload.
- The estimate on screen and the saved premium agree, at the launch rates.
- `npm test` (API) and `npm run type-check` + `npm run build` (client) pass; both CI jobs on the merge commit are **green**.
- The containerized API serves the wired app, and the cluster demo shows three API pods behind one Service.
- The landing page carries the launch banner and points at the app.
- A reviewed PR is merged, branch deleted.
- `delivery-leadership-package/` is complete and committed.

## Out of scope (this week)

- Authentication and user accounts.
- Payments or checkout.
- A real rate engine; the API's rates are the source of truth.
- Required cloud spend; the demo of record runs on the local cluster.
- Rewriting the provided pieces; we assemble and configure, we do not re-author.
