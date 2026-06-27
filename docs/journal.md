# Project Journal

A dated, running log of what was worked on, what was decided, and what remains
open. The goal is an honest record of the *thinking*, not just the output — so
that the reasoning behind each decision is recoverable later, and so the depth of
work is visible.

---

## Entry 1 — Phase 1: framing the problem

**Where we started.** The motivation was broad: do something useful with
privacy-enhancing technologies for people in disaster-affected areas. The first
real work was narrowing that theme into a concrete, solvable problem.

**The path of reasoning.**

- Began from the observation that disaster zones are *privacy-catastrophic*: aid
  organizations collect highly sensitive data about extremely vulnerable people.
- Looked for the specific coordination need that requires sharing: organizations
  operating in the same area need to know which beneficiaries they have in
  common, to avoid double-counting and to find people who are missed.
- This pointed initially at **private set intersection (PSI)** — compute the
  overlap of two sets without revealing the rest.
- Key realization (the turning point): in a low-documentation displaced
  population, names and birthdates are unreliable — inconsistent, estimated, or
  missing. The identifier that actually works across organizations is
  **biometric** (fingerprint, iris). This is why humanitarian agencies already
  collect biometrics.
- Second key realization: biometrics are the *most* dangerous data to hold —
  permanent, unchangeable, family-implicating, with documented real-world harms
  when leaked or seized. So a naive "match on biometrics" approach, even a private
  one, is unacceptable if any party ever stores a reversible biometric.
- This reframed the problem into something harder and more worthwhile than plain
  PSI: **fuzzy matching over protected biometric templates, computed privately.**

**Decisions made.**

- **Topic, committed:** privacy-preserving biometric deduplication of aid
  beneficiaries.
- **Scope for the first build:** two parties; honest-but-curious; synthetic/public
  data only.
- **Hard rule:** never use real beneficiaries' biometric data, at any stage.
- Wrote the Phase 1 documents: motivation (`00`), problem statement (`01`), threat
  model (`02`), and this journal.

**Open questions carried into Phase 2.**

1. What concretely is a "protected template," and which template-protection
   approach do we use? (Needs a short literature scan — see `research/notes/`.)
2. What distance metric defines "close enough to be the same person," and how is
   the threshold chosen? What is the resulting error rate on synthetic data?
3. Which private-computation technique do we build the fuzzy match on — secure
   two-party computation (e.g. garbled circuits / secret sharing) or homomorphic
   encryption? Each has different cost and depth trade-offs (cf. the multiplicative
   depth and cost analysis from the PSI exercises).
4. Does one party learn the intersection, or both? What metadata (set sizes,
   intersection size) is unavoidably revealed, and can it be reduced?

**Next action.** Phase 2 — translate the problem statement into a concrete
technical model: precise inputs (protected feature vectors), the exact
functionality the protocol computes, who learns the output, and what is hidden.
Before committing to a technique, do a short, honest scan of existing work on
biometric template protection and fuzzy/threshold PSI, and summarize it in
`research/notes/` so we build on what exists rather than reinventing it.
