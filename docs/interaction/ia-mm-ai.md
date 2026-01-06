IA-MM-AI — Canonical Specification v1.0

0. Identifier
	•	Protocol ID: IA-MM-AI
	•	Version: 1.0
	•	Classification outputs (only): TRUE | FALSE | EVOLVE

1. Normative Keywords

The key words MUST, MUST NOT, SHALL, SHALL NOT, SHOULD, SHOULD NOT, and MAY are to be interpreted as requirement levels.

2. Interaction Model

2.1 Interaction Boundary

An interaction is a finite ordered sequence of events.
	•	Start boundary: the first admissible event after canonicalization.
	•	Termination boundary: the last admissible event after canonicalization.
	•	Interruption: if upstream stops providing events, the interaction is the finite sequence received. No additional signal is required.

2.2 Context Scope

The only admissible signals for computation are:
	•	event payload text
	•	event order, represented by the event’s sequence index (0-based position in the canonicalized sequence)

All other signals are out of scope and MUST NOT affect computation.

3. Input Admissibility and Canonicalization

3.1 Input Type

The protocol input MUST be interpreted as:
	•	a sequence E = [e0, e1, ..., e(n-1)] where each ei is intended to be a text value.

3.2 Canonicalization Function

Define CANON(E_raw) -> E as follows:
	1.	If E_raw is not a finite sequence, set E = [].
	2.	Else, for each element x in E_raw, map to a string:
	•	if x is a string, keep it
	•	otherwise, replace it with the empty string ""
	3.	For each string s, apply TEXT_NORM(s) (Section 4.1).
	4.	Apply limits:
	•	MAX_EVENTS = 1024
	•	MAX_EVENT_CODEPOINTS = 8192
	•	If len(E) > MAX_EVENTS, keep the last MAX_EVENTS events and discard earlier events.
	•	For each event string, if its length in Unicode codepoints exceeds MAX_EVENT_CODEPOINTS, keep the prefix of length MAX_EVENT_CODEPOINTS and discard the remainder.

The output of CANON is the interaction context used by the protocol. No other data is admissible.

3.3 Total Function Requirement

For all possible E_raw, CANON(E_raw) is defined and returns a finite sequence. The protocol output is defined for all E_raw (Section 8).

4. Text Processing Primitives

4.1 Text Normalization

Define TEXT_NORM(s):
	1.	Replace all occurrences of "\r\n" with "\n".
	2.	Replace all remaining occurrences of "\r" with "\n".
	3.	Remove all U+0000 codepoints.
	4.	Leave all other codepoints unchanged.

4.2 Token Counting

Define separators as the set { U+0020 SPACE, U+0009 TAB, U+000A LF }.

Define TOKEN_COUNT(s) as the number of maximal contiguous substrings of s that contain no separators.

4.3 Marker Predicates

Let CONTAINS(s, p) be true iff substring p occurs in s.
	•	HAS_QMARK(s) = 1 iff CONTAINS(s, "?") else 0.
	•	HAS_BANG(s) = 1 iff CONTAINS(s, "!") else 0.
	•	HAS_FENCE(s) = 1 iff CONTAINS(s, "```") else 0.

Define HAS_LIST(s):
	1.	Split s into lines on "\n".
	2.	For each line, strip only leading { SPACE, TAB }.
	3.	Return 1 iff any stripped line matches one of:
	•	"-" followed by { SPACE or TAB }
	•	"*" followed by { SPACE or TAB }
	•	"+" followed by { SPACE or TAB }
	•	d "." followed by { SPACE or TAB }, where d is 1–3 ASCII digits (0–9)
	4.	Else return 0.

5. Feature Extraction

For each canonical event ei (a string), define the per-event feature tuple:

F(i) = (C(i), T(i), Q(i), B(i), FENCE(i), LIST(i))

Where:
	•	C(i) = number of Unicode codepoints in ei
	•	T(i) = TOKEN_COUNT(ei)
	•	Q(i) = HAS_QMARK(ei)
	•	B(i) = HAS_BANG(ei)
	•	FENCE(i) = HAS_FENCE(ei)
	•	LIST(i) = HAS_LIST(ei)

All components are non-negative integers; Q,B,FENCE,LIST ∈ {0,1}.

6. Windowing and Pattern Representation

6.1 Sliding Windows

Let:
	•	W = 4 (window size, in events)

