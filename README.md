# private-aid-matching

**Privacy-preserving biometric deduplication of aid beneficiaries.**

Enabling humanitarian organizations to coordinate aid — without exposing the
vulnerable people they serve.

---

## What this is

In disaster and refugee settings, multiple aid organizations independently
register the people they help. To coordinate effectively — avoid
double-counting, fairly allocate scarce supplies, and find people who have
fallen through the cracks — these organizations need to know which beneficiaries
they have **in common**.

The problem: many displaced people have no documents and no consistent name or
birthdate, so the only reliable way to recognize the same person across two
organizations is **biometric** (e.g. a fingerprint or iris scan). But raw
biometric data is uniquely dangerous. Unlike a password, a fingerprint cannot be
changed if it leaks. A breached or seized database of refugee biometrics can
expose vulnerable people — and their families — to trafficking, persecution, or
violence, permanently.

**This project builds a way for two organizations to discover which beneficiaries
they share, using biometrics, such that no party — and no attacker who later
compromises a party — ever obtains a usable biometric, or learns anything about
the people the organizations do *not* have in common.**

## The technical challenge

This is harder than a standard private set intersection (PSI):

1. **Biometrics never match exactly.** Two scans of the same finger always differ
   slightly, so we cannot rely on exact-match techniques. We need *fuzzy* private
   matching: "are these two templates close enough to be the same person?",
   computed without revealing the templates.
2. **No one may ever hold a reversible biometric.** We operate on *protected
   templates* — transformed representations that can be matched but not turned
   back into the original biometric.

The contribution lives at the intersection: **fuzzy matching, over protected
biometric templates, computed privately between two parties.**

## ⚠️ Responsible-use commitment

This project exists to *reduce* the risk that biometric data poses to vulnerable
people. It would be self-defeating to be careless with that same data. Therefore:

- **We develop and test exclusively on synthetic and publicly available research
  data. We never use real beneficiaries' biometric data — at any stage, for any
  reason.**
- We do not claim that collecting biometrics from vulnerable populations is
  *safe*. Our position is narrower and honest: biometric collection already
  happens in the humanitarian sector, and *given that it does*, the matching step
  can be made dramatically safer than current practice. Reducing harm is the
  goal, not endorsing collection.

## Status

**Phase 1 — Problem definition.** See [`docs/`](docs/).

- [x] Motivation and human stakes — [`docs/00-motivation.md`](docs/00-motivation.md)
- [x] Problem statement — [`docs/01-problem-statement.md`](docs/01-problem-statement.md)
- [x] Threat model — [`docs/02-threat-model.md`](docs/02-threat-model.md)
- [ ] Phase 2 — Technical model (inputs, parties, functionality)
- [ ] Phase 3 — Prototype on synthetic data + benchmarks

A running log of decisions and reasoning lives in
[`docs/journal.md`](docs/journal.md).

## Repository structure

```
private-aid-matching/
├── README.md                     this file
├── docs/
│   ├── 00-motivation.md          why this matters; the human stakes
│   ├── 01-problem-statement.md   the precise problem we solve
│   ├── 02-threat-model.md        parties, assumptions, what is protected
│   └── journal.md                dated log of work, decisions, open questions
├── research/
│   └── notes/                    summaries of papers and sources
└── src/                          implementation (begins in Phase 3)
```

## License

To be decided (likely a permissive open-source license, so the work can actually
be used and built upon).
