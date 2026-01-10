# KAPIA - Threshold Crossing Protocol

Status: CANONICAL  
Class: Irreversible Threshold Evidence  
Authority: DERIVED (via EVENT + IAM.MAI)  
Execution Power: LIMITED (crossing only)  
Identity Power: NONE  
Mutation Rule: Additive-only (via EVOLVE + CANON)

---

## 0. Canonical Statement

KAPIA governs **irreversible crossings** of defined thresholds during a live EVENT.

It records that a boundary was crossed **as evidence**, not as truth, and without inferring identity, intent, or outcome.

KAPIA does not decide who should cross.  
It records that a crossing occurred.

---

## 1. Purpose (Normative)

KAPIA exists to answer one question only:

**Did an irreversible threshold get crossed during a valid EVENT?**

It prevents:
- narrative claims without evidence,
- retroactive reconstruction of crossings,
- thresholds being implied by intent or payment.

---

## 2. Scope (LOCKED)

KAPIA applies **only while** `EVENT.state = ⊙`.

KAPIA does NOT apply to:
- interpretation (BPL),
- legitimacy of finality (IAM.MAI),
- presence custody (BNK),
- capacity regulation (ZIVai),
- narration (22),
- truth instantiation (PoP).

KAPIA is **evidence-only**.

---

## 3. Threshold Definition

A **threshold** is a defined boundary whose crossing is irreversible by nature.

Examples (non-binding):
- physical entry into a venue,
- access to a restricted zone,
- initiation of a live process.

Thresholds MUST be:
- explicitly defined before EVENT-LIVE,
- event-scoped,
- non-ambiguous.

---

## 4. Crossing Event (Irreversible)

A KAPIA crossing:
- occurs at a specific moment,
- cannot be undone,
- cannot be re-attempted retroactively.

Each crossing produces a **KAPIA_CROSS_RECORD**.

KAPIA_CROSS_RECORD is **evidence**, not truth.

---

## 5. KAPIA_CROSS_RECORD (Minimal)

A valid crossing record MUST include:

- `event_id`
- `threshold_id`
- `cross_ts`
- `evidence_ref` (implementation-defined)
- `record_id` (opaque)

It MUST NOT include:
- identity,
- intent,
- evaluation,
- outcome,
- presence truth.

---

## 6. Authority & Power

KAPIA:
- does NOT grant permission,
- does NOT admit or deny access,
- does NOT attest presence,
- does NOT finalize truth,
- does NOT regulate capacity.

KAPIA only **records that a crossing occurred**.

Permission logic, if any, lives outside KAPIA.

---

## 7. Relationship to Other Protocols

- **EVENT:** KAPIA crossings are valid only while EVENT = ⊙.
- **IAM.MAI:** KAPIA records may be referenced in legitimate finalizations.
- **BNK:** Bracelets MAY be used as capability artifacts; BNK does not authorize crossing.
- **ZIVai:** Capacity MAY inform pacing but does not alter KAPIA semantics.
- **22:** Narration MUST NOT reference individual crossings.
- **PoP:** PoP MAY reference KAPIA records as supporting evidence.
- **SPIRAL:** KAPIA records are not truth and are not appended directly unless referenced by a finalized truth.

---

## 8. Failure Modes (EXPLICIT)

The following are **NON-COMPLIANT**:

- recording crossings outside EVENT ⊙,
- retroactively creating crossing records,
- inferring identity from crossings,
- treating crossings as presence truth,
- using KAPIA to grant or deny access,
- collapsing multiple crossings into one narrative fact.

---

## 9. Canonical One-Line Definition

KAPIA is the protocol that records irreversible threshold crossings as evidence during a live event, without creating truth or authority.

---

END — KAPIA.md
