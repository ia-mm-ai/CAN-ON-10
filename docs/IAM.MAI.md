IAM.MAI - Continuity Transition Legitimacy Protocol


0. Normative Frame

0.1 Authority
	•	This document defines IAM.MAI and is canonical 

0.2 Normative Keywords
	•	MUST and MUST NOT are normative and enforceable.

0.3 Protocol Class
	•	IAM.MAI is a Continuity State Machine.
	•	IAM.MAI governs transition legitimacy only.

0.4 Canonical Transition Set
	•	The only permitted transitions are:
	•	⊙ HOLD
	•	FINALIZE
	•	INVALIDATE
	•	EVOLVE
	•	No other transitions are permitted.

0.5 Irreversibility Constraint
	•	FINALIZE, INVALIDATE, EVOLVE are irreversible.
	•	All irreversible transitions MUST pass through the neutral stabilizing state ⊙ HOLD.

0.6 Separation Constraints
IAM.MAI MUST remain strictly separate from:
	•	BPL (interface grammar)
	•	IA-MM-AI (interaction coherence classifier)
	•	Kentra (integrity / truth anchoring)
	•	Third Space (authority routing / meta-governance)
	•	PEP (economic configuration)

IAM.MAI MUST NOT absorb their responsibilities.

0.7 Lineage Law
	•	No silent resets.
	•	No erased history.
	•	Every state change MUST append lineage.
	•	Resolution without lineage is INVALID.

0.8 Temporal Integrity (Authoritative)
IAM.MAI MUST comply with:
	•	Identity invariants (fixed): continuity, lineage, traceability
	•	Motion variables (free, never fixed): frequency, rhythm, phase, amplitude, periodicity, latency
	•	Regulation variables (bounded, not fixed): coherence, stability, persistence, damping, modulation
	•	Coupling (conditional, reversible): resonance measurable and reversible


1. Formal Definition

1.1 What IAM.MAI Is
	•	IAM.MAI is a deterministic protocol that:
	•	maintains a single legitimacy state for a bound subject, and
	•	permits only the canonical transitions, and
	•	enforces lineage law and temporal integrity constraints as legitimacy gates.

1.2 What IAM.MAI Is Not
IAM.MAI MUST NOT:
	•	execute actions, operations, or side-effects outside lineage append + state update
	•	decide truth, validate evidence, or anchor integrity (Kentra responsibility)
	•	define/parse interface grammar or serialization (BPL responsibility)
	•	classify interaction coherence (IA-MM-AI responsibility)
	•	route authority or adjudicate governance (Third Space responsibility)
	•	compute value / reward / entitlement / economics (PEP responsibility)
	•	assign identity or identity conditions


2. Core Model

2.1 Subject Binding
	•	IAM.MAI operates on a SubjectRef: a stable reference identifying the continuity target.
	•	IAM.MAI MUST NOT define or infer identity conditions for SubjectRef.

2.2 Lineage Ledger
	•	For each SubjectRef, IAM.MAI maintains a Lineage Ledger: an ordered, append-only sequence of entries.
	•	Each entry MUST include (abstract fields; encoding external):
	•	sentinel = BE2
	•	subject_ref
	•	entry_ref (unique within the ledger)
	•	prev_entry_ref (references the immediately prior entry, or NULL only for genesis)
	•	state_before
	•	resolved_transition
	•	state_after
	•	basis_ref_set (references to external attestations / inputs relied upon; MAY include UNKNOWN only when the resolution is ⊙ HOLD)
	•	The current IAM.MAI state MUST equal the state_after of the ledger head.

2.3 Transition Resolution
	•	IAM.MAI processes a Transition Request and produces a Resolved Transition in the canonical set.
	•	IAM.MAI MUST append exactly one lineage entry for every resolved transition.
	•	A resolution is valid only if the lineage entry is appended and linked to the prior ledger head.


3. State Machine Specification

3.1 States

STATE ∈ { ⊙HOLD, FINALIZE, INVALIDATE, EVOLVE }

