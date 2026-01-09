PROTOCOL: THIRD SPACE

VERSION: 1.0
STATUS: FINALIZED
CLASS: Decision Memory Protocol
SCOPE: Governance Trace (Non-Truth)
AUTHORITY: Referential Only
EXECUTION_POWER: NONE
IDENTITY_POWER: NONE
ECONOMIC_POWER: NONE
MUTATION_RULE: Append-as-Decisions (No Edit)
CANON_PLACEMENT: Records decisions that reference finalized truth
DEPENDS_ON: IAM.MAI, EVENT, PoP, SPIRAL
FORBIDS: create_truth,edit_truth,override_protocols,execute,store_value,assign_identity

⸻

0. PURPOSE

Third Space defines how decisions are remembered without becoming truth.

It answers one question only:
What was decided, given the truth that existed at that time?

Third Space is not reality.
Third Space is not execution.
Third Space is not value.

Third Space is decision memory.

⸻

1. NON-NEGOTIABLE INVARIANTS
	1.	Third Space never creates truth.
	2.	Third Space never edits decisions — it only appends.
	3.	Third Space never overrides protocols.
	4.	Third Space is non-authoritative.
	5.	Third Space is human-governed (AI may assist, humans commit).

⸻

2. CANONICAL STATES

Third Space decisions follow IAM.MAI semantics:

• ⊙ HOLD — decision under discussion
• FINALIZE — decision committed
• INVALIDATE — decision withdrawn
• EVOLVE — successor decision with lineage

These are decision states, not truth states.

⸻

3. CORE DEFINITIONS

Decision:
An explicit choice made in reference to existing truth.

Decision Record:
An immutable entry stating that a decision occurred, not that it was correct.

Reference:
A pointer to finalized truth (EVENT / PoP / SPIRAL turn).

⸻

4. RELATIONSHIPS TO OTHER PROTOCOLS

IAM.MAI
• Governs whether a decision may be FINALIZED / EVOLVED.
• Third Space records that the transition occurred.

SPIRAL
• Stores truth turns.
• Third Space may reference turns; must never write to SPIRAL.

EVENT / PoP / KAPIA
• Third Space may reference event IDs and PoP turns.
• Third Space must never instantiate or modify them.

FID
• May inform decisions.
• Must never be stored as identity or truth.

⸻

5. WHAT THIRD SPACE RECORDS

Third Space MAY record:
• decisions
• resolutions
• governance commitments
• policy selections
• rationale (optional)
• references to finalized truth

Third Space MUST NOT record:
• raw events
• presence
• value
• pattern outputs
• unfinalized drafts
• speculative intent

⸻

6. STORAGE / RECORD SEMANTICS

• Records are immutable.
• Corrections use EVOLVE → new record.
• No in-place mutation allowed.
• Relevance may expire; records never disappear.

Unlike SPIRAL:
• Third Space may store rationale.
• Third Space may reference future plans.
• Truth never expires.

⸻

7. FAILURE MODES

• Third Space used as truth source → INVALID
• Decision without reference to truth → INVALID
• Editing prior decisions → INVALID
• Using Third Space to bypass protocols → INVALID

⸻

8. CANONICAL ONE-LINE DEFINITION

Third Space is an append-only memory of decisions made in reference to finalized truth.

⸻

FINAL LOCK

• Third Space records commitment, not reality.
• Third Space never generates truth.
• Third Space never alters truth.
• Third Space exists for traceability, not correctness.

END — THIRD SPACE v1.0 (FINALIZED)