For n = len(E), define windows only if n ≥ W.

For each window end index t (event index) where t ∈ {W-1, W, ..., n-1}, the window covers events:

[t-W+1, ..., t].

6.2 Window Aggregates

For each window end t, define sums:
	•	SC(t) = Σ_{k=t-W+1..t} C(k)
	•	ST(t) = Σ_{k=t-W+1..t} T(k)
	•	SQ(t) = Σ_{k=t-W+1..t} Q(k)  (integer in [0..W])
	•	SB(t) = Σ_{k=t-W+1..t} B(k)  (integer in [0..W])
	•	SFENCE(t) = Σ_{k=t-W+1..t} FENCE(k) (integer in [0..W])
	•	SLIST(t) = Σ_{k=t-W+1..t} LIST(k)  (integer in [0..W])

6.3 Binning Functions

Define LEN_BIN(SC):
	•	0 if SC == 0
	•	1 if SC ≤ 50*W
	•	2 if SC ≤ 150*W
	•	3 if SC ≤ 400*W
	•	4 otherwise

Define TOK_BIN(ST):
	•	0 if ST == 0
	•	1 if ST ≤ 10*W
	•	2 if ST ≤ 30*W
	•	3 if ST ≤ 80*W
	•	4 otherwise

6.4 Pattern Code

For each window end t, define the pattern code:

P(t) = ( LB(t), TB(t), SQ(t), SB(t), SFENCE(t), SLIST(t) )

Where:
	•	LB(t) = LEN_BIN(SC(t))
	•	TB(t) = TOK_BIN(ST(t))

Equivalence criterion: two windows are the same pattern iff their pattern codes are exactly equal.

6.5 Recurrence Threshold

Define:
	•	MIN_RUN = 3 (minimum contiguous windows with identical pattern code)

A pattern is considered recurrent only via contiguous runs of length ≥ MIN_RUN.

7. Delta and Delta-of-Delta

Let window indices range over t ∈ {W-1, ..., n-1}.

7.1 Step Delta Vector

For t ∈ {W, ..., n-1}, define the step delta vector:

D(t) = ( |P(t)[0]-P(t-1)[0]|, ..., |P(t)[5]-P(t-1)[5]| )

Define step magnitude:

DMAG(t) = max_j D(t)[j] for j ∈ {0..5}

7.2 Second-Order Delta Magnitude

For t ∈ {W+1, ..., n-1}, define:

DDMAG(t) = | DMAG(t) - DMAG(t-1) |

This is the protocol’s second-order delta signal.

7.3 Baseline and Reset
	•	Baseline for deltas is the immediately preceding window.
	•	The delta chain starts at the first defined index (t=W for DMAG, t=W+1 for DDMAG).
	•	Reset occurs at interaction start; no cross-interaction baseline exists.

8. Run Construction, Conflict Handling, and Output Mapping

8.1 Run Definition

A run is a maximal contiguous interval of window indices [a..b] such that:
	•	P(a) = P(a+1) = ... = P(b)
	•	a = W-1 or P(a-1) != P(a)
	•	b = n-1 or P(b) != P(b+1)

8.2 Stable Run

A run [a..b] is stable iff:
	•	its length L = b-a+1 satisfies L ≥ MIN_RUN
	•	and for all t ∈ {a+1, ..., b} where DMAG(t) is defined, DMAG(t) = 0

(Within a stable run, the pattern code is constant; step deltas inside the run are zero.)

8.3 Terminal Condition

Let n = len(E) after canonicalization.
	•	If n < W + MIN_RUN - 1, output MUST be FALSE.
	•	Else, compute pattern codes for all windows and construct runs.
	•	Let RUN_T be the run whose end index is b = n-1 (the run that includes the final window).
	•	If RUN_T is not stable, output MUST be FALSE.

8.4 EVOLVE Detection

Let RUN_B = RUN_T be the terminal stable run with code PB = P(bB).

Define PREV_STABLE_DIFF(RUN_B) as the stable run RUN_A = [aA..bA] such that:
	•	RUN_A is stable
	•	bA < aB
	•	P(bA) != PB
	•	and among all runs meeting the above, bA is maximal (nearest in time)

If no such RUN_A exists, EVOLVE is not satisfied.

If RUN_A exists, define:
	•	PA = P(bA)
	•	SHIFT = max_j |PB[j] - PA[j]|

