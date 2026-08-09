# Axiom

Job boards are very hard to deal with. Especially if your are doesn't have many jobs and you are looking for remote roles either in your country or abroad, also when trying to find freelancing roles. The filters are always off, the jobs seniority level almost always default to giving the senior roles, outdated and reposted jobs everywhere, in addition to the continuously increasing number of scams and ghost jobs. Then finally the application takes sometimes up to an hour for a job you are not sure is real.

## What it does

Axiom pulls job postings from a handful of sources on a schedule, cleans up the mess, and hands you a short digest of what's actually worth looking at with reasons, not just a score. Ofc we cannot catch every scam and ghost job, but it's a massive improvement, now the jobs will actually match the exp level and the major we are in.

It's not a keyword filter. It's a handful of small agents that each do one job:

- **Source agents** — pull postings from different places (job boards, company pages, "who's hiring" style threads) and normalize the chaos into one consistent shape. Every source formats things differently; this is where most of the actual pain lives.
- **Dedup layer** — the same job shows up on three boards with three different titles more often than you'd think. This collapses them before you ever see them.
- **Fit agent** — reads a posting against my actual profile and reasons about whether it's a real match, not just whether the right buzzwords appear.
- **Risk agent** — actively looks for the stuff that makes a posting a trap: vague seniority, no salary listed, scope-creep language, the "we're basically pre-revenue but need a 10-year senior engineer" energy.
- **Arbiter** — when Fit and Risk disagree (a great skill match with three red flags, say), this is what reconciles them into one entry with a visible reason, instead of quietly averaging them into a meaningless number.
- **Tailoring agent** — for postings that make the cut, drafts a starting point: which of my actual projects to lead with, and why they fit this specific role. It doesn't send anything anywhere — it just means I'm editing a draft instead of starting from a blank page every time.

### Note: The agents count and names could change as the project goes, as the number of agents needed to actually run the project is less.

Runs on a schedule via GitHub Actions. Output is a digest you can actually skim in thirty seconds, with the strongest matches already half-written.

## Why agents, and not just one script

Early version of this was closer to a straight pipeline scan, rank, done. It worked, but it wasn't really thinking about anything, it was just sorting. The interesting part of this problem isn't ranking postings, it's that fit and risk are genuinely different questions that can point in opposite directions, and pretending they're one score throws away the actual signal. Splitting them out means the system can tell you *why* something's flagged, not just *that* it is.

## Status

Actively being built. Source agents and normalization are the current focus, a difficult part but the main source of "intelligence" in this system. Fit/Risk/Arbiter and the tailoring agent come after that foundation is solid.

## Stack

Python, LLM-based agents for fit/risk reasoning, GitHub Actions for scheduling.

---

Decide to build this because I was losing hours a week to job board noise, and figured the time was better spent building something that filters it instead.
