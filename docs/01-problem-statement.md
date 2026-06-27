# 01 — Problem Statement

## One-sentence version

Enable two humanitarian organizations to determine which beneficiaries they have
in common, using biometrics, such that no party — and no attacker who later
compromises a party — ever obtains a usable biometric or learns anything about
the beneficiaries the organizations do *not* share.

## The precise problem

There are two organizations, **A** and **B**. Each holds a set of registered
beneficiaries. For each beneficiary, the organization has captured a biometric
(for concreteness, assume a fingerprint or iris, represented after feature
extraction as a numeric **feature vector**).

The organizations want to compute the **intersection** of their beneficiary sets
— the people both have registered — so they can coordinate. They are willing to
learn *who is shared*. They must not learn anything about *who is not shared*, and
no usable biometric may exist anywhere in the system.

## What makes this not "just PSI"

A standard private set intersection (PSI) protocol computes the intersection of
two sets while revealing nothing but the intersection itself. That machinery is
the starting point, but two domain realities break the textbook version:

### Challenge 1 — Fuzzy matching

Biometric captures are noisy. Two scans of the *same* person's finger produce
*similar but not identical* feature vectors. Standard PSI matches elements that
are **exactly** equal, so it would fail to recognize the same person across two
captures.

We therefore need **fuzzy** matching: two records should match when their feature
vectors are *close* under some distance metric (e.g. within a threshold), not
only when they are identical. And this closeness must be evaluated **privately**
— without revealing the feature vectors to anyone.

### Challenge 2 — No reversible biometric anywhere

Even a private matching protocol is unacceptable if either organization stores
raw, reversible biometrics that can later be stolen. So the system must operate on
**protected templates**: transformed representations that (a) can still be matched
fuzzily, but (b) cannot be reverted into the original biometric, even by the
organization that created them.

## What the system must guarantee

The following are the properties we will hold the design to. (They are stated
informally here; the [threat model](02-threat-model.md) makes the assumptions
precise, and Phase 2 will formalize them.)

1. **Correctness.** When the protocol finishes, the organizations correctly learn
   which beneficiaries they share (up to the inevitable error rate of fuzzy
   biometric matching — false matches / missed matches — which we will measure,
   not pretend away).

2. **Intersection-only privacy.** Neither organization learns anything about the
   other's beneficiaries beyond the shared set. In particular, the people unique
   to one organization remain completely hidden from the other.

3. **No usable biometric.** No party in the system — and no attacker who later
   compromises a party's storage — obtains a biometric that can be reversed back
   to a person's fingerprint/iris.

## Explicit non-goals (for now)

To keep the project honest and scoped, the following are *out of scope* for the
initial work, and noted as such rather than silently assumed away:

- **We do not address whether biometrics should be collected at all.** We take it
  as a given that collection already happens in practice, and we make the
  *matching* step safer. The collection question is a policy and ethics matter
  beyond this technical project.
- **We start with two parties**, not many. Multi-organization matching is a
  natural extension, deferred.
- **We start with an honest-but-curious threat model** (parties follow the
  protocol but are curious), and treat malicious parties as future work — mirrored
  on how these problems are normally approached and built up.
- **We use only synthetic and public research data**, never real beneficiary
  data. (See the responsible-use commitment.)

## Why this scoping is the right starting point

The fuzzy-matching-over-protected-templates core is the hard, novel, and
genuinely useful part. Getting *that* working and honestly benchmarked on
synthetic data — even in the simplest two-party, honest-but-curious setting — is a
real result. The extensions (more parties, stronger adversaries) are meaningful
follow-ups that build on a solid core, rather than prerequisites for it.
