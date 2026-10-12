# RC-0002 — bbhost documents original-code differential testing

**Level:** PROJECT_REPORTED + SOURCE_INSPECTED header, 2026-10-12. **Independently reproduced here:** NO.

At bbhost commit `566184a74f071166299bb656c4af479e5bbe2771`, `docs/decomp.md` describes running original machine code alongside rewritten functions on generated inputs and comparing behavior during game sessions. `tests/decomp/eboot_kit.h` declares a helper for mapping the user's game executable and configuring guest TLS/floating-point state, with missing/incorrect executable skipped via an explicit code.

**Sources:** [method](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/docs/decomp.md); [helper interface](https://github.com/droogie/bbhost/blob/566184a74f071166299bb656c4af479e5bbe2771/tests/decomp/eboot_kit.h).

**Important limits:** 'Without the game' can still mean *executing user-provided game code* in a fixture. Mocks shared by both versions can conceal missing behavior; same_float accepts NaNs regardless of payload. Neither a source comment nor a CI skip is a game proof. Do not execute proprietary code without actual authorization.

**Next testable question:** For one eligible pure game function, specify matched inputs, state isolation, falsifying wrong-output case and the exact equality rule before reusing a differential runner.