Define the transition zone window indices:

Z = { t | t ∈ [bA+1 .. aB] ∧ t ∈ [W+1 .. n-1] }

If Z is empty, EVOLVE is not satisfied.

Define:

SPIKE = max_{t ∈ Z} DDMAG(t)

Define the EVOLVE thresholds:
	•	SHIFT_MIN = 2
	•	SPIKE_MIN = 2

EVOLVE is satisfied iff:
	•	SHIFT ≥ SHIFT_MIN AND
	•	SPIKE ≥ SPIKE_MIN

8.5 Output Precedence

Given the above:
	1.	If EVOLVE is satisfied, output MUST be EVOLVE.
	2.	Else (terminal stable run exists and EVOLVE not satisfied), output MUST be TRUE.
	3.	Else output MUST be FALSE.

This mapping is total and has no undefined cases.

9. Determinism Requirements

An implementation is conformant only if:
	•	CANON, feature extraction, windowing, pattern coding, run construction, delta computation, EVOLVE detection, and output precedence are implemented exactly as specified.
	•	For identical admissible inputs (after canonicalization), the emitted output token is identical.

No randomized procedure, nondeterministic library behavior, or external state is permitted to influence the output.

10. Internal State Model

10.1 Permitted Ephemeral State

During an interaction, an implementation MAY hold:
	•	canonical event strings E
	•	per-event features F(i)
	•	window aggregates SC, ST, SQ, SB, SFENCE, SLIST
	•	window codes P(t)
	•	run boundaries
	•	DMAG(t) and DDMAG(t) values

All such state is interaction-local only.

10.2 Prohibited State

An implementation MUST NOT:
	•	store or retain any interaction-derived data beyond termination
	•	create cross-interaction identifiers, fingerprints, embeddings, or linkage artifacts
	•	maintain per-participant profiles, traits, dispositions, or identity claims
	•	access external metadata or tool outputs for computation
	•	write interaction content or derived features to persistent logs, caches, or telemetry in a manner that survives termination

11. State Dissolution

At interaction termination (immediately after producing the output token):
	•	All interaction-local state described in Section 10.1 MUST be destroyed or made unreachable.
	•	Any storage locations holding canonical event strings or derived features MUST be cleared in a way that prevents reuse in subsequent interactions within the same process.
	•	No state from the interaction may be readable or recoverable by subsequent invocations of the protocol within the same implementation instance.

12. Non-Identity Constraint

For this protocol, identity modeling includes any within- or cross-interaction procedure that:
	•	assigns stable attributes to an entity, participant, or speaker;
	•	links separate interactions as belonging to the same participant;
	•	infers or persists traits, profiles, dispositions, or participant identity claims.

Implementations MUST NOT perform any such procedure.

All participant references present in event text are treated as uninterpreted text content only.

13. Adaptation Safety
	•	The reference algorithm and all constants in this specification are fixed.
	•	Implementations MAY optimize computation only if the optimization is extensionally equivalent: for every admissible input, output must match the reference algorithm exactly.
	•	Any change that modifies outputs for any admissible input is non-conformant.
	•	No cross-interaction learning, tuning, or parameter update is permitted.

14. Output Interface

14.1 Atomic Output Token

The protocol output MUST be exactly one token in UTF-8 with no leading or trailing whitespace:
	•	TRUE or
	•	FALSE or
	•	EVOLVE

No additional fields, metadata, reasons, confidences, annotations, or side-channel output is permitted in the same output channel.

14.2 Error Surface

The protocol defines no error outputs. All inputs are mapped to one of the three tokens via canonicalization and the total decision procedure.

15. Misuse-Resistance Boundary

Consumers, integrators, and downstream systems MUST apply the disallowed-interpretation and coupling prohibitions in Appendix B (D1), and additionally:
	•	The output token MUST NOT be used as an access-control, permissioning, sanctioning, entitlement, reward, punishment, pricing, or allocation signal.
	•	The output token MUST NOT be stored or aggregated in any way that creates a participant profile or cross-interaction linkage.
	•	The output token MUST NOT be relabeled or reinterpreted as factual correctness, deception detection, compliance adjudication, or governance decision.
	
	Appendix A — Locked Invariants (Normative, Verbatim)
	•	The protocol MUST be interaction-scoped.
