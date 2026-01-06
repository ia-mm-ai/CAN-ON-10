Buddy Protocol Language (BPL) - BE2 Canonical Specification

0. Normative terms

0.1. MUST / MUST NOT / MAY are requirement keywords:
	•	MUST: required for conformance.
	•	MUST NOT: prohibited for conformance.
	•	MAY: optional; if implemented, the behavior is constrained by this specification.

0.2. Determinism requirement: for a fixed (protocol_version, system_constraints, input_message), the result of BE2 evaluation is a single, fully determined output (including envelope type, normalization, precedence application, and guidance formatting).

⸻

1. Scope and non-scope

1.1. BE2 defines:
	•	a single-message interface header format,
	•	deterministic parsing + normalization,
	•	deterministic classification into exactly one of {VALID, INVALID, INCOMPLETE},
	•	deterministic application of SYSTEM vs HEADER constraint precedence,
	•	deterministic control-response behavior for INVALID and INCOMPLETE.

1.2. BE2 does not define:
	•	task reasoning, planning, execution, evaluation, optimization,
	•	governance, truth adjudication,
	•	interaction coherence classification,
	•	any semantics derived from payload text.

⸻

2. Surfaces, sources, and objects

2.1. Input message
A message is an ordered sequence of bytes.

2.2. Header line / Payload
	•	The header line is the byte sequence from index 0 up to (but excluding) the first LF byte (0x0A), or the entire message if no LF exists.
	•	The payload is the byte sequence after the first LF (0x0A), if present; otherwise it is the empty sequence.
	•	If the header line ends with a single CR byte (0x0D), that CR is removed from the header line for parsing (CRLF compatibility). This removal does not alter payload.

2.3. Authority sources (closed set)
	•	SYSTEM: externally supplied system constraints (if any) provided to the BE2 evaluator as an explicit input parameter.
	•	HEADER: the parsed BE2 header line of the input message.
	•	PAYLOAD: the payload bytes; non-authoritative.

2.4. Precedence (fixed)
SYSTEM > HEADER > PAYLOAD

2.5. Statelessness
BE2 evaluation is stateless across turns. Correlation is permitted only via TOKEN pass-through; TOKEN creates no stored state and carries no implied semantics at this layer.

⸻

3. Sentinel choice

3.1. The BPL sentinel token is BE2 (exactly).
BPL/2 is not used in this version.

3.2. The header line MUST begin at byte index 0 with the 3-byte ASCII sequence BE2. Any leading bytes before BE2 render the header non-admissible.

⸻

4. Lexical constraints

All constraints in this section apply to the header line only.

4.1. Allowed header bytes
The header line MUST consist solely of bytes from the following ASCII set:
	•	Letters: A–Z and a–z
	•	Digits: 0–9
	•	Symbols: _ - + / . =
	•	Space: 0x20

Any other byte in the header line ⇒ INVALID.

4.2. Token delimiter
	•	The delimiter between header tokens is one or more ASCII spaces (0x20).
	•	Tabs and all other whitespace are disallowed by 4.1.

4.3. Key lexical form
	•	A key token (before normalization) MUST match: 1*(ALPHA / "_") where ALPHA = A–Z / a–z.
	•	Keys are case-insensitive on input and normalized to uppercase.

4.4. Value lexical form
	•	A value token (before normalization) MUST match: 1*(ALPHA / DIGIT / "_" / "-" / "+" / "/" / ".").
	•	Values are case-insensitive on input and normalized to uppercase except TOKEN, which is preserved exactly as provided (byte-preserving within the ASCII constraints above).

4.5. Empty values
	•	For any KEY=VALUE token, VALUE MUST NOT be empty.
	•	Empty value handling is specified in §7 (classification rules).

⸻

5. Header grammar

5.1. Header is a single line; payload begins after the first LF (0x0A) if present (§2.2).

header-line   = "BE2" 1*SP req-mode 1*SP req-intent 1*SP req-alt *(1*SP opt-token)

SP            = %x20

req-mode      = mode-key "=" value
req-intent    = intent-key "=" value
req-alt       = alt-key "=" value

opt-token     = strict-token / field-token / token-token / sys-token

