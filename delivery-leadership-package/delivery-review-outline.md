# Program Showcase: Evergreen Quote


## Slide 1: Delivery goal & did we hit it?

- Goal: By Thursday end of day, a quote saved in the Evergreen Quote app will survive a reload at the price the estimate promised, and the launch will be running on our cluster and merged to main with both CI jobs green.
- Hit? ☑ Yes  ☐ Partially  ☐ No
- A saved quote now survives a reload, the estimate and the saved price both read $450.00, three copies of the service ran on our cluster, and the launch merged to main in one reviewed change with every automated check green.

## Slide 2: What shipped

- A screenshot of the wired app: 

- Link to the merged PR (the diff is the whole program in one page: HTML, TypeScript, JavaScript, a Dockerfile, YAML): https://github.com/asc1-student02/evergreen-quote-launch/pull/9
- Link to the green two-job CI run (API tests + client type-check and build): https://github.com/asc1-student02/evergreen-quote-launch/actions/runs/44172152615
- A visitor lands on the marketing page, clicks through to the quote app, sees a live estimate, saves a quote, and it is still there tomorrow. The same service also answers a partner team through a second, more flexible door.

## Slide 3: Two key decisions

- **Decision 1:** Keep two price calculators (an instant estimate on the page, the official price on the server) and make the server the source of truth. Why it mattered: customers saw two different prices ($425.00 vs. $450.00) for the same inputs until we aligned them, and we chose speed over a single calculator.
- **Decision 2:** Split the sponsor's "lead with life" request into two decisions: approve the landing-page wording myself (content I own), and route the quote-form default to the engineering team that owns that code. Renters coverage stayed out of launch scope and is parked on its own branch. Why it mattered: small to type is not small to ship, two days before launch.
- (Both should be in `decision-memo.md`.)

## Slide 4: Risks & injects

- Top risk we tracked: Premium math lives in two places (R2). The page estimates instantly, and the service sets the official price. On Tuesday the same inputs showed $425.00 on the page and $450.00 once saved. We aligned the page to the service, which is the source of truth, and now check one standard quote before every demo. A second tracked risk, an empty list on the cluster because its database is separate from my machine's (R4), was predicted, then occurred on Wednesday exactly as planned.
- Inject #1 (Tue): The sponsor asked for a life-first launch, renters coverage, and a written local demo plan. I split the ask in two: I approved the landing-page wording (content I own), and routed the quote-form default to the engineering team that owns that code, with the launch date attached, because small to type is not small to ship. Renters stayed out of launch scope; a working version is parked on its own branch. The demo plan names the machine, the cluster, the command, and the addresses.
- Inject #2 (Wed): A manager reported "Could not load recent quotes" on the shared demo environment, which the platform team owns, and its service was restarting after a configuration rename. I did not touch it. I verified my own cluster and automated checks were healthy, asked the platform team one specific question with a deadline, and sent the manager a calm message. The call was GO WITH CONDITIONS: Friday runs on my verified setup, not the shared one, and I would flip to no-go if my own checks turned red.
- A small catch worth telling: after a color change, a box on the landing page looked broken. The first explanation (a color problem) was wrong; reading the page showed two items sharing one name. Fixed in minutes.

## Slide 5: What three phases built

- The journey in one slide: a static page that estimated but forgot, then a live typed React app that answered as you typed but could not remember, then a service with a database that remembered but had no screen, then a wired, containerized, orchestrated product. The page estimates, the service remembers, and for the first time they have met.
- What I take back to work on Monday: When a symptom does not match the first explanation, I say so out loud and look at the evidence before changing anything.
- One thing I'd do differently next round: Check what is already running, and which environment I am looking at, before I start something new. Several of my delays this week came from a service I forgot was already running.

## Q&A prep: likely questions

- "Why didn't you ship renters or the life default?" Renters crosses two checking systems across five files, and the form default sits in code every estimate flows through. Both are real requests with an owner and a first-after-launch slot, not a no. A working version of renters is parked on its own branch.
- "The demo returned quotes all week; why does one red check matter?" Because a green demo only tells you about my machine. The automated checks run on a clean machine every time anyone changes anything, so they catch what I cannot see. That is why my go/no-go cites the check results, not my own screen.
- "Why are there two price calculators?" The page must answer instantly as someone types, and the server decides the official price. We aligned them and check one standard quote before every demo; if rates change weekly, I would move all calculation to the server.
- "The shared environment broke on Wednesday. Why is Friday safe?" Friday runs on my own verified setup with every automated check green. The shared environment belongs to the platform team, and I asked them a specific question instead of changing it.
- "What would make you say no-go?" My own cluster or checks turning red, finding the same configuration mistake in my own files, or a decision to demo from the shared environment.

