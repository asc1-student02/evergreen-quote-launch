# Incident Communications: Shared Demo Cluster

**Date:** Wednesday, November 18, 2026
**Author:** Angela Jeske
**Incident:** Shared demo cluster API pods in CrashLoopBackOff (reported by a manager's dry run, ~13:25)
**Owner of the environment:** Platform services team

## What I observed

- On the shared demo cluster (namespace `demo`), three API pods are in CrashLoopBackOff with 6 to 7 restarts; the mongo pod is healthy (Running, 0 restarts).
- The API logs show it refused at `127.0.0.1:27017`, meaning it tried to reach a database inside itself and was not given the database address.
- The deployment's environment block shows `MONGO_URI`, and the pods are about 32 minutes old, which lines up with the environment variable tidy-up earlier that day.
- Not confirmed: that the rename is the cause. The report said the two might be related.

## Which environment this describes

The shared demo cluster, which the platform team owns. It is not the environment Friday's demo runs on.

## My own environment

- My cluster (`kind-evergreen`): 3 API pods and 1 mongo pod Running.
- CI on `delivery/lead`: both jobs green. Run link: [paste URL]

## Message 1: To the platform services team

**To:** Platform services team
**Re:** Shared demo cluster: API pods in CrashLoopBackOff since ~13:25

I am the Delivery Lead for the Evergreen Quote launch. The three API pods on the shared demo cluster (namespace `demo`) are in CrashLoopBackOff with 6 to 7 restarts, while the mongo pod is healthy. The API logs show it trying to reach a database at 127.0.0.1 and being refused, which suggests it is not receiving its database address. The deployment's environment block now shows `MONGO_URI`, and the pods are about 32 minutes old, which lines up with the environment variable tidy-up earlier today. I have not touched that environment.

Can your team confirm whether the rename is the cause, and restore the variable name the application reads (`MONGODB_URI`)? Could you tell me by [time] whether you can take it, and when you expect it restored? My own cluster and CI are green, so this does not block my merge.

## Message 2: To the manager who reported it

**To:** [Manager's name]
**Re:** "Could not load recent quotes" on the shared demo environment

Thank you for flagging this, and for running the dry run early. What we know: the quote service on the shared demo environment is restarting after a configuration change made earlier today, and the platform team, who own that environment, have been asked to confirm and fix it. The database itself is healthy.

For Friday: the launch demo does not run on that environment. It runs on my own verified setup, where the quote page loads and saves quotes, and our automated checks are green. I will update you by [time] on whether the shared environment is restored.

## Send log

| Message | Sent to | Where | Time sent | Reply by |
|---|---|---|---|---|
| 1 | Platform services team | [channel] | [time] | [time] |
| 2 | [Manager] | [channel] | [time] | [time] |

## What I did not do

I did not connect to the shared cluster or change anything in it. That environment has an owner, and the right move is to ask the owner a specific question.