mode-key      = key-insensitive("MODE")
intent-key    = key-insensitive("INTENT")
alt-key       = key-insensitive("ALT")

strict-token  = key-insensitive("STRICT") "=" value
field-token   = key-insensitive("FIELD")  "=" value
token-token   = key-insensitive("TOKEN")  "=" value
sys-token     = key-insensitive("SYS")    "=" value

; value lexical constraints are in §4.4, and semantic constraints in §6.

; key-insensitive("X") means the input key may be any case variant of X.

5.3. Required positional tokens (locked)
	•	Immediately after BE2, tokens MUST appear in this exact order:
	1.	MODE=...
	2.	INTENT=...
	3.	ALT=...

Any deviation from required ordering ⇒ INVALID (not INCOMPLETE).

5.4. Permitted keys (closed set)
	•	Required keys: MODE, INTENT, ALT
	•	Optional keys: STRICT, FIELD, TOKEN, SYS
	•	Any other key in the header ⇒ INVALID.

5.5. Uniqueness
Each key in the closed set MUST appear at most once in the header line. Duplicate occurrence ⇒ INVALID.

⸻

6. Key semantics and constraints

6.1. MODE (required)
	•	Parsed as an opaque token value (after normalization).
	•	BE2 does not interpret MODE beyond syntax/normalization/precedence.

6.2. INTENT (required)
	•	Parsed as an opaque token value (after normalization).
	•	BE2 does not interpret INTENT beyond syntax/normalization/precedence.

6.3. ALT (required; “altitude”)
	•	Parsed as an opaque token value (after normalization).
	•	BE2 does not interpret ALT beyond syntax/normalization/precedence.

6.4. STRICT (optional; default behavior locked)
	•	Value domain after normalization: ON or OFF only.
	•	If STRICT is absent from the header and absent from SYSTEM constraints, the effective value is ON.

6.5. FIELD (optional; interface-only; locked constraint)
	•	Parsed as an opaque token value (after normalization).
	•	Additional prohibition (locked): after normalization, FIELD MUST NOT equal HOLD. If it equals HOLD ⇒ INVALID.
	•	No other semantics are defined at this layer.

6.6. TOKEN (optional; correlation only; locked)
	•	Value is byte-preserving: the exact value substring bytes from the header token after TOKEN= are preserved without case normalization.
	•	TOKEN has no semantics at this layer beyond correlation identifier pass-through.

6.7. SYS (optional; seven-layer pointer; locked)
	•	Value domain after normalization is exactly one of:
	•	L1, L2, L3, L4, L5, L6, L7
	•	If SYS is absent (and not supplied by SYSTEM constraints), the effective SYS target is the internal state UNKNOWN.
	•	UNKNOWN is an internal state label only; it is not serialized as a SYS= value in a header line.

⸻

7. Normalization and evaluation algorithm

7.1. Inputs to evaluation

The evaluator takes two inputs:
	•	MESSAGE: input message bytes
	•	SYSTEM_CONSTRAINTS: an optional set of key/value constraints, supplied out-of-band

SYSTEM_CONSTRAINTS is either empty or a mapping where:
	•	Keys are restricted to the closed set in §5.4.
	•	Values obey the same lexical + semantic constraints as header values for that key (§4.4 and §6.4–§6.7).
	•	TOKEN values in SYSTEM_CONSTRAINTS are also byte-preserving (no normalization).

7.2. Outputs of evaluation

Evaluation returns exactly one envelope:
	•	VALID
	•	INVALID
	•	INCOMPLETE

and either:
	•	for VALID: a routable record (defined in §8.1), or
	•	for INVALID/INCOMPLETE: a control response (defined in §8.2).

7.3. Header parsing (deterministic)

Given HEADER_LINE from §2.2 (after CR removal if applicable):

Step H0 — Sentinel check
	•	If HEADER_LINE[0..2] is not exactly ASCII "BE2" ⇒ INVALID.

Step H1 — Header byte set check
	•	If any byte in HEADER_LINE is outside the allowed set in §4.1 ⇒ INVALID.

Step H2 — Tokenization
	•	Split HEADER_LINE on one or more spaces (0x20) into a list TOKENS.
	•	TOKENS[0] MUST be exactly "BE2"; otherwise ⇒ INVALID.

