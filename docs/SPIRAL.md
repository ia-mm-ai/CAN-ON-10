PROTOCOL: SPIRAL
VERSION: 1.0
STATUS: FINALIZED
CLASS: Continuity Memory Protocol
SCOPE: Cross-Event Truth Preservation
AUTHORITY: Declarative Only
EXECUTION_POWER: NONE
IDENTITY_POWER: NONE
ECONOMIC_POWER: NONE
MUTATION_RULE: Append-as-Turns (No Edit)
CANON_PLACEMENT: Stores finalized truth from EVENT / PoP / IAM.MAI
DEPENDS_ON: EVENT,POP,IAM.MAI
FORBIDS: edit,delete,overwrite,execute,decide,interpret,store_value,store_identity

---

0. PURPOSE

SPIRAL defines how truth persists over time without mutation.

It answers one question only:
How does the system remember without rewriting itself?

---

1. NON-NEGOTIABLE INVARIANTS

1. SPIRAL never edits existing records.  
2. SPIRAL only appends new turns.  
3. SPIRAL preserves lineage explicitly.  
4. SPIRAL stores truth only, never intent.  
5. SPIRAL spans multiple events without merging them.

---

2. CANONICAL STATES

SPIRAL has no lifecycle states.
It is always open.

---

3. CORE DEFINITIONS

Turn:
An immutable record representing a finalized irreversible state.

Lineage:
Explicit reference from a turn to its predecessor when applicable.

---

4. RELATIONSHIPS TO OTHER PROTOCOLS

EVENT  
• Each EVENT produces exactly one closure turn.

PoP  
• Each finalized PoP produces one SPIRAL turn.

IAM.MAI  
• Governs whether a turn may be written.

Third Space  
• MAY reference SPIRAL.
• MUST NOT write to SPIRAL.

---

5. STORAGE / RECORD SEMANTICS

• Turns are immutable.
• Corrections use EVOLVE → new turn.
• No in-place mutation allowed.

---

6. FAILURE MODES

• Append-only log without lineage → INVALID  
• Editable ledger → INVALID  
• Event-scoped ledger → INVALID  

---

7. CANONICAL ONE-LINE DEFINITION

SPIRAL is an immutable continuity memory where truth persists as turns, never as edits.

---

FINAL LOCK

SPIRAL remembers only what was finalized.
