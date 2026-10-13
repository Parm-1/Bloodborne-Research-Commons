# BRC-PAD-SAMPLING-01 — independent source/API and cumulative integration review r1

Date: 2026-10-13. Outcome: **one actionable resolver-contract wording finding (F1); affected recheck required**. No other actionable defect found in the inspected pad source/API or cumulative integration scope. This is an independent review, not acceptance, integration, publication, merge or runtime authority. The reviewer did not author or substantially design the candidate and made no candidate/canonical edits.

## Exact frozen subject

Commons branch `research/brc-pad-sampling-01`, HEAD `639254582f7034ff82ffea03e84e18ff3d693d3a`, tree `f4726126c508b75ca1fdaa91c80cda31d7a87a12`, tag `brc-pad-sampling-candidate-r1`; independently matched, clean before and after inspection. Full dossier, RC-0024/RC-0025, frontier, author r1 and eleven-file delta were read.

Independently matched SHA-256 pins:

- Author r1: `de46b3b40e5228055c82af3bee1d7e44cef8443d7a0aab6f584d629405fbd5e4`.
- Dossier: `5a442f4fe14e6ce16399bca6f39ccb07d714177899c99553250bbda70d3dbc15`.
- RC-0024: `f1edb32963a58dc8e41c76db8dc8041d2f4cf18c868bf8ecb456e26b9465f25c`.
- RC-0025: `ba72553844e3aa8d8a2487861a8ef4b4a335dd260db4826ca69c09009eb4c8dd`.
- Frontier: `34580783d856a280815ded110743c0226e0cdd6bb5325fc8e2350f51da356427`.

Public bbport source `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`, was independently matched and clean. All fifteen declared whole-file blobs match both Git objects and current read-only bytes. The existing fifteen-file inventory is reused; each declared selected operation bound was inspected, not promoted into a whole framework audit. The incidental heap helper is excluded. No original/game input or caller was inspected or executed.

## F1 — name the required capability mask unambiguously

