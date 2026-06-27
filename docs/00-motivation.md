# 00 — Motivation: Why This Matters

## The setting

When a disaster strikes — an earthquake, a flood, a conflict that displaces a
population — humanitarian organizations move in to help. Multiple organizations
typically operate in the same area at once: UN agencies, the Red Cross / Red
Crescent, international NGOs, and local groups. Each registers the people it
serves so it can deliver aid, track who has been helped, and report to donors.

This registration produces data about some of the most vulnerable people in the
world, at the most vulnerable moment of their lives.

## Two problems collide

**Problem 1 — Coordination requires sharing.**
When several organizations work independently, the same person may be registered
many times while another person is missed entirely. Supplies are double-counted
or misallocated. To coordinate well, organizations need to know which
beneficiaries they have *in common* — and which they don't. That requires
comparing their records.

**Problem 2 — The records are dangerous.**
Many displaced people have lost their documents, or never had them. Names are
recorded inconsistently across languages and transliterations; birthdates are
often unknown or estimated. As a result, the only identifier reliable enough to
recognize the same person across two organizations is frequently a **biometric**:
a fingerprint or an iris scan. This is why major humanitarian agencies already
collect biometrics in the field.

But biometric data is uniquely hazardous:

- **It is permanent.** A leaked password can be reset. A leaked fingerprint or
  iris cannot. The exposure is for life.
- **It implicates families.** Biometric and relationship data can expose not just
  an individual but their relatives.
- **The threat is real, not hypothetical.** There have been documented cases of
  humanitarian biometric and registration data being exposed to, shared with, or
  demanded by the very authorities people were fleeing. A single breached or
  seized database can turn a tool meant to help into an instrument of harm.

## The gap

Today, organizations are caught between these two problems. Either they:

- **Don't share** — and accept poor coordination, double-counting, and missed
  people; or
- **Share raw records** — typically by pooling data into a shared database or
  exchanging files — and in doing so create a single, catastrophic point of
  failure: a concentrated store of the most sensitive possible data about the
  most vulnerable possible people.

Neither is acceptable. The coordination is genuinely needed. The data is
genuinely lethal if mishandled.

## Why privacy-enhancing technologies are the right tool

This is precisely the kind of problem privacy-enhancing technologies (PETs) exist
to solve: letting parties compute a needed result over sensitive data *without*
exposing the underlying data. The needed result here is the **overlap** between
two beneficiary lists. The data that must stay protected is everything else —
above all, the biometrics themselves and any information about people who are
*not* shared between the organizations.

If we can compute that overlap without any party ever holding a usable biometric,
and without revealing the non-overlapping people, we remove the catastrophic
database without removing the coordination. That is the aim of this project.

## A personal note on intent

This project began from a simple motivation: a wish to do something useful for
people in disaster-affected areas. The right way to honor that motivation is to
take the responsibility seriously — to build *with* humility about how
humanitarian response actually works, to defer to the people who do it, and to be
rigorous about not creating new harm in the name of preventing old ones. The
[responsible-use commitment](../README.md#️-responsible-use-commitment) in the
README is part of that, and it is not optional.