Step H3 — Minimum token count for required axes
	•	If len(TOKENS) < 4 ⇒ INCOMPLETE.

Step H4 — Required positional tokens
Parse tokens at positions 1..3 as KEY=VALUE:
	•	TOKENS[1] MUST have key MODE (case-insensitive) ⇒ else INVALID
	•	TOKENS[2] MUST have key INTENT (case-insensitive) ⇒ else INVALID
	•	TOKENS[3] MUST have key ALT (case-insensitive) ⇒ else INVALID

If any of these three tokens:
	•	lacks exactly one = separator, or
	•	has a key violating §4.3, or
	•	has a value violating §4.4,
then ⇒ INVALID.

If any of these three required tokens has an empty value (e.g., MODE=) then ⇒ INCOMPLETE.

Step H5 — Optional tokens
For each TOKENS[i] where i >= 4:
	•	MUST be KEY=VALUE with exactly one =, else ⇒ INVALID
	•	key MUST satisfy §4.3, else ⇒ INVALID
	•	key MUST be one of {STRICT, FIELD, TOKEN, SYS} (case-insensitive), else ⇒ INVALID
	•	no duplicate keys, else ⇒ INVALID
	•	value MUST satisfy §4.4, else ⇒ INVALID
	•	empty value ⇒ INVALID (optional keys do not use INCOMPLETE)
	•	semantic checks:
	•	STRICT value after normalization MUST be ON or OFF, else ⇒ INVALID
	•	FIELD value after normalization MUST NOT be HOLD, else ⇒ INVALID
	•	SYS value after normalization MUST be one of L1..L7, else ⇒ INVALID
	•	TOKEN is preserved byte-for-byte; no case normalization is applied

7.4. Canonical normalization (deterministic)

If parsing succeeds (i.e., not INVALID/INCOMPLETE per §7.3):

N1 — Key normalization
	•	Normalize all keys to uppercase.

N2 — Value normalization
	•	For keys other than TOKEN: map a–z to A–Z in the value.
	•	For TOKEN: value is unchanged.

N3 — Defaulting
	•	If STRICT is absent in HEADER and absent in SYSTEM constraints, set effective STRICT to ON.

N4 — SYS absence state
	•	If SYS is absent in HEADER and absent in SYSTEM constraints, set effective SYS target state to UNKNOWN.

7.5. SYSTEM constraint application (deterministic)

After header normalization:

S0 — SYSTEM constraint validation
If SYSTEM_CONSTRAINTS violates §7.1, evaluation result is INVALID (control response reason SYSTEM_CONSTRAINTS).

S1 — Conflict check (non-bypassable precedence)
For each key K present in both SYSTEM and HEADER:
	•	Compare effective canonical values:
	•	For TOKEN: byte-for-byte equality
	•	For others: equality after normalization per §7.4
	•	If not equal ⇒ INVALID (reason SYSTEM_CONFLICT)

S2 — Effective value selection
For each key K in the closed set:
	•	If SYSTEM provides K, effective source is SYSTEM.
	•	Else if HEADER provides K, effective source is HEADER.
	•	Else:
	•	STRICT effective value is ON (source DEFAULT)
	•	SYS effective target state is UNKNOWN (source DEFAULT)
	•	all other absent keys remain absent (no value)

7.6. Envelope selection (total order)

Envelope is selected by this fixed priority:
	1.	If any INVALID condition is triggered in §7.3 or §7.5 ⇒ INVALID
	2.	Else if any INCOMPLETE condition is triggered in §7.3 ⇒ INCOMPLETE
	3.	Else ⇒ VALID

⸻

8. Emissions

8.1. Routable record for VALID (internal gate output)

When envelope is VALID, BE2 produces a routable record with:
	•	VERSION: fixed value identifying this spec version: BE2
	•	EFFECTIVE constraint set (values after precedence + defaulting):
	•	MODE (required; source HEADER only, because absence would have yielded INCOMPLETE)
	•	INTENT (required; source HEADER only)
	•	ALT (required; source HEADER only)
	•	STRICT (source SYSTEM or HEADER or DEFAULT)
	•	FIELD (if present; source SYSTEM or HEADER)
	•	TOKEN (if present; source SYSTEM or HEADER; byte-preserved)
	•	SYS (if present; source SYSTEM or HEADER; else SYS target state = UNKNOWN)
	•	PROVENANCE: for each key present in EFFECTIVE, the source tag in {SYSTEM, HEADER, DEFAULT}
	•	PAYLOAD_BYTES: the payload byte sequence (§2.2), passed through unchanged

