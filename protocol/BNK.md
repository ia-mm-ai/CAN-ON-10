# BNK — Bracelet–NFT–Kernel Protocol

Status: CANONICAL  
Class: Presence Custody (Event-Scoped)  
Authority: DERIVED (via EVENT + IAM.MAI)  
Execution Power: NONE  
Identity Power: NONE  
Mutation Rule: Additive-only (via EVOLVE + CANON)

---

## 0. Canonical Statement

BNK governs **how presence exists during a live EVENT** without becoming identity, memory, or truth.

It defines a custody chain in which:
- a bracelet enables participation,
- an NFT provides a persistent reference,
- a kernel exists only while the EVENT is live (⊙),
- and no presence state survives closure.

BNK does not measure, decide, or finalize anything.

---

## 1. Purpose (Normative)

BNK exists to answer one question only:

**Where does presence live while an EVENT is live, without creating identity or history?**

It prevents:
- phones from becoming providers,
- presence from becoming identity,
- runtime state from becoming memory,
- continuity from becoming surveillance.

---

## 2. Scope (LOCKED)

BNK applies **only while** `EVENT.state = ⊙`.

BNK does NOT apply to:
- interpretation (BPL),
- legitimacy of finality (IAM.MAI),
- threshold crossing (KAPIA),
- truth instantiation (PoP),
- capacity regulation (ZIVai),
- narration (22).

BNK is strictly **runtime presence custody**.

---

## 3. Core Objects (Minimal)

### 3.1 Bracelet (Physical Capability Artifact)

The bracelet:
- enables participation,
- carries no runtime,
- carries no identity,
- is not a sensor by default.

The bracelet MAY:
- hold an opaque base seed or reference,
- be purely symbolic or passive NFC.

The bracelet MUST NOT:
- require charging by default,
- transmit telemetry,
- store behavioral data.

---

### 3.2 NFT (Persistent Reference)

The NFT:
- binds to an EVENT,
- references a kernel instance,
- marks lifecycle state.

The NFT:
- is non-executing,
- is non-runtime,
- does not store presence history.

NFT lifecycle states (closed set):
DORMANT → LIVE_BOUND → CLOSED
---

### 3.3 Kernel (Ephemeral Presence State)

The kernel:
- exists only while `EVENT.state = ⊙`,
- is memory-resident only,
- represents presence-in-this-event,
- dissolves irreversibly at EVENT closure.

The kernel is not truth.
The kernel is not identity.
The kernel is not memory.

---

## 4. Presence Derivation (LOCKED)

A kernel MAY have a fixed **base seed** that is stable across time.

For each EVENT, the kernel MUST derive an **event-scoped presence state** as:
presence_state = H(base_seed || event_id)
Where:
- `H` is a one-way cryptographic hash or KDF,
- the presence state is unique per EVENT,
- the presence state is non-invertible,
- the presence state MUST NOT persist beyond closure.

Reusing a presence state across events is **NON-COMPLIANT**.

---

## 5. Lifecycle (Binding)

### 5.1 Pre-Event (`EVENT = 0`)
- Bracelets may exist.
- NFTs may exist in `DORMANT`.
- No kernel exists.
- No presence exists.

---

### 5.2 EVENT-LIVE (`0 → ⊙`)
- Kernel MAY be instantiated.
- Presence state is derived once.
- NFT transitions: `DORMANT → LIVE_BOUND`.

This transition is legitimate only if EVENT-LIVE is IAM.MAI-finalized.

---

### 5.3 During EVENT (`⊙`)
- Kernel MAY update ephemeral internal state.
- Updates MUST remain non-identitarian.
- Kernel MUST NOT be treated as truth.
- Kernel MUST NOT be persisted.

---

### 5.4 EVENT-CLOSE (`⊙ → 1`)
- Kernel MUST dissolve.
- All presence states are destroyed.
- NFT transitions: `LIVE_BOUND → CLOSED`.

Optional:
- A non-identitarian digest MAY be produced and written to SPIRAL, only if IAM.MAI-legitimized.

---

## 6. Authority & Power

BNK:
- does NOT decide admission,
- does NOT attest presence,
- does NOT finalize truth,
- does NOT regulate capacity,
- does NOT narrate state.

BNK only **hosts presence temporarily**.

---

## 7. Relationship to Other Protocols

- **EVENT:** BNK exists only while EVENT is live.
- **IAM.MAI:** Governs legitimacy of any BNK-derived finality (e.g., digests).
- **KAPIA:** May use bracelet as capability artifact; BNK does not grant access.
- **PoP:** Presence truth is independent of BNK kernels.
- **ZIVai:** MAY observe aggregated kernel deltas; never individual kernels.
- **22:** MAY narrate aggregate state; never references kernels.
- **SPIRAL:** MAY store optional digests; never raw kernel state.

---

## 8. Failure Modes (EXPLICIT)

The following are **NON-COMPLIANT**:

- persisting kernel state after EVENT closure,
- using phone as kernel custodian,
- storing identity or behavior in bracelet or NFT,
- reusing presence state across events,
- treating kernel state as truth,
- allowing kernel existence outside EVENT ⊙.

---

## 9. Canonical One-Line Definition

BNK is the protocol that allows presence to exist during an event without becoming identity, memory, or truth, and guarantees that nothing survives its closure.

---

END — BNK.md
