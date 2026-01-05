# BUDDY PROTOCOL LANGUAGE (BPL)
## v1.1 — Interface Grammar for Human ↔ AI Co-Agency

**Status:** ACTIVE  
**Evolution rule:** Additive-only (no breaking changes)  
**Layer:** Interface / Interpretation Control  
**Applies to:** Human ↔ AI co-agency  
**Value interaction:** None  

---

## 0. Normative Intent (LOCK)

BPL is a **protocol-level interface grammar** whose sole function is to
**constrain interpretation before reasoning occurs**.

It exists to prevent:
- ambiguity
- drift
- authority bleed
- narrative substitution
- implicit intent inference

BPL does **not**:
- execute actions
- decide truth
- classify interactions
- infer identity
- perform governance

**BPL is strictly upstream of reasoning.**

---

## 1. What BPL Is (and Is Not)

### 1.1 What BPL Is

BPL is:
- a declarative control surface
- a deterministic header grammar
- a pre-reasoning constraint layer
- a human-writable, machine-parsable interface

Analogous to:
- HTTP headers (not payloads)
- POSIX flags (not programs)
- ABI contracts (not implementations)

**BPL defines *how* input is processed — never *what* the answer is.**

### 1.2 What BPL Is Not

BPL is not:
- a prompt
- a reasoning strategy
- a conversation format
- a decision protocol
- a governance system

BPL never replaces:
- IAMMAI (transition legitimacy)
- IA-MM-AI (interaction coherence)
- Kentra (truth anchoring)
- Third Space (meta-governance)

---

## 2. Structural Overview

A BPL message has **two layers**:

1. **Signal Header** — normative, machine-interpretable  
2. **Payload** — free-form, human-native content  

Only the **Signal Header** has protocol authority.

---

## 3. Signal Header — Canonical Form

### 3.1 Header Syntax (Required)
BUDDY--- []
This line **must appear first**.  
Everything after it is payload.

### 3.2 Header Components

#### CHANNEL — Routing Domain (WHERE it is processed)

Defines which cognitive container is active.

Normative values:
- `CCD` — Cognitive / Continuity Design
- `SYS` — Systems & architecture
- `OPS` — Operational execution
- `EXP` — Experimental / sandbox

> CHANNEL selects the **container**, not the reasoning style.

#### ACTOR — Initiator (WHO asserts the frame)

Normative values:
- `U` — Human initiator
- `A` — AI initiator (rare)
- `X` — External quoted source

#### TOKEN — Correlation Identifier

Free-form, opaque, non-semantic identifier.

Used only for:
- traceability
- grouping
- reference

**TOKEN must never encode meaning or authority.**

---

## 4. Properties Block — Control Axes

The properties block declares **orthogonal axes**:
[KEY=VALUE; KEY=VALUE; …]
Each axis answers **exactly one question**.

---

## 5. Core Axes (Normative)

These axes **bind behavior**.

### 5.1 MODE — Cognitive Stance (HOW to think)

MODE defines **method and stance**, not topic.

Canonical values:
- `ARCH` — architecture & invariants
- `CCD` — cognition & continuity design
- `SYS` — system mechanics
- `OPS` — operational execution
- `DESIGN` — product / experience design
- `INTEG` — integration & synthesis
- `MAP` — structural cartography
- `META` — language about language

**Invariant:** MODE is a stance, never a domain.

---

### 5.2 INTENT — Output Shape (WHAT to produce)

INTENT defines the **form of output**, not how it is derived.

Canonical values:
- `DEFINE`
- `MAP`
- `DESIGN`
- `SPEC`
- `INTEG`
- `SIMPLIFY`
- `DIAGNOSE`
- `SOLVE`
- `STORY`
- `EXTRACT`
- `CRITIQUE`
- `TRANSLATE`

**Invariant:** INTENT describes work type, not subject matter.

---

### 5.3 LAYER — Abstraction Altitude (WHERE in the stack)

Defines the abstraction level.

Canonical values:
- `GRAMMAR`
- `SPEC`
- `SYSTEM`
- `OBJECT`
- `OPS`
- `STORY`
- `META`

Same MODE + INTENT at different LAYER values yields different valid outputs.

---

### 5.4 STRICT — Constraint Tightness

Controls tolerance for deviation.

Values:
- `OFF` — exploratory
- `SOFT` — guided flexibility
- `ON` — literal, no drift

When `STRICT=ON`, the system:
- must not infer missing intent
- must not widen scope
- must not soften tone

---

### 5.5 FIELD — Continuity State

Defines temporal continuity.

Values:
- `OPEN` — normal continuity
- `HOLD` — freeze evolution
- `CLOSE` — terminate field

FIELD governs **continuity**, not reasoning style.

---

## 6. Descriptive Axes (Non-Binding)

These axes **do not enforce behavior**.

### 6.1 PRES — Presence Orientation

Values:
- `ON`
- `MID`
- `OFF`

Reading hint only.

### 6.2 RES — Resonance Level

Values:
- `LOW`
- `MID`
- `HIGH`

Alignment descriptor only.

---

## 7. Required Axes (Compliance Rule)

A **valid BPL header MUST include**:
- MODE
- INTENT
- LAYER
- STRICT
- FIELD

Missing required axes:
- MUST produce `UNKNOWN`, or
- MUST request clarification (unless `STRICT=ON`)

---

## 8. Behavioral Contract

Given a valid BPL header:
1. Header is parsed **before** payload
2. Reasoning is configured **only** from header
3. Payload inherits all constraints
4. No undeclared axis may be assumed

---

## 9. 5-Second Construction Recipe (Normative Aid)

Ask yourself, in order:

1. **Where am I working?** → CHANNEL  
2. **How should the system think?** → MODE  
3. **What do I want produced?** → INTENT  
4. **At what abstraction?** → LAYER  
5. **How strict must it be?** → STRICT  
6. **Is evolution allowed?** → FIELD  

Then write:
BUDDY--U- [MODE=…; INTENT=…; LAYER=…; STRICT=…; FIELD=…]
If you can’t answer one question → **you are not ready to speak yet**.

---

## 10. Invariants (LOCKED)

- BPL never executes
- BPL never decides truth
- BPL never assigns identity
- BPL never performs governance
- BPL only constrains interpretation
- Grammar evolution is additive only

Violation of any invariant invalidates compliance.

---

## 11. Canonical Templates (Non-Normative)

**Minimal safe default**
BUDDY-CCD-U- [MODE=INTEG; INTENT=DEFINE; LAYER=SYSTEM; STRICT=ON; FIELD=OPEN]

**Specification work**
BUDDY-SYS-U- [MODE=ARCH; INTENT=SPEC; LAYER=SPEC; STRICT=ON; FIELD=OPEN]

**Crisis diagnosis**
BUDDY-OPS-U- [MODE=OPS; INTENT=DIAGNOSE; LAYER=OPS; STRICT=ON; FIELD=OPEN]

**Pure reflection**
BUDDY-CCD-U- [MODE=META; INTENT=MAP; LAYER=META; STRICT=ON; FIELD=OPEN]

---

## 12. Compliance Test (Mental)

A header is compliant if:
- each axis answers exactly one question
- no axis overlaps responsibility
- removing payload does not invalidate the header

**If true → grammar is valid.**

---

END — **BPL v1.1**