BE2 does not add, remove, interpret, or transform payload bytes.

8.2. Control response for INVALID / INCOMPLETE (user-facing)

When envelope is INVALID or INCOMPLETE, the pipeline MUST terminate before any downstream task reasoning, and the assistant output MUST be exactly two lines:
	•	Line 1: the envelope literal (INVALID or INCOMPLETE)
	•	Line 2: deterministic minimal guidance per §8.3

No other bytes, lines, or content are permitted (no partial answers).

8.3. Minimal guidance formatting (deterministic)

8.3.1. INCOMPLETE guidance
Line 2 is a single space-delimited list of missing required items, in this fixed order:
MODE INTENT ALT (include only those missing or empty)

8.3.2. INVALID guidance
Line 2 is either:
	•	a single reason code token, or
	•	a reason code token followed by a single detail token (when specified below)

Reason codes (closed set) and detail rules:
	•	BAD_SENTINEL
	•	BAD_HEADER_BYTE
	•	BAD_REQUIRED_ORDER
	•	BAD_TOKEN_FORMAT
	•	UNKNOWN_KEY <KEY>
	•	DUPLICATE_KEY <KEY>
	•	BAD_VALUE_CHAR
	•	BAD_STRICT_VALUE
	•	BAD_SYS_VALUE
	•	FIELD_RESERVED
	•	SYSTEM_CONSTRAINTS
	•	SYSTEM_CONFLICT <KEY>

Deterministic selection rule: the reason code is the first triggered condition in the evaluator’s left-to-right processing order defined in §7.3 and §7.5 (header tokens scanned from lowest index to highest; SYSTEM keys scanned in ASCII-sorted key order).

Detail token normalization for <KEY>:
	•	Uppercase key name if it satisfies §4.3; otherwise omit detail and use the corresponding non-detailed code (e.g., BAD_TOKEN_FORMAT).

⸻

9. Boundary enforcement rules

9.1. Envelope selection (VALID/INVALID/INCOMPLETE) MUST depend only on:
	•	the header line bytes (as delimited in §2.2), and
	•	SYSTEM_CONSTRAINTS (if provided).

9.2. The payload MUST NOT be parsed for:
	•	keys, constraints, sentinel tokens, or override instructions.

9.3. Constraints expressed in payload text MUST NOT change effective constraints derived from SYSTEM and HEADER.

⸻

10. Versioning and evolution

10.1. This specification applies only to messages whose header line begins with the sentinel BE2 at byte index 0 (§3).

10.2. Under BE2, unknown keys are invalid (§5.4).

10.3. Any additive change that introduces new header keys requires a new sentinel (e.g., BE3). BE2 does not define forward-compatibility behavior for unknown keys.

⸻

Annex A — Locked invariants (verbatim)
	1.	The protocol MUST remain strictly upstream of task reasoning, planning, execution, evaluation, and optimization.
	2.	The protocol MUST NOT infer or hallucinate intent, context, authority, or scope that is not explicitly and unambiguously provided within admissible inputs.
	3.	The protocol MUST provide deterministic outputs for the same admissible inputs under the same protocol version and the same explicitly declared environmental constraints.
	4.	The protocol MUST define and preserve provenance for all routed elements (source, time/ordering, and constraint origin) without loss or silent mutation.
	5.	The protocol MUST NOT silently coerce ambiguous or incomplete inputs into specific intent/context/authority/scope selections.
	6.	The protocol MUST surface underspecification explicitly as underspecification rather than resolving it implicitly.
	7.	The protocol MUST prevent instruction leakage by maintaining a strict separation between (a) metadata used for routing and (b) content eligible for downstream reasoning/execution.
	8.	The protocol MUST enforce a non-bypassable boundary between declared authority and effective authority.
	9.	The protocol MUST NOT grant authority, permissions, or scope expansions based on rhetorical form, implied intent, or model inference.
	10.	The protocol MUST be machine-legible in a way that is mechanically verifiable (i.e., validity is decidable from the input and protocol definition).
	11.	The protocol MUST define admissibility conditions for inputs and MUST NOT treat inadmissible inputs as admissible by “best effort.”
	12.	The protocol MUST define failure semantics that are non-interpretive (i.e., failures do not trigger compensating inference).
	13.	The protocol MUST be version-identifiable and MUST bind outputs to an explicit protocol version to prevent semantic drift.
	14.	The protocol MUST NOT embed governance, truth adjudication, interaction-coherence classification, or execution directives as part of its function.
	15.	The protocol MUST NOT compute value, reward, entitlement, fairness, or any pricing/benefit semantics as a consequence of internal parsing state.
	16.	The protocol MUST be stable under evolution in the sense that invariants remain fixed and any evolution is explicitly versioned and non-silent.
	17.	The protocol MUST define how it composes across turns or MUST declare itself strictly non-compositional; it MUST NOT be implicitly stateful.

