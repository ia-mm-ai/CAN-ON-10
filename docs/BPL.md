BUDDY PROTOCOL LANGUAGE (BPL)

Official Canonical Specification
Version: 1.1 (Singular, Identity-Bearing)
Status: ACTIVE
Evolution Rule: Additive-only (no breaking changes)
Authority: Interface / Translation only
Value Interaction: NONE

This document is the only canonical definition of BPL.
All other forms (compressed, ergonomic, derived) must expand to this without semantic loss.

No parallel definitions exist.
No alternate interpretations are valid.

⸻

0. NORMATIVE INTENT

BPL is a translation-layer protocol whose sole function is to bind interpretation before reasoning or execution occurs.

It exists to prevent:
	•	ambiguity
	•	interpretive drift
	•	authority bleed
	•	hallucination
	•	false coherence

BPL operates upstream of intelligence.

If BPL is absent, the system is non-deterministic by definition.

⸻

1. CANONICAL PLACEMENT (LOCKED)
	•	Layer: Translation / Adaptation
	•	Type: Cognitive Interface Protocol
	•	Scope: Human ↔ AI co-agency
	•	Temporal Position: Pre-reasoning, pre-execution
	•	Mutability: Additive-only
	•	Governance Power: NONE
	•	Execution Power: NONE
	•	Truth Authority: NONE

BPL is not governance.
BPL is not execution.
BPL is not value-bearing.

BPL is an interpretive membrane.

⸻

2. WHAT BPL IS (AND IS NOT)

2.1 What BPL IS

BPL is:
	•	a deterministic interface grammar
	•	a declarative control surface
	•	a machine-parsable signal header
	•	a human-writable protocol
	•	a constraint on interpretation

Its role is analogous to:
	•	HTTP headers (not payloads)
	•	POSIX flags (not programs)
	•	ABI contracts (not implementations)

BPL defines how input is to be read, never what the answer should be.

⸻

2.2 What BPL IS NOT

BPL is not:
	•	a prompt
	•	a reasoning strategy
	•	a conversation format
	•	a decision protocol
	•	a governance system
	•	an execution rail

BPL never replaces:
	•	IAMMAI (transition legitimacy)
	•	IA-MM-AI (interaction coherence)
	•	Kentra (truth anchoring)
	•	Third Space (authority routing)

Any attempt to merge these layers is a protocol violation.

⸻

3. MESSAGE STRUCTURE (CANONICAL)

A BPL message has exactly two layers:
	1.	Signal Header — normative, authoritative
	2.	Payload — free-form, non-authoritative

Only the Signal Header has protocol authority.
Payload content cannot override header constraints.

⸻

4. SIGNAL HEADER — ABSTRACT FORM

The Signal Header must appear first.
BUDDY--- [PROPERTIES]
Everything following this line is payload.

⸻

5. HEADER COMPONENTS

5.1 CHANNEL — Routing Domain

Defines the cognitive container.

Normative values:
	•	CCD — Cognitive / Continuity Design
	•	SYS — Systems & Architecture
	•	OPS — Operational Execution
	•	EXP — Experimental / Sandbox

CHANNEL routes cognition.
CHANNEL does not assign authority.

⸻

5.2 ACTOR — Initiator

Defines who asserts the frame.

Normative values:
	•	U — Human initiator
	•	A — AI initiator (rare, explicit)
	•	X — External quoted source

ACTOR does not imply ownership or truth.

⸻

5.3 TOKEN — Correlation Identifier
	•	Free-form
	•	Opaque
	•	Non-semantic

Used only for:
	•	traceability
	•	grouping
	•	reference

TOKEN must never encode meaning or authority.

⸻

6. PROPERTIES BLOCK — CORE AXES (NORMATIVE)

Each axis answers exactly one question.
Axes are orthogonal and must not overlap.

Format:
[KEY=VALUE; KEY=VALUE; …]
6.1 MODE — Cognitive Stance (HOW to think)

MODE defines method and stance, not topic.

Canonical values:
	•	ARCH — architecture & invariants
	•	CCD — cognition & continuity design
	•	SYS — system mechanics
	•	OPS — operational execution
	•	DESIGN — product / experience design
	•	INTEG — integration & synthesis
	•	MAP — structural cartography
	•	META — language about language

Invariant: MODE is a stance, never a domain.

⸻

6.2 INTENT — Output Shape (WHAT to produce)

INTENT defines the form of output, not derivation.

Canonical values:
	•	DEFINE
	•	MAP
	•	DESIGN
	•	SPEC
	•	INTEG
	•	SIMPLIFY
	•	DIAGNOSE
	•	SOLVE
	•	STORY
	•	EXTRACT
	•	CRITIQUE
	•	TRANSLATE

Invariant: INTENT describes work type, not subject matter.

⸻

6.3 LAYER — Abstraction Altitude (WHERE in the stack)

Defines resolution and altitude.

Canonical values:
	•	GRAMMAR
	•	SPEC
	•	SYSTEM
	•	OBJECT
	•	OPS
	•	STORY
	•	META

Same MODE + INTENT at different LAYER values yields different valid outputs.

⸻

6.4 STRICT — Constraint Tightness

Controls tolerance for deviation.

Values:
	•	OFF — exploratory
	•	SOFT — guided flexibility
	•	ON — literal, no drift

When STRICT=ON, the system:
	•	must not infer missing intent
	•	must not widen scope
	•	must not soften tone
	•	must return UNKNOWN for undefineds

⸻

6.5 FIELD — Continuity State

Controls temporal evolution.

Values:
	•	OPEN — normal continuity
	•	HOLD — freeze evolution
	•	CLOSE — terminate field

FIELD governs continuity, not reasoning style.

⸻

7. DESCRIPTIVE AXES (NON-BINDING)

These axes do not enforce behavior.

7.1 PRES — Presence Orientation
	•	ON
	•	MID
	•	OFF

Interpretive hint only.

⸻

7.2 RES — Resonance Level
	•	LOW
	•	MID
	•	HIGH

Describes alignment, not authority.

⸻

8. SEMANTIC CONTRACT

Given a valid BPL header:
	1.	Header is parsed before payload
	2.	Reasoning is configured only from header
	3.	Payload inherits all declared constraints
	4.	No undeclared axis may be assumed

If a required axis is missing:
	•	return UNKNOWN, or
	•	request clarification (unless STRICT=ON)

⸻

9. INVARIANTS (LOCKED)

The following must never change:
	•	BPL never executes
	•	BPL never decides truth
	•	BPL never assigns identity
	•	BPL never governs transitions
	•	BPL only constrains interpretation
	•	Grammar evolution is additive-only

Violation of any invariant invalidates compliance.

⸻

10. COMPLIANCE TEST

A BPL header is valid if:
	•	each axis answers exactly one question
	•	no axis overlaps responsibility
	•	removing payload does not invalidate header

If these hold, the protocol is compliant.

⸻

11. IDENTITY LOCK (FINAL)

BPL is singular.

All versions across time:
	•	share identical invariants
	•	share identical semantics
	•	differ only in expression or compression

Any document that:
	•	changes authority
	•	adds execution
	•	alters semantics
	•	reassigns truth

is NOT BPL.

⸻

FINAL STATEMENT (NON-NEGOTIABLE)

BPL is the Translation-Layer Cognitive Interface Protocol that binds intent, context, authority, and scope before intelligence is applied, ensuring continuity, bounded interpretation, and system sovereignty.

END — BPL v1.1 (Canonical, Official, Singular)
