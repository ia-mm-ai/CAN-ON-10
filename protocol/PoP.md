# PoP — Proof of Presence Protocol

Status: CANONICAL  
Class: Truth Instantiation  
Authority: DERIVED (via IAM.MAI)  
Execution Power: LIMITED (finalization only)  
Identity Power: NONE  
Mutation Rule: Additive-only (via EVOLVE + CANON)

---

## 0. Canonical Statement

PoP governs **when presence becomes truth**.

It defines how human-attested presence during a live EVENT is finalized into an immutable fact, independent of identity, payment, or narrative.

PoP does not measure presence.  
PoP finalizes it.

---

## 1. Purpose (Normative)

PoP exists to answer one question only:

**Did presence occur during this EVENT?**

It prevents:
- attendance being inferred from payments,
- presence being assumed from access,
- evidence being mistaken for truth,
- retroactive claims of attendance.

---

## 2. Scope (LOCKED)

PoP applies **only after** an EVENT has closed (`EVENT.state = 1`).

PoP does NOT apply to:
- interpretation (BPL),
- legitimacy of finality (IAM.MAI),
- presence custody (BNK),
- threshold crossing (KAPIA),
- capacity regulation (ZIVai),
- narration (22).

PoP is the **only protocol that creates attendance truth**.

---

## 3. Truth Definition (LOCKED)

A **presence truth** is a finalized claim that presence occurred during a specific EVENT.

Presence truth:
- is binary (present / not-present),
- is event-scoped,
- is immutable once finalized,
- contains no identity.

There is no partial, probabilistic, or graded presence truth.

---

## 4. Inputs (Admissible)

PoP MAY reference the following as **supporting evidence**:

- KAPIA_CROSS_RECORD(s)
- Event timing (EVENT-LIVE → EVENT-CLOSE)
- Human attestations (role-scoped)

PoP MUST NOT:
- infer presence from payment,
- infer presence from kernel state,
- infer presence from narration,
- infer presence from capacity signals.

Evidence informs PoP; it does not replace attestation.

---

## 5. Human Attestation (MANDATORY)

Presence truth MUST be human-attested.

Requirements:
- attestor role is explicit and authorized,
- attestation occurs only after EVENT closure,
- attestation scope is declared,
- attestation is irreversible once finalized.

Automated attestation is **NON-COMPLIANT**.

---

## 6. Finalization (Irreversible)

A PoP claim becomes truth only when:

- attestation is complete,
- EVENT.state = 1,
- IAM.MAI FINALIZE(PoP) is executed,
- SPIRAL append occurs.

Before finalization, all PoP claims are provisional.

---

## 7. Authority & Power

PoP:
- does NOT grant access,
- does NOT regulate capacity,
- does NOT execute economics,
- does NOT narrate state,
- does NOT process identity.

PoP only **creates immutable truth**.

---

## 8. Relationship to Other Protocols

- **EVENT:** PoP is valid only after EVENT closure.
- **IAM.MAI:** PoP truth requires IAM.MAI legitimacy.
- **BNK:** Kernel existence does not imply truth.
- **KAPIA:** Crossings may support PoP but do not constitute it.
- **ZIVai:** Capacity is irrelevant to PoP.
- **22:** Narration has no bearing on PoP.
- **SPIRAL:** PoP truth is written immutably.
- **THIRD SPACE:** Decisions may reference PoP truth but cannot alter it.

---

## 9. Failure Modes (EXPLICIT)

The following are **NON-COMPLIANT**:

- finalizing PoP before EVENT closure,
- automated presence attestation,
- deriving presence from payment or access,
- modifying PoP after finalization,
- encoding identity in PoP records,
- creating multiple presence truths per EVENT.

---

## 10. Canonical One-Line Definition

PoP is the protocol that converts human-attested presence into immutable event truth.

---

END — PoP.md