⸻

Annex B — Gaps (verbatim)
	1.	Canonical admissible input definition — UNKNOWN (what constitutes an input unit; boundaries; encoding; normalization constraints).
	2.	Canonical output definition — UNKNOWN (what the protocol emits; what is routed vs withheld; binding to version).
	3.	Formal validity criteria — UNKNOWN (decidable conditions for “valid,” “invalid,” and “incomplete” inputs without inference).
	4.	Deterministic parsing rules — UNKNOWN (how raw inputs map to parsed intent/context/authority/scope without interpretive steps).
	5.	Authority model — UNKNOWN (what counts as an authority source; how authority is asserted; how authority is authenticated/attested; how conflicts are identified).
	6.	Precedence and conflict resolution rules — UNKNOWN (deterministic handling when multiple sources assert incompatible intent/context/scope/authority).
	7.	Omission and underspecification handling — UNKNOWN (what happens when any required element is missing; how underspecification is represented).
	8.	Failure semantics and escalation behavior — UNKNOWN (reject vs partial accept vs quarantine; what downstream visibility exists when upstream fails).
	9.	Provenance and lineage representation — UNKNOWN (how to represent source, ordering, and constraint origin in a machine-verifiable way).
	10.	State model across turns — UNKNOWN (stateless vs stateful; if stateful, what is retained; how state affects admissibility and determinism).
	11.	Boundary enforcement mechanism — UNKNOWN (how to mechanically guarantee “upstream-only” and prevent downstream reasoning leakage through the interface layer).
	12.	Adversarial input handling constraints — UNKNOWN (how spoofed authority, scope expansion attempts, and instruction smuggling are detected/handled at the interface layer without invoking task reasoning).
	13.	Versioning and compatibility rules — UNKNOWN (how versions are identified, negotiated, and applied; how deprecations are handled without silent semantic change).
	14.	Interaction with external policies/constraints — UNKNOWN (how system constraints are represented upstream without turning into governance or execution logic).
	15.	Determinism dependencies — UNKNOWN (which environmental variables are permitted to affect parsing; how those variables are declared and bounded).

⸻

Annex C — Gap resolution index
	1.	Canonical admissible input definition → §2.1–§2.2, §3, §4, §5
	2.	Canonical output definition → §7.2, §8.1–§8.3
	3.	Formal validity criteria → §7.3–§7.6
	4.	Deterministic parsing rules → §7.3–§7.4
	5.	Authority model → §2.3–§2.4, §7.5
	6.	Precedence and conflict resolution rules → §2.4, §7.5
	7.	Omission and underspecification handling → §7.3 (INCOMPLETE), §8.3.1
	8.	Failure semantics and escalation behavior → §8.2–§8.3
	9.	Provenance and lineage representation → §8.1 (PROVENANCE), §7.5 (source selection)
	10.	State model across turns → §2.5
	11.	Boundary enforcement mechanism → §9
	12.	Adversarial input handling constraints → §4 (byte set), §5 (closed keys), §9 (payload non-authority)
	13.	Versioning and compatibility rules → §10
	14.	Interaction with external policies/constraints → §2.3 (SYSTEM), §7.1 and §7.5
	15.	Determinism dependencies → §0.2, §7.6
