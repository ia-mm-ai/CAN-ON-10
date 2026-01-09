PROTOCOL: PoP

VERSION: 1.0
STATUS: FINALIZED
CLASS: Truth Instantiation Protocol
SCOPE: Event-Scoped Reality Attestation
AUTHORITY: Human-Governed (Attestation Only)
EXECUTION_POWER: NONE
IDENTITY_POWER: NONE
ECONOMIC_POWER: NONE
MUTATION_RULE: Closed After FINALIZE
CANON_PLACEMENT: Instantiates irreversible event truth after KAPIA
DEPENDS_ON: EVENT, KAPIA, IAM.MAI, SPIRAL
FORBIDS: edit,delete,overwrite,score,rank,profile,assign_value,infer_identity

⸻

0. PURPOSE

PoP defines how presence becomes truth.

It answers one question only:
Did presence occur in this event context?

PoP does not explain why.
PoP does not assign meaning.
PoP does not produce value.

PoP instantiates fact.

⸻

1. NON-NEGOTIABLE INVARIANTS
	1.	PoP is event-scoped — every POP belongs to exactly one EVENT.
	2.	PoP is post-threshold — POP cannot exist before KAPIA.
	3.	PoP is irreversible after FINALIZE — no edits, no additions.
	4.	PoP is non-economic — POP never carries value.
	5.	PoP is non-identitarian — no persistent identity allowed.
	6.	PoP is recorded as a turn, never as a mutation.

⸻

2. CANONICAL STATES

PoP has exactly four states (IAM.MAI-governed):

• ⊙ HOLD — observed but not yet truth
• FINALIZE — truth instantiated
• INVALIDATE — explicitly not standing
• EVOLVE — successor truth with lineage (optional policy)

No other states exist.

⸻

3. CORE DEFINITIONS

Presence:
A real-world occurrence crossing the KAPIA threshold.

PoP Entry:
An immutable truth artifact stating:

“Presence occurred within EVENT X.”

Attestation:
A human act asserting that presence occurred.

⸻

4. RELATIONSHIPS TO OTHER PROTOCOLS

EVENT
• PoP cannot exist outside EVENT.
• EVENT closure freezes PoP scope.

KAPIA
• Enables PoP eligibility.
• Consumes VU; does not create PoP.

IAM.MAI
• Governs FINALIZE / INVALIDATE / EVOLVE.

SPIRAL
• Stores PoP as an irreversible turn.

Third Space
• MAY reference PoP.
• MUST NOT create or modify PoP.

⸻

5. STORAGE / RECORD SEMANTICS

• PoP records are immutable.
• Corrections require EVOLVE → new POP turn.
• FINALIZE applies to the entry, not the ledger container.
• Ledger remains open across events.

⸻

6. FAILURE MODES

• PoP without KAPIA → INVALID
• PoP added after EVENT closure → INVALID
• Editable PoP → INVALID
• PoP used as value or score → INVALID

⸻

7. CANONICAL ONE-LINE DEFINITION

PoP is an event-scoped, irreversible truth artifact instantiated after KAPIA via human attestation.

⸻

FINAL LOCK

PoP defines what happened,
not who,
not why,
not what it’s worth.