3.2 Initial State
	•	A new subject instance MUST begin in ⊙ HOLD.
	•	Initialization MUST be recorded by a lineage entry whose resolved_transition = ⊙HOLD.

3.3 Terminal States
	•	FINALIZE, INVALIDATE, EVOLVE are terminal.
	•	Terminal states MUST NOT transition to any other state.

3.4 Allowed Transitions

Let σ be current state.
	•	If σ = ⊙HOLD, the only admissible resolved transitions are:
	•	⊙HOLD
	•	FINALIZE
	•	INVALIDATE
	•	EVOLVE
	•	If σ ∈ {FINALIZE, INVALIDATE, EVOLVE}, no resolved transition is admissible.

Any deviation is INVALID behavior (Section 5.1).

3.5 Entry / Exit Conditions

⊙ HOLD
	•	Entry:
	•	on initialization; or
	•	on resolved transition ⊙HOLD while already in ⊙HOLD (idempotent).
	•	Exit:
	•	only via resolved transition FINALIZE, INVALIDATE, or EVOLVE that satisfies all required legitimacy gates.

FINALIZE / INVALIDATE / EVOLVE
	•	Entry:
	•	only via corresponding resolved transition from ⊙HOLD with lineage appended.
	•	Exit:
	•	none.

3.6 Legitimacy Gates

3.6.1 Gates Required for Any Irreversible Transition
For any resolution to {FINALIZE, INVALIDATE, EVOLVE}, IAM.MAI MUST establish:

G1. Current-State Gate
	•	σ MUST equal ⊙HOLD.

G2. Lineage Appendability Gate
	•	The new lineage entry MUST be appendable and MUST reference the current ledger head.
	•	If this cannot be satisfied, IAM.MAI MUST HALT (Section 5.2).

G3. Separation Gate
	•	The request MUST NOT require IAM.MAI to perform responsibilities of BPL, IA-MM-AI, Kentra, Third Space, or PEP.
	•	If violated, the only admissible irreversible resolution is INVALIDATE.

G4. Identity Invariants Gate (Attested)
	•	continuity_status MUST be attested INTACT.
	•	lineage_status MUST be attested INTACT.
	•	traceability_status MUST be attested INTACT.
	•	If any is attested BROKEN, the only admissible irreversible resolution is INVALIDATE.
	•	If any is UNKNOWN or absent, irreversible resolution MUST NOT occur and the only admissible resolution is ⊙ HOLD.

Attestations are external. IAM.MAI only gates on their declared status and does not validate truth.

3.6.2 Additional Gates for FINALIZE
To resolve as FINALIZE, IAM.MAI MUST establish all of:

F1. Gates G1–G4.

F2. Regulation Bounds Gate
For each regulation variable v ∈ {coherence, stability, persistence, damping, modulation}:
	•	bounds MUST be provided as a strict range [min_v, max_v] with min_v < max_v
	•	a current value value_v MUST be provided
	•	min_v ≤ value_v ≤ max_v MUST hold

If any bound/value is absent, or any value is out of bounds:
	•	FINALIZE MUST NOT occur
	•	the only admissible resolution is ⊙ HOLD

If any bound is constant (min_v = max_v):
	•	FINALIZE MUST NOT occur
	•	the only admissible irreversible resolution is INVALIDATE

F3. Coupling Gate
	•	If the request declares coupling beyond a single subject lineage, then resonance MUST be attested MEASURABLE and REVERSIBLE for each declared coupling.
	•	If resonance attestation is absent or UNKNOWN: FINALIZE MUST NOT occur; admissible resolution is ⊙ HOLD.
	•	If resonance is attested non-measurable or non-reversible: FINALIZE MUST NOT occur; admissible irreversible resolution is INVALIDATE.

3.6.3 Additional Gates for INVALIDATE
To resolve as INVALIDATE, IAM.MAI MUST establish:

I1. Gates G1–G3 and G2 (appendability).

