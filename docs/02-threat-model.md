# 02 — Threat Model

A threat model states precisely *who* the parties are, *what they are trusted to
do*, *what they are allowed to learn*, and *what an attacker can do*. Every later
design and security claim is judged against this document. If reality turns out
to differ from these assumptions, that is a finding to record — not something to
quietly paper over.

## Parties

- **Organization A** and **Organization B** — two humanitarian organizations,
  each holding a set of beneficiary records. Each record contains a protected
  biometric template (and, in deployment, whatever local information the
  organization needs to act on a match — out of scope for the privacy core).
- There is **no trusted third party** in the core design. (If a later variant
  introduces one, that is a distinct, explicitly-stated model.)

## Adversary model: honest-but-curious (starting point)

We begin with the **honest-but-curious** (also called *semi-honest*) model:

- Each organization **follows the protocol correctly** — it runs the agreed steps
  and supplies its real inputs.
- But each organization **is curious**: it will try to learn as much as it can
  from everything it legitimately sees during the protocol (its inputs, the
  messages it receives, and the output).

This is a realistic starting model for two organizations that genuinely want to
cooperate and have agreed to run the protocol, but that still must not be trusted
with each other's sensitive data. It is also the standard foundation on which
stronger models are built.

### Why not start with malicious?

A **malicious** party may deviate arbitrarily — lie about its inputs, run
different computations, send malformed messages — to extract information or
corrupt the result. Defending against this is substantially harder and requires
heavier machinery. We treat it as **future work**, stated openly, rather than
claiming protections we have not built. (See "Known limitations" below for the
specific risks this leaves open.)

## What must be protected

In order of importance:

1. **Raw / reversible biometrics.** These must not exist in usable form anywhere
   in the system — not in storage, not in transit, not reconstructable from
   protocol messages, and not recoverable by an attacker who later compromises a
   party. This is the strongest requirement and the reason for protected
   templates.

2. **Non-shared beneficiaries.** Anything about the people who are in one
   organization's set but not the other's must remain hidden from the other
   organization. Their existence, their count, their templates — none of it should
   leak beyond what is unavoidable (any unavoidable leakage, such as set sizes,
   must be stated explicitly in Phase 2).

3. **Beneficiary attributes generally.** Beyond the fact of a shared match, no
   additional personal information should cross between organizations through the
   protocol.

## What the parties are allowed to learn

- **The intersection** — which beneficiaries the two organizations share. This is
  the intended output and the entire point of the protocol. Whether *both* parties
  learn it or only one does is a design choice to be fixed in Phase 2.

## Attacker capabilities considered

- **A curious participant** (the honest-but-curious organization itself) trying to
  infer protected information from what it sees during a protocol run. — *In scope.*
- **Later compromise of a party's stored data** (e.g. a database breach or
  seizure after the fact). Because we forbid usable biometrics from existing at
  rest, such a compromise must not yield reversible biometrics. — *In scope; this
  is a primary motivation.*
- **A malicious participant** that deviates from the protocol. — *Out of scope for
  now; future work.*
- **Network adversaries.** We assume protocol messages travel over secure,
  authenticated channels (e.g. TLS), and — per the project's working assumptions —
  that network-level anonymity of connections can be taken as given where needed.
  Channel security is not the focus of this project.

## Known limitations (stated honestly)

- Under honest-but-curious, we do **not** defend against a party that lies about
  its input set or otherwise cheats. A malicious party could, for example, probe
  for specific individuals. This is the main gap and the clearest direction for
  follow-up work.
- Fuzzy biometric matching has an inherent **error rate** (false matches and
  missed matches). This is a property of biometrics, not of the privacy layer; we
  will measure and report it rather than hide it.
- Some **metadata** (such as set sizes, or the size of the intersection) may be
  revealed by the protocol. Exactly what is revealed will be made explicit in
  Phase 2; minimizing it is a design goal.
