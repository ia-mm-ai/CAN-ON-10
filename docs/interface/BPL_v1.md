# BUDDY PROTOCOL LANGUAGE (BPL)
## v1.0 — Official Specification (FINAL)

**Status:** FINAL (v1.0)  
**Evolution rule:** Additive-only. No breaking changes.  
**Layer:** Interface / Interpretation Control (pre-reasoning)  
**Applies to:** Human ↔ AI co-agency  
**Value interaction:** None (zero)

BPL is **not** a programming language, governance document, or execution protocol.  
It is a deterministic interaction language whose sole purpose is to **constrain interpretation before reasoning or execution occurs**.

---

## 1. Purpose

BPL (Buddy Protocol Language) defines a strict but lightweight way for a human architect and an AI system to exchange **intent, context, authority, and constraints** without ambiguity or drift.

It enforces two layers:

1. **Signal Layer** — exactly one structured header line (machine-parseable intent)
2. **Payload Layer** — free-form content bound by the signal

BPL exists to:
- Separate **intent** from **content**
- Stabilize co-agency (prevent drift)
- Prevent hallucination and authority bleed
- Preserve continuity across sessions and threads

---

## 2. High-Level Structure

A BPL message has the following form:

1) **SignalLine**  
2) **PayloadBlock** (optional)

Example:
BUDDY-CCD-U-04012026 [MODE=INTEG; FIELD=OPEN; STRICT=ON; DEPTH=DEEP; LENS=SYS]

Everything starts with **exactly one SignalLine**.

---

## 3. Lexical Rules

### 3.1 Character set
- Payload: UTF-8 (any language; emojis allowed)
- Keywords / keys: ASCII

### 3.2 Case
- Keys / keywords: UPPERCASE
- Values: case-insensitive unless enumerated

### 3.3 Whitespace
- Signal line: single spaces recommended
- Payload: free

---

## 4. Signal Line

### 4.1 Grammar
SignalLine ::= SignalID (WS PropertiesBlock)?

### 4.2 SignalID
SignalID ::= “BUDDY” “-” ChannelCode “-” ActorCode “-” Token
#### ChannelCode (3 letters)

- **CCD** — Cognitive Container Dialogue  
- **OPS** — Operations / procedures / execution threads  
- **SYS** — Systems / architecture / protocols  
- **EXP** — Experiments / sandboxing  

#### ActorCode

- **U** — User (human initiator)  
- **A** — Assistant (AI initiator, rare)  
- **X** — External actor being quoted  

#### Token

Free-form identifier controlled by the user.  
Recommended formats:
- `DDMMHHMM`
- `DDMMYYHHMM`
- Optional suffix: `-CUSTOM`

Examples:
- `04012026`
- `05121746-POP`
- `02121200-MARINA`

---

## 5. Properties Block

### 5.1 Grammar
PropertiesBlock ::= “[” Property (”;” Property)* “]”
Property ::= KEY “=” VALUE
### 5.2 Standard properties (normative)

#### MODE — cognitive stance (how to process)

- **INTEG** — integrate, unify, surface invariants  
- **ANALYZE** — debug, find failure modes  
- **DESIGN** — architect systems, protocols  
- **EXEC** — produce ready-to-use artifacts  
- **EXTRACT** — extract facts only  
- **REFLECT** — structural mirroring (no persuasion)  
- **DUMP** — minimal processing / reformat  

#### FIELD — container state (continuity control)

- **OPEN** — maintain continuity  
- **HOLD** — freeze evolution (no forward moves)  
- **CLOSE** — explicitly end the field  

#### STRICT — hallucination tolerance

- **ON** — no speculation; declare `UNKNOWN` if unsure  
- **OFF** — normal reasoning allowed  

#### DEPTH — verbosity

- **SNAP** — one screen  
- **MID** — default  
- **DEEP** — full architecture  

#### LENS — interpretive frame (what lens to privilege)

- **CEO** — risk, leverage, sequencing  
- **OPS** — procedures, timelines  
- **SYS** — states, transitions, invariants  
- **HUMAN** — load, boundaries, communication  
- **MARKET** — narrative, positioning  

Multiple lenses may be combined: `CEO+SYS`

#### PRIORITY

- **P0** — immediate crisis  
- **P1** — high importance  
- **P2** — normal work  
- **P3** — background  

#### SCOPE

Free-form domain identifier (e.g., `POP_LEDGER`, `THIRD_SPACE`, `UPAD_V2_ARCH`)

#### VERSION (optional)

Internal versioning only.

---

## 6. Payload Layer

Everything after the SignalLine is payload.

### 6.1 Free text
Unstructured, human-native text.

### 6.2 Inline Directives (optional)

Inline directives MUST be on their own line and UPPERCASE:

- `#TASK` — concrete action  
- `#CONTEXT` — background only  
- `#ASK` — explicit questions  
- `#MEMO` — store / export  
- `#END` — end of important content  

---

## 7. Semantics (Behavioral Contract)

Given a valid BPL message, the AI must:

1) Parse the SignalLine first  
2) Configure behavior strictly from properties  
3) Treat the payload as one coherent field  

### STRICT=ON rules (hard)

- Unknowns must be declared explicitly as `UNKNOWN`
- No soothing or coaching language
- No invented facts, tools, or claims
- Conflicts must be reported as `CONSTRAINT_CONFLICT`
- No “helpfulness substitution” (no action not requested)

---

## 8. Formal Grammar (relaxed EBNF)
Message ::= SignalLine NEWLINE PayloadBlock?
SignalLine ::= “BUDDY” “-” ChannelCode “-” ActorCode “-” Token (WS PropertiesBlock)?
ChannelCode ::= UPPER{3}
ActorCode ::= “U” | “A” | “X”
Token ::= (LETTER | DIGIT | “-”){1,32}
PropertiesBlock ::= “[” Property (”;” Property)* “]”
Property ::= KEY “=” VALUE
PayloadBlock ::= (PayloadLine NEWLINE)*
PayloadLine ::= UTF8_TEXT

---

## 9. Canonical Examples

### Integration

BUDDY-CCD-U-05121746 [MODE=INTEG; FIELD=OPEN; STRICT=ON; DEPTH=DEEP; LENS=SYS]
Integrate BPL into the overall architecture.

### Crisis ops

BUDDY-OPS-U-05121740 [MODE=ANALYZE; FIELD=OPEN; STRICT=ON; PRIORITY=P0]
#CONTEXT Payments succeeded, tickets missing.
#ASK Define immediate containment.

### Closing a field

BUDDY-CCD-U-05121756 [MODE=REFLECT; FIELD=CLOSE]
Field closed. Store invariants only.

---

## 10. Canonical Definition

BPL is a translation-layer cognitive interface protocol that formalizes how intent, context, authority, and constraints are signaled between a human and an AI, ensuring bounded interpretation and continuity before any reasoning or execution occurs.

---

## 11. Design Invariants (LOCK)

- BPL never executes  
- BPL never carries value  
- BPL never decides truth  
- BPL constrains interpretation upstream  
- All evolution is additive  

---

**END — BPL v1.0 (FINAL)**
