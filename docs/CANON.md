# CANON - Protocol Registry & Lineage Index

**Status:** FINALIZED  
**Class:** Canonical Registry Protocol  
**Scope:** Protocol Governance (Non-Operational)  
**Authority:** Declarative Only  
**Mutation Rule:** Additive-only  
**Execution Power:** NONE  
**Identity Power:** NONE  
**Economic Power:** NONE  

---

## 0. Purpose

CANON defines the authoritative set of protocols in the system.

It answers one question only:

**What is canonical, what is deprecated, and what is allowed to evolve?**

CANON exists to prevent:
- parallel definitions
- silent forks
- protocol drift
- retroactive reinterpretation

CANON does **not**:
- execute logic
- enforce behavior
- decide truth
- reason about content

CANON is a registry, not a controller.

---

## 1. Canonical Rule (Hard Lock)

If a protocol is **not listed in CANON**, it is **non-canonical**.

Non-canonical artifacts may exist as:
- drafts
- experiments
- scaffolding
- historical residue

They carry **no authority**.

---

## 2. Canonical Protocol Set

The following protocols are authoritative.

### 2.1 BPL — Buddy Protocol Language

**Role:** Translation / Interpretation Control  
**Version:** v1.1  
**Status:** LOCKED  
**Mutation Rule:** Additive-only  
**Authority:** NONE  

**Purpose:**
- binds meaning before intelligence
- constrains interpretation
- prevents authority bleed and hallucination

---

### 2.2 FID — Frequency ID Protocol

**Lineage Name:** IA-MM-AI  
**Role:** Pattern Identity Emission  
**Version:** v2.0  
**Status:** LOCKED  
**Mutation Rule:** Additive-only  
**Authority:** NONE  

**Purpose:**
- emits temporary, field-local pattern identity
- processes deltas only
- dissolves without persistence or identity carryover

---

### 2.3 IAM.MAI — Transition Legitimacy Protocol

**Role:** Continuity & Irreversibility Gate  
**Version:** v1.0  
**Status:** LOCKED  
**Mutation Rule:** Closed Set  

**Transition Set:**
- ⊙ HOLD  
- FINALIZE  
- INVALIDATE  
- EVOLVE  

**Purpose:**
- authorizes irreversible transitions
- preserves lineage
- forbids silent mutation

---

### 2.4 EVENT — Event Context & Closure Protocol

**Role:** Truth Container & Closure  
**Version:** v1.0  
**Status:** LOCKED  

**Purpose:**
- defines bounded context where truth may occur
- governs lifecycle (0 → ⊙ → 1)
- scopes PoP, KAPIA, and SPIRAL turns
- locks closure semantics

---

### 2.5 KAPIA — Irreversible Threshold Protocol

**Role:** Reality Boundary  
**Version:** v1.0  
**Status:** LOCKED  

**Purpose:**
- defines admissible entry
- consumes reversible value
- collapses potential into fact
- forbids reverse flow

---

### 2.6 PoP — Proof of Presence Protocol

**Role:** Truth Instantiation & Attestation  
**Version:** v1.0  
**Status:** LOCKED  
**Mutation Rule:** Closed After FINALIZE  

**Purpose:**
- defines what constitutes presence
- governs attestation authority
- instantiates irreversible event truth
- binds truth to EVENT context

---

### 2.7 SPIRAL — Continuity Memory Protocol

**Role:** Irreversible System Memory  
**Version:** v1.0  
**Status:** LOCKED  
**Mutation Rule:** Append-as-Turns (No Edit)  

**Purpose:**
- stores finalized truth as turns
- preserves lineage across events
- forbids overwrite or mutation
- enables reference without reinterpretation

---

### 2.8 Third Space — Decision Memory Protocol

**Role:** Governance Memory (Non-Truth)  
**Version:** v1.0  
**Status:** LOCKED  
**Authority:** Referential Only  

**Purpose:**
- records decisions
- references finalized truth
- does not generate or alter truth

---

## 3. Canonical System Surfaces (Non-Protocol)

The following are canonical **surfaces**, not protocols.

### 3.1 UPAD — Marketplace Execution Surface

**Role:** Primary Economic Execution Interface  
**Status:** ACTIVE  
**Authority:** Merchant of Record at EEI Boundary  

**Purpose:**
- issues reversible Value Units (VU)
- manages Balance
- enforces KAPIA
- triggers PoP instantiation
- sole interface to fiat (EEI)

---

### 3.2 ISPAD — Operational Command Surface

**Role:** Outbound Realization Interface  
**Status:** ACTIVE  
**Authority:** Delegated (Under Protocols)  

**Purpose:**
- coordinates organizers and partners
- applies finalized truth
- handles reporting, settlement, accountability
- realizes consequence without rewriting reality

---

## 4. External / Private Protocols

The following protocol exists **outside this repository** and is **not canonical here**.

### 4.1 PEP — Personal Economy Protocol

**Role:** Economic Coordination  
**Status:** EXTERNAL / PRIVATE  
**Authority:** Proprietary  

**Purpose (reference only):**
- separates reversible value (VU) from irreversible truth (PoP)
- governs UPAD, KAPIA, Balance, settlement logic
- aligns accounting with reality over time

No PEP mechanics, rules, or specifications may be mirrored in this repository.

---

## 5. Naming & Lineage Rules

- Public names may differ from lineage names.
- Lineage names preserve historical continuity.
- Renaming does not imply semantic change.
- Semantic change requires a new version entry in CANON.

---

## 6. Evolution Rules

A protocol may **EVOLVE** only if:
- invariants remain intact
- lineage is preserved
- prior versions remain referenceable

A protocol may be **INVALIDATED** only if:
- it violates invariants
- it enables identity capture
- it collapses value and truth

---

## 7. Non-Canonical Artifacts

The following are explicitly **non-canonical**:
- presentations
- examples
- onboarding docs
- experimental drafts
- chat transcripts
- internal notes

They may inform understanding but carry **no authority**.

---

## 8. Enforcement Statement

CANON is the final authority on:
- protocol existence
- protocol scope
- protocol legitimacy

Any system, document, or agent that contradicts CANON is **non-compliant by definition**.

---

## Final Lock

CANON exists so protocols cannot drift, fork, or be reinterpreted under pressure.

**END — CANON.md (FINALIZED)**