Locations: `knowledge/pad-sampling.md:39` and P16 at `knowledge/pad-sampling.md:86`. Both say “capabilities bit1”; P16 also says “bit1 absent” is the negative. The producer [runtime.c:204–205](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c#L204-L205) tests `capabilities & 1`, namely mask `0x1`, bit index 0. “Bit1” can instead mean bit index 1/mask `0x2`, which reverses the stated positive/negative lookup decision. This is a consequential ambiguity in the accepted setup predicate, not a style preference or missing runtime test.

A source-faithful positive has capabilities `0x1`, non-data/function selection and exact `YndgXqQVV7c#A#B`. The [import table:261](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/import_names.inc#L261), [lookup:263–278](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c#L263-L278) and [pad exports:757–765](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L757-L765) select ReadState through this route. The contradictory raw-field negative has the same exact NID/non-data setup but capabilities `0x2`: it returns 0 immediately. Capabilities 0 also refuse. With capabilities `0x1`, data-kind still returns 0 for this pad NID. Literal names and absent Read/motion-state mappings remain separate selected-route negatives, not global unsupported-functionality proof.

Repair condition: identify mask `0x1` and bit index 0 consistently in the explanation and P16 positive/negative, preserving the non-data, exact-NID, body-versus-binding and relocation limitations. Freeze a linked r2+ candidate/author receipt; keep r1 and this report immutable. Recheck these affected predicates and their resolver/import/relocation interaction only. No new runtime, ABI, hardware or unrelated test is needed.

## Producer, phases, fields and controls

The sixteen rows are conditional source/model reasoning, **not sixteen executed tests**. Their supplied API answers and clocks are hypothetical premises. Checker flags and author-generated expectations were not used as evidence of producer behavior.

| Cases | Independently checked positive and contradictory raw fields/phases |
|---|---|
| P1–P3 composite/scaling | [Host producer:499–553](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L499-L553), bindings and keyboard precedence support Return/Options without a pad, SOUTH/Cross plus Return/Options, D overriding left_x to255, and trigger32767 becoming255. Axis0 with disabled calibration/center0 gives128; official invalid-axis0 also defeats interpreting center as health. Mouse transformation is a later right-stick contribution. |
| P4–P5 record/time | [Read bodies:717–731](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L717-L731) fill only the first record even with count64; 0/65 reject before sampling. Read ignores nested status. Local monotonic timestamp precedes selector/query; repeated last-processed SDL state can coexist with advancing timestamp and diagnostic reads. No exposed sequence or acquisition receipt exists. |
| P6–P8 identity/lifecycle | [Selector:209–251](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L209-L251) increments uint8 only on successful SDL open, with count written before selection in samples and after selection in Info. Counter255 replacement wraps0, masked to1 next time. GUID/name preference and internal instance IDs are not exported; unique fields stay zero. [Close/Open:699–716](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L699-L716) reuse handle1 without SDL close/state reset. Guard/Close accesses do not supply an incarnation lease or concurrency guarantee; stable serial-open is a necessary premise. |
| P9–P11 overlay/synthetic order | Stable true capture at both checks produces neutral controls while retaining connected/time/default motion and clearing mouse accumulation. Two checks are not atomic. [Postprocessing:683–697](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L683-L697) records host state before injection/replay, applies due replay controls, then ORs injected buttons and overrides sticks/triggers/touch. File stat/open failure retains injected state. P11's replay triggers7/8 survive its cross/lx-only injection; record rows omit those later changes. |
| P12 touch/calibration | Actual successful down-finger queries and synthetic Back/key/file clicks can produce equal count/slot-ID fields. [touch_ids:668–682](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L668-L682) overwrites SDL finger IDs with persistent cyclic1..127 occupied-slot IDs and uint32 host-time duration. Calibration's eight quiet samples and timeout/bias predicates are caller samples, not eight acquired reports; selected replacement resets calibration, PadOpen does not. |
| P13–P15 capability | [Info/vibration/helpers:732–764](https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_pad.c#L732-L764) give fixed Info values/connected1 without hardware, identical guard success for flags0/1 and no motion mutation, and return0 for no-pad/SDL-false/SDL-true rumble. Bytes255/1 produce conditional attempted amplitudes65535/257 for1000ms. Only the supplied true API result supports conditional SDL acceptance, never physical effect/completion. |
| P16 selection | Exact mapped NID, native interface, capability mask and non-data selection are distinct premises. Read/motion-state absent names are limited to this import lookup. Body/export presence is not actual guest invocation. F1 corrects only the ambiguous capability predicate. |

PadData/PadTouch/ControllerInfo declarations and static assertions constrain source sizes/selected offsets; they are not compiled ABI receipts. Correct sysv_abi/native interface and full writable output extent remain supplied premises. No output pointer is retained. Return under the valid serial setup closes these source writes, not device ownership, an SDL acquisition or native/game correctness.

## Independent official API and dependency check

Eight primary official SDL3 pages were independently opened/read on 2026-10-13: [PollEvent](https://wiki.libsdl.org/SDL3/SDL_PollEvent), [GetKeyboardState](https://wiki.libsdl.org/SDL3/SDL_GetKeyboardState), [GetGamepadID](https://wiki.libsdl.org/SDL3/SDL_GetGamepadID), [GetGamepads](https://wiki.libsdl.org/SDL3/SDL_GetGamepads), [GetGamepadAxis](https://wiki.libsdl.org/SDL3/SDL_GetGamepadAxis), [GamepadConnected](https://wiki.libsdl.org/SDL3/SDL_GamepadConnected), [GetGamepadTouchpadFinger](https://wiki.libsdl.org/SDL3/SDL_GetGamepadTouchpadFinger), and [RumbleGamepad](https://wiki.libsdl.org/SDL3/SDL_RumbleGamepad).

PollEvent can pump implicitly and documents video-initializing/main-thread requirements. Keyboard state is an internal array updated by pumping; intervening press/release can be absent. Selected gamepad APIs permit any-thread calls; instance/query/failure fields support the dossier's distinctions. Finger query success/down and normalized coordinates differ from output slot identity. Rumble bool and event-processing/UpdateJoysticks requirement support the conditional acceptance/update limit. The selected window thread constructs VIDEO|GAMEPAD then polls; pad sampling does not itself pump/update. Actual caller eligibility, event ordering and cross-device snapshot consistency remain UNKNOWN.

These mutable CC BY4.0 API descriptions have no bound revision or linked artifact; availability since3.2.0 is not installed-version proof. Ambient pkg-config SDL flags and ambient nixpkgs do not bind a version. README GPL v2-or-later declaration, GPL v2 LICENSE text and VENDOR lineage match the bounded registry statement. No per-file/dependency license-combination judgment or independent-fork corroboration is added.

## Cumulative integration checks

Exact integration-only bases independently matched:

- Accepted main `287353e1b1d8392e13c019837cfd349e27d9b4bd`, tree `1c3076314bad8edeb1340c3bdef85659ce8b1c31`.
- Peer memory PR17 `2b4ae7b0a45fb1af7e0a220156ca1c874c46a5cb`, tree `a2c1533d6395eee3e6c2f3ca1e02245941bffefb`.
- Peer audio PR18 `80e518a2a6f9acb5da56c78112833b37c74356f3`, tree `d615f6448e04e97addf43b29250aaefc15221f59`.

Main→memory→audio→pad ancestry holds. All109 of115 main paths,118 of124 memory paths and125 of131 audio paths outside the six shared routing/registry/log surfaces preserve exact Git blobs and modes. This includes every accepted technical and frozen record, every memory/audio technical file and their frozen reports. Seven accepted README route rows match main exactly. START_HERE/llms/source-log/checkpoint prefixes preserve all three bases. Five pad append surfaces retain the audio baseline prefixes. Removing only pad's registry block restores the whole audio registry; removing the cumulative memory/audio/pad extensions restores the main registry. Pad's fifteen-path/eight-URL list is grouped under bbport before shadps4; prior pins/licenses/fields are unchanged. No YAML parser validation or installation is claimed.

RC-0020 through RC-0025 each has exactly one claim path. All three Batch02 routes remain proposals; memory/audio are peer-reviewed unmerged topics, not eighth/ninth accepted topics or pad corroboration. Both linked usability NOT MET records and Issue9 OPEN remain. Append history preserves earlier pending statuses with subsequent dated delivery dispositions. Candidate eleven-file delta is six shared modifications plus five new pad documents; all are text. Scoped whitespace check passed; an independent relative-path check found351 occurrences with no missing targets. Existing anchor/range inventories are reused, not semantic proof.

Unchanged memory source semantics were reused from review r1 plus affected recheck r2, and audio from review r1; no repeated memory/audio source audit. Their incorporated SHA-256s independently match: memory r1 `6a8ed515a477c7397241b75acac331700f1d02e6c728d5a2e21b6d2af08ac149`, memory r2 `334f43bc5d50020e5f65d72726ffee3354931f7d6e30ccd931b854c2b1928063`, audio r1 `8e674653a19f24c10483193c563e51dba44f6a3b722d395db23af1eb08a8391f`. Their original scope, resolved findings and preserved failed usability evidence remain distinct from this cumulative integration check.

## Handoff, limits and closure

Return F1 through the parent for supported activation of the completed original author, followed by this same reviewer's affected recheck of frozen r2+. Parent retains acceptance/integration/publication; human editorial consolidation/merge remain pending. The correction clarifies an existing raw-mask contract, adding no authority or target claim. No fourth topic, broad heap/SDL/UI/renderer campaign or new reader is selected.

Missing actual caller/library/compiler evidence, SDL acquisition freshness, physical identity/features, sensor/rumble effect/completion, concurrent lifetime/snapshot behavior, original-controller fidelity and Linux/native/game ABI validity are disclosed limits, not additional defects demanding new tests. Source/model reasoning, serialized execution, native fixture and game evidence remain separate; only the first exists here.

Candidate/canonical/source state stayed unchanged. No upstream execution/build/script, source import, runtime/controller/device/UI/game launch/input, installation, framework, reader, child/model shopping, external communication/publication or push occurred. All commands completed; no live process/session handle, runtime resource, child or writer claim remains. The sole authored artifact is this scratch review. Served-model identity, token/cost usage and elapsed-time telemetry are unavailable/UNKNOWN; no timed experiment occurred. Freeze this report before delivery; corrections use a linked successor.