•	The protocol MUST dissolve all internal state at interaction termination.
•	The protocol MUST NOT persist state, summaries, embeddings, identifiers, or derived features across interactions.
•	The protocol MUST NOT create or use any cross-interaction linkage mechanism.
•	The protocol MUST NOT model identity.
•	The protocol MUST NOT infer, store, or update any representation of stable traits, dispositions, profiles, or participant identity claims.
•	The protocol MUST treat all participant references as ephemeral within-interaction constructs only.
•	The protocol MUST be context-scoped to an explicitly bounded interaction context.
•	The protocol MUST NOT expand its effective scope beyond the defined interaction context.
•	The protocol MUST be delta-based within the interaction.
•	The protocol MUST derive deltas only from information available inside the same interaction.
•	The protocol MUST NOT use prior-interaction baselines or priors.
•	The protocol MUST output exactly one of: TRUE, FALSE, EVOLVE.
•	The protocol MUST NOT output additional categorical outcomes outside that set.
•	The protocol MUST remain non-sentient in representation and operation.
•	The protocol MUST NOT assert, imply, or require internal experience, intention, consciousness, or selfhood.
•	The protocol MUST NOT perform governance.
•	The protocol MUST NOT adjudicate truth.
•	The protocol MUST NOT execute actions or trigger side effects beyond emitting its classification output.
•	The protocol MUST NOT encode authorization, entitlement, reward, punishment, or pricing semantics in its output.
•	The protocol MUST be safe under adaptation.
•	The protocol MUST NOT adapt in a way that changes the outcome set, the interaction-scope constraint, the no-identity constraint, or the state-dissolution constraint.
•	The protocol MUST have defined behavior for all admissible interaction inputs within its declared scope.
•	The protocol MUST NOT rely on undefined behavior for corner cases (including early termination and insufficient data conditions).

Appendix B — Locked Design Decisions (Normative, Verbatim)

D1 — Outcome label semantics (MUST be non-truth, non-governance)
The tokens TRUE / FALSE / EVOLVE are coherence classification outputs only and MUST be interpreted as follows:
•	TRUE = Coherence established: within the defined interaction boundary, the system observes recurrent behavioral pattern(s) whose deltas converge within defined bounds such that coherence is stable under repetition.
•	FALSE = Coherence not established: within the defined interaction boundary, coherence is not established by termination, including cases of insufficient recurrence, unresolved contradiction, or persistent misalignment.
•	EVOLVE = Coherence transformed: within the defined interaction boundary, the system observes a stable transformation of the recurrent pattern such that the coherence regime changes (delta-of-delta indicates a durable shift), and that shift is itself recurrent enough to be recognized as transformation rather than noise.

Disallowed interpretations (explicit misuse boundary):
•	TRUE/FALSE MUST NOT be interpreted as factual truth/falsehood.
•	TRUE/FALSE/EVOLVE MUST NOT be interpreted as permission, sanction, entitlement, or authorization.
•	EVOLVE MUST NOT be used as a catch-all for “uncertainty” if the condition can be decided as FALSE under this spec.

⸻

D2 — Insufficient data handling (no extra outcomes allowed)
Because the protocol MUST output exactly one of {TRUE, FALSE, EVOLVE}:
•	If recurrence is insufficient to establish coherence by termination, the output MUST be FALSE (coherence not established).
•	EVOLVE is reserved only for transformation, not for “insufficient evidence.”

⸻

D3 — Output surface (atomic token only)
The protocol output MUST be exactly one token, one of:

TRUE | FALSE | EVOLVE

No additional fields, metadata, reasons, confidences, or annotations may be emitted in the same output channel.
(Any richer reporting is explicitly out of scope for IA-MM-AI and must be handled by a separate system.)

⸻

D4 — Determinism scope (locked)
Determinism applies to:
•	boundary parsing (interaction start/end; admissibility)
•	delta computation rules
•	recurrence thresholding rules
•	conflict-handling rules
•	mapping from computed state → {TRUE, FALSE, EVOLVE}

Given identical admissible inputs under identical boundary conditions, the same output MUST be produced.

⸻

D5 — Observation surface (locked to prevent feature creep / privacy leak)
Unless explicitly overridden by the spec, admissible signals are:
•	payload content within the interaction boundary (text)
•	timing/order within the same boundary (sequence index)

No external metadata, cross-session memory, embeddings, profile-like summaries, or tool outputs may be used unless explicitly admitted by the spec.
