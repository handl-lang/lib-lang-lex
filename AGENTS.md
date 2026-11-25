# lib-lang-lex

`handl-plugin-lib-lang-lex` — the `lex` meta function as a composable
`plugin-lib-*` leaf crate.

## Layout

| path | role |
| --- | --- |
| `handl-packages/lang_lex/lang_lex.hnl` | the .hnl surface |
| `src/lib.rs`, `src/tests.rs` | the Rust crate |
| `pkg.hnl` | package manifest |
| `scripts/hnl-gate.sh` | shared hnl typecheck/lint/test gate |
| `ci.sh` | bupha entry → hnl-gate.sh |

## Contract

- One callable: `lex.lex(lang, text)` — extracts the
  `handl_language::Language`, builds a sub-runtime via
  `RuntimeFactory`, lexes `text` into tokens, returns JSON-serialized
  `handl_language::Tokens`.
- Leaf crate: `handl-runtime`/`handl-language`/`handl-platform`/
  `handl-plugin-module` only — no engine impl crates, no `handl-kit-*`.
- Same `Rc<dyn RuntimeFactory>` wiring caveat as the other `lang-*`
  meta crates (not `Send + Sync`; see `src/lib.rs`).
- Sibling-repo deps are git deps (`branch = "main"`); `[patch]` tables
  resolve them from sibling checkouts.

## Verification

```bash
cargo test    # the Rust suite
bash ci.sh    # the bupha gate — delegates to scripts/hnl-gate.sh
```

## License

MIT.

<!-- myco:agent-awareness -->

## Agent awareness

- Session start / any work discussion: run `myco status --prompt`
  before proposing next steps — know the board first.
- User describes new work → offer to capture it (`myco todo add`,
  `issue new`, `proposal new`). Don't wait to be asked.
- Picking up a task: `myco resume <ID>` is the briefing.
- Wrapping up: `myco handoff <ID>` anything resumable; keep statuses
  honest (claimed → in-progress → blocked/done).

<!-- /myco:agent-awareness -->
