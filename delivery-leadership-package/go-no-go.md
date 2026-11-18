# Go / No-Go: Launch Decision



**Date / time:** Wednesday, November 18, 2026, [time you finish, e.g. 15:20]
**Decision:** ☐ GO   ☐ NO-GO   ☑ GO WITH CONDITIONS

## CI evidence

- Latest run on `delivery/lead` (both jobs): **green** · link: https://github.com/asc1-student02/evergreen-quote-launch/actions/runs/44172152615
- Workflow file: `.github/workflows/ci.yml`
- What the workflow actually checked:
  - **Test the API:** started a throwaway `mongo:7` service, installed from the lock file with `npm ci`, and ran the API's seven tests.
  - **Type-check and build the client:** installed from the client's lock file, ran `npm run type-check`, and produced the production build.
- Environment this evidence describes: GitHub's clean build machine, testing the code on my branch. It says nothing about the shared demo cluster.

## Other evidence, by environment

| Environment | Evidence | Status |
|---|---|---|
| **My cluster** (`kind-evergreen`, on my VM) | `kubectl get pods`: 3 `evergreen-quote-api` pods and 1 `mongo` pod, all Running. A quote saved through the unchanged app survived a reload. Manifest and code agree on `MONGODB_URI` [confirm with the grep check] | Verified green |
| **Shared demo cluster** (platform team's `demo` namespace) | Incident capture: 3 API pods in CrashLoopBackOff (6 to 7 restarts), mongo pod healthy. Logs show the API refused at 127.0.0.1, and the deployment shows `MONGO_URI` after a rename about 30 minutes earlier | Broken; owned by the platform team |

## What "GO" would mean

- Merge `delivery/lead` → `main`, squash, delete branch.
- Tag the merge commit `launch`.

## What "NO-GO" would mean

- Hold the merge until: my own cluster or CI turns red, or the same variable rename is found in my manifests.
- Owner of that condition: me for my stack; the platform team for the shared demo cluster.
- Re-evaluate at: Thursday 10:00 check-in, and again before the merge.

## My call

**GO WITH CONDITIONS.** Friday's demo runs on my own verified stack (my `kind` cluster plus a green two-job CI run), not on the shared demo cluster, so the platform team's incident is real and tracked but does not gate my merge. The one thing that drove the call is that nothing on the list Friday depends on has changed. I would flip it to NO-GO if my own pods or CI turn red, if I find the same rename in my manifests, or if the plan changes to demo from the shared environment.