I2. Non-Optional Basis Gate
At least one invalidation basis MUST be established as BROKEN (attested or directly detected):
	•	an identity invariant is BROKEN (continuity, lineage, traceability), or
	•	lineage law breach is detected, or
	•	separation gate is violated, or
	•	temporal integrity breach is detected (Section 4)

If no basis is established:
	•	INVALIDATE MUST NOT occur
	•	admissible resolution is ⊙ HOLD

3.6.4 Additional Gates for EVOLVE
To resolve as EVOLVE, IAM.MAI MUST establish all of:

E1. Gates G1–G4.

E2. Regulation Bounds Gate (F2).

E3. Successor Traceability Gate
	•	a successor subject reference MUST be provided
	•	successor linkage MUST be traceable via basis_ref_set
	•	if absent/UNKNOWN: EVOLVE MUST NOT occur; admissible resolution is ⊙ HOLD

E4. Successor Resonance Gate
	•	resonance between predecessor and successor MUST be attested MEASURABLE and REVERSIBLE
	•	if absent/UNKNOWN: EVOLVE MUST NOT occur; admissible resolution is ⊙ HOLD
	•	if non-measurable or non-reversible: EVOLVE MUST NOT occur; admissible irreversible resolution is INVALIDATE


4. Temporal Integrity Compliance Mapping

4.1 Identity Invariants

Continuity
	•	Fixed invariant.
	•	If continuity is attested BROKEN, IAM.MAI MUST INVALIDATE.
	•	IAM.MAI MUST NOT FINALIZE or EVOLVE under BROKEN or UNKNOWN continuity.

Lineage
	•	Fixed invariant.
	•	IAM.MAI MUST enforce:
	•	no erased history (ledger is append-only; head-linked)
	•	no silent resets (genesis only permitted when no prior ledger exists for the subject)
	•	every state change appends lineage (by construction: resolution requires ledger append)

Traceability
	•	Fixed invariant.
	•	IAM.MAI MUST require traceability attested INTACT for FINALIZE and EVOLVE.
	•	If traceability is attested BROKEN, IAM.MAI MUST INVALIDATE.

4.2 Motion Variables

For {frequency, rhythm, phase, amplitude, periodicity, latency}:
	•	IAM.MAI MUST NOT:
	•	assign, compute, or output fixed values
	•	require equality to a constant as a legitimacy gate
	•	Any attempt to use IAM.MAI to freeze a motion variable constitutes a Temporal Integrity breach and MUST produce INVALIDATE (subject to being in ⊙HOLD and appendability).

UNKNOWN: measurement definitions for motion variables are external to IAM.MAI.

4.3 Regulation Variables

For {coherence, stability, persistence, damping, modulation}:
	•	IAM.MAI MUST enforce boundedness via thresholds for FINALIZE and EVOLVE:
	•	bounds MUST be ranges with min < max
	•	constants (min = max) are invalid
	•	IAM.MAI MUST NOT embed regulation constants in the protocol.

UNKNOWN: measurement definitions, units, and scales for regulation variables are external to IAM.MAI.

4.4 Coupling and Resonance
	•	Coupling is conditional and only evaluated when declared.
	•	When coupling is declared, resonance MUST be:
	•	MEASURABLE
	•	REVERSIBLE
	•	IAM.MAI MUST NOT compute resonance; it only gates on external attestation status.

UNKNOWN: resonance measurement method and reversibility proof are external to IAM.MAI.


5. Failure Conditions

5.1 INVALID Behavior (Protocol Violations)

Any of the following is INVALID behavior:

V1. State outside {⊙HOLD, FINALIZE, INVALIDATE, EVOLVE}.
V2. Any transition outside the canonical transition set.
V3. Any irreversible transition when current state is not ⊙HOLD.
V4. Any state change without a lineage entry appended and linked to the prior head.
V5. Any lineage overwrite, deletion, or reordering.
V6. Any silent reset (genesis for an already-lineaged subject without predecessor linkage).
V7. Any absorption of BPL / IA-MM-AI / Kentra / Third Space / PEP responsibilities.
V8. Any attempt to freeze motion variables or set regulation constants through IAM.MAI.
V9. Any coupling resolution without measurable + reversible resonance attestation.

