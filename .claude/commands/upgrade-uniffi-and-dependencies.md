---
name: upgrade-uniffi-and-dependencies
description: Workflow command scaffold for upgrade-uniffi-and-dependencies in uniffi-bindgen-go.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /upgrade-uniffi-and-dependencies

Use this workflow when working on **upgrade-uniffi-and-dependencies** in `uniffi-bindgen-go`.

## Goal

Upgrade the uniffi dependency and related Rust crates, adapt code and templates to new APIs, and update release metadata.

## Common Files

- `Cargo.toml`
- `bindgen/Cargo.toml`
- `fixtures/Cargo.toml`
- `Cargo.lock`
- `bindgen/src/gen_go/*.rs`
- `bindgen/templates/*.go`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update version numbers in Cargo.toml and bindgen/Cargo.toml (and sometimes fixtures/Cargo.toml).
- Update Cargo.lock.
- Adapt Rust source files in bindgen/src/gen_go/ (multiple .rs files) to new uniffi APIs.
- Update Go template files in bindgen/templates/ to match new FFI conventions.
- Update or add tests in binding_tests/ and fixtures/ as needed.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.