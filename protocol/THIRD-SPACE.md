# THIRD SPACE — Decision Trace Protocol

Status: CANONICAL  
Class: Governance / Decision Trace  
Authority: NONE  
Execution Power: NONE  
Truth Power: NONE  
Mutation Rule: Additive-only (via EVOLVE + CANON)

---

## 0. Canonical Statement

THIRD SPACE governs **how decisions exist without becoming truth**.

It defines a space where interpretations, policies, and choices may be recorded, referenced, and evolved, while remaining explicitly non-factual and non-authoritative.

THIRD SPACE does not decide reality.  
It records how reality was interpreted.

---

## 1. Purpose (Normative)

THIRD SPACE exists to answer one question only:

**What decisions were made in response to immutable facts?**

It prevents:
- decisions being mistaken for truth,
- policy masquerading as reality,
- governance silently rewriting history,
- interpretation collapsing into authority.

---

## 2. Scope (LOCKED)

THIRD SPACE applies **only after truth exists**.

THIRD SPACE does NOT apply to:
- interpretation binding (BPL),
- temporal admissibility (EVENT),
- legitimacy of finality (IAM.MAI),
- presence custody (BNK),
- threshold evidence (KAPIA),
- capacity regulation (ZIVai),
- truth instantiation (PoP),
- immutable history (SPIRAL).

THIRD SPACE is **post-truth, pre-execution**.

---

## 3. Decision Records (Core Object)

A **DECISION_RECORD** represents a single decision or policy choice.

A valid DECISION_RECORD MUST include:

- `decision_id` (opaque)
- `referenced_fact_ids` (SPIRAL turn IDs)
- `decision_ts`
- `decision_scope`
- `decision_statement` (human-readable)
- `lineage_ref` (optional, for EVOLVE)

DECISION_RECORD MUST NOT include:
- identity,
- speculative facts,
- unverifiable claims,
- execution instructions.

---

## 4. Relationship to Truth (LOCKED)

DECISION_RECORDs:
- MAY reference SPIRAL records,
- MUST NOT modify SPIRAL records,
- MUST NOT reinterpret facts as different facts,
- MUST NOT assert new truth.

Truth flows **into** THIRD SPACE.  
It never flows back.

---

## 5. Authority & Power

THIRD SPACE:
- does NOT create truth,
- does NOT legitimize finality,
- does NOT execute actions,
- does NOT enforce outcomes.

Authority remains external.

THIRD SPACE is **referential only**.

---

## 6. Lineage & Evolution

THIRD SPACE supports **decision evolution**, not correction.

Rules:
- decisions MAY be superseded via EVOLVE,
- prior decisions remain visible,
- no decision is deleted or rewritten.

This preserves:
- governance transparency,
- historical accountability,
- non-retroactive reasoning.

---

## 7. Relationship to Other Protocols

- **SPIRAL:** Provides immutable facts referenced by decisions.
- **PoP:** Supplies finalized presence truth.
- **EVENT:** Provides temporal context.
- **IAM.MAI:** Does not apply; THIRD SPACE is reversible.
- **ZIVai:** MAY be referenced but not acted upon.
- **22:** Narration MAY reference decisions; narration does not validate them.
- **UPAD / ISPAD:** MAY consume decisions for execution, but execution is external.

---

## 8. Failure Modes (EXPLICIT)

The following are **NON-COMPLIANT**:

- recording decisions before truth exists,
- modifying or deleting prior decisions,
- encoding identity in decision records,
- asserting decisions as facts,
- using THIRD SPACE to legitimize execution.

---

## 9. Canonical One-Line Definition

THIRD SPACE is the protocol that records decisions made in response to truth, without allowing those decisions to become truth themselves.

---

END — THIRD SPACE.md