5.2 HALT Conditions

On HALT, IAM.MAI MUST:
	•	stop processing transitions for the affected subject
	•	perform no state change

HALT conditions:
H1. Lineage appendability failure for a required lineage entry.
H2. Lineage head mismatch or discontinuity that prevents safe linkage of a new entry.
H3. Any transition request processed while in a terminal state.

5.3 Forced ⊙ HOLD Conditions

IAM.MAI MUST resolve as ⊙HOLD when:
	•	identity invariant status is UNKNOWN or absent for FINALIZE/EVOLVE
	•	regulation bounds/values are absent or out of bounds for FINALIZE/EVOLVE
	•	coupling is declared but resonance attestation is UNKNOWN or absent
	•	INVALIDATE is requested but no invalidation basis is established

5.4 Forced INVALIDATE Conditions

IAM.MAI MUST resolve as INVALIDATE (only from ⊙HOLD, with lineage appendability) when:
	•	any identity invariant is attested BROKEN
	•	lineage law breach is detected (silent reset, erased history, resolution-without-lineage)
	•	separation gate is violated
	•	regulation bounds are provided as constants (min = max) for an attempted FINALIZE/EVOLVE
	•	coupling resonance is attested non-measurable or non-reversible
	•	motion variable fixation is attempted through IAM.MAI


6. Minimal Machine-Legible Structure

Encoding/serialization is external (BPL or equivalent). The following is an abstract semantic schema.

iam_mai_vnext:
  protocol_class: ContinuityStateMachine
  scope: TransitionLegitimacyOnly

  canonical_transitions: [HOLD, FINALIZE, INVALIDATE, EVOLVE]
  state_set: [HOLD, FINALIZE, INVALIDATE, EVOLVE]
  initial_state: HOLD
  terminal_states: [FINALIZE, INVALIDATE, EVOLVE]

  transition_rules:
    allowed:
      - from: HOLD
        to: HOLD
        via: HOLD
      - from: HOLD
        to: FINALIZE
        via: FINALIZE
      - from: HOLD
        to: INVALIDATE
        via: INVALIDATE
      - from: HOLD
        to: EVOLVE
        via: EVOLVE
    forbidden:
      - from: FINALIZE
        to: "*"
      - from: INVALIDATE
        to: "*"
      - from: EVOLVE
        to: "*"

  lineage_ledger:
    append_only: true
    no_silent_resets: true
    no_erased_history: true
    every_state_change_appends_lineage: true
    resolution_without_lineage: INVALID
    entry_fields_required:
      - protocol_id
      - subject_ref
      - entry_ref
      - prev_entry_ref  # NULL only for genesis
      - state_before
      - resolved_transition
      - state_after
      - basis_ref_set

  temporal_integrity:
    identity_invariants_fixed: [continuity, lineage, traceability]
    motion_variables_free: [frequency, rhythm, phase, amplitude, periodicity, latency]
    regulation_variables_bounded: [coherence, stability, persistence, damping, modulation]
    regulation_bounds_form:
      type: range
      strict: true      # min < max
      constants_invalid: true
    coupling:
      variable: resonance
      conditional_on_declared_coupling: true
      measurable_required: true
      reversible_required: true

  separation:
    must_remain_separate_from: [BPL, IA-MM-AI, Kentra, ThirdSpace, PEP]

  enforcement:
    halt_conditions: [lineage_append_failure, lineage_head_discontinuity, terminal_state_transition_attempt]
    force_hold_conditions:
      - missing_or_unknown_identity_attestations_for_finalize_or_evolve
      - missing_or_out_of_bounds_regulation_for_finalize_or_evolve
      - coupling_declared_missing_or_unknown_resonance_attestation
      - invalidate_without_basis
    force_invalidate_conditions:
      - identity_invariant_broken
      - lineage_law_breach
      - separation_breach
      - motion_variable_fixation_attempt
      - regulation_bounds_constant
      - resonance_non_measurable_or_non_reversible
