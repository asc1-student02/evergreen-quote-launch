# Copilot Review: AI Oversight Note

**Date:** Tuesday, November 17, 2026 (Day 3)
**Author:** Angela Jeske
**Task:** Use GitHub Copilot for one assembly step and critique the result

## What I asked

I asked GitHub Copilot to add two more seed quotes to `api/src/seed.js`, matching the existing shape and the Mongoose schema in `api/src/Quote.js`.

## What Copilot proposed

| Id | Type | Age | Coverage | Monthly premium | Tags |
|---|---|---|---|---|---|
| q7 | life | 45 | 500,000 | 420.00 | renewal |
| q8 | home | 61 | 320,000 | 512.00 | bundle, senior |

## What it got right

- **Field names** matched the existing rows.
- **Coverage types** (life, home) are allowed by the schema.
- **Ids** continued the q-pattern.
- **Ages and coverage amounts** sit inside the schema's limits (age 18 to 100, coverage at least 10,000).
- **The `tags` field** is real: the schema defines it as an array of strings, even though my request did not mention it.

## What I could not verify

- **The premiums.** Using today's formula in `api/src/premium.js` (base rate × age factor × coverage ÷ 10,000), the life quote would be $3,500.00 and the home quote $5,400.00. Copilot wrote $420.00 and $512.00.
- **Whether the difference matters.** The six existing seed rows carry historical premiums from an older rate table that I do not have, so I cannot tell whether Copilot's numbers are consistent with them.

## My decision

I did not keep the rows. I will not ship numbers I cannot verify, and extra rows add nothing to the launch or the Friday demo. I discarded the change and restored the original six quotes.

## Which gate would catch a bad row

| Gate | Reads `seed.js`? | Would it catch a wrong premium? |
|---|---|---|
| TypeScript (`npm run type-check`) | No. `seed.js` is JavaScript in the API | No |
| Mongoose schema (`Quote.js`) | Yes, every document, at runtime | **No.** It checks that a premium is a number, not that it is the right number |
| API tests (`npm test`) | No. They test the routes | No |
| CI pipeline | No. It runs the same tests and the client build | No |
| A person who checks the math | Yes | **Yes** |

The schema would reject some errors at the moment I run `npm run seed`: an unknown coverage type, an age of 12, or a premium written as text. It would not object to a premium that is a valid number and wrong.

## Would I ship its rows as-is?

No. The structure is right and the numbers are unverified. In AI-assisted work, plausible-looking output is where the risk sits, because nothing in our pipeline checks it.

## What I would ask of the team

- Ask the platform services team where the historical rate table lives, so a seed row can be checked against it.
- Treat AI-generated data the same as any other change: a named person verifies it before it merges.

## Takeaway for a leader

Plausible is not correct. Knowing which contract reaches where, and which does not, is the judgment AI-assisted teams need from the person leading them.
