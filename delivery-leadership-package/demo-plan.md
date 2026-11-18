# Demo Plan: Friday Program Showcase

**Date:** Friday, November 20, 2026
**Author:** Angela Jeske
**Format:** Live demo from the local cluster, with screenshots as the fallback

## What the audience will see

A visitor lands on the marketing page, clicks through to the quote app, sees quotes that came from a database, saves a new quote, reloads, and it is still there. Nothing in this demo needs the cloud.

## Where it runs

| Item | Detail |
|---|---|
| Machine | My VM |
| Cluster | `kind` cluster named `evergreen`: 3 API pods and 1 database pod |
| Connection | `kubectl port-forward svc/evergreen-quote-api 3000:80` |
| Quote app on screen | `http://localhost:5173` |
| Landing page | `http://localhost:8080` |

## Which database the audience sees

The cluster's database, not the VM's. It holds three believable quotes: auto (age 35, $450.00), home (age 40, $3,375.00), and life (age 30, $700.00). The oldest was saved on Tuesday and survived a full day, which is the point of the product.

## Pre-demo checklist (about 10 minutes before)

1. `kubectl config current-context` prints `kind-evergreen`.
2. `kubectl get pods` shows 3 API pods and 1 mongo pod, all Running, with 0 restarts on mongo (a mongo restart would wipe the demo data).
3. `docker ps` shows only the `evergreen-control-plane` container, so nothing competes for port 3000.
4. The port-forward is running in its own named tab, and I do not type commands there.
5. `curl http://localhost:3000/api/quotes` returns the three demo quotes.
6. `http://localhost:5173` shows the same three in the Recent quotes panel.
7. The landing page loads at `http://localhost:8080` and its Get your quote button opens the app.

## Demo flow (about 90 seconds)

1. Landing page: point to the launch banner and click Get your quote.
2. Quote app: type auto, 35, 50000. The estimate reads $450.00 as I type.
3. Recent quotes: point out that these came from a database, not a file.
4. Save a new quote. It appears at the top.
5. Reload the page. It is still there.
6. Say: a week ago this list was a sample file, and a saved quote vanished on reload.

## Known risks and what I do about them

| Risk | What I do |
|---|---|
| The port-forward drops (it did on Wednesday) | Re-run the port-forward command, then re-check the quote list |
| A pod restart wipes the cluster's database | Re-save two or three believable quotes before going on |
| Port 3000 is held by something else | Check `docker ps` and the other terminal tabs |
| A live step fails in front of managers | Switch to the screenshots without apology |

## Fallback (one keystroke away)

Screenshots, in this order: the wired app showing database quotes, the merged pull request (#9), the green two-job check run, and the cluster with 3 API pods and 1 database pod.
