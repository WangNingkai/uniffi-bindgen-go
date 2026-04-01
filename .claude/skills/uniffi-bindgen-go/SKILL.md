```markdown
# uniffi-bindgen-go Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development conventions and workflows for contributing to the [`uniffi-bindgen-go`](https://github.com/mozilla/uniffi-bindgen-go) project. This repository enables generating Go bindings for Rust libraries using [UniFFI](https://mozilla.github.io/uniffi-rs/), and involves both Go and Rust code, code generation templates, and a suite of integration tests. You'll learn how to upgrade dependencies, add new features, manage fixtures, and maintain tests, all while following the project's coding standards.

---

## Coding Conventions

### File Naming

- **PascalCase** is used for Go template files and some Rust files.
  - Example: `ObjectTemplate.go`, `VTableImpl.go`, `Helpers.go`
- Test files follow Go's convention: `*_test.go`
  - Example: `object_test.go`

### Import Style

- **Relative imports** are used in Go code.
  - Example:
    ```go
    import "./helpers"
    ```

### Export Style

- **Named exports** are preferred for Go and Rust modules.
  - Example (Go):
    ```go
    func NewObject() *Object { ... }
    ```
  - Example (Rust):
    ```rust
    pub fn generate_go_bindings(...) { ... }
    ```

### Commit Patterns

- Commit messages are freeform, usually concise (~33 characters), and may use prefixes but are not strictly enforced.

---

## Workflows

### Upgrade UniFFI and Dependencies

**Trigger:** When updating to a new version of UniFFI or core dependencies  
**Command:** `/upgrade-uniffi`

1. Update version numbers in `Cargo.toml`, `bindgen/Cargo.toml`, and (if needed) `fixtures/Cargo.toml`.
2. Update `Cargo.lock`.
3. Adapt Rust source files in `bindgen/src/gen_go/` to new UniFFI APIs.
4. Update Go template files in `bindgen/templates/` to match new FFI conventions.
5. Update or add tests in `binding_tests/` and `fixtures/` as needed.
6. Update `README.md` and `CHANGELOG.md` with release notes.
7. Update `rust-toolchain.toml` if the Minimum Supported Rust Version (MSRV) changes.

**Example:**
```toml
# Cargo.toml
[dependencies]
uniffi = "0.25"
```

---

### Release Version Bump

**Trigger:** When preparing a new release  
**Command:** `/bump-version`

1. Update version numbers in `Cargo.toml` and `bindgen/Cargo.toml`.
2. Update `Cargo.lock`.
3. Update `README.md` and `CHANGELOG.md` with the new version and release notes.

**Example:**
```markdown
# CHANGELOG.md
## v0.4.0
- Added support for new FFI feature X
```

---

### Add or Update Fixture

**Trigger:** When adding a new test case or regression test for a specific FFI scenario  
**Command:** `/add-fixture`

1. Add or update a directory under `fixtures/` (e.g., `fixtures/empty_string_and_bytes/`).
2. Edit or add `Cargo.toml`, `build.rs`, `*.udl`, and `src/lib.rs` in the fixture.
3. Update `fixtures/Cargo.toml` to include the new fixture.
4. Add or update corresponding test files in `binding_tests/`.

**Example:**
```toml
# fixtures/empty_string_and_bytes/Cargo.toml
[package]
name = "empty_string_and_bytes"
```

---

### Feature or Bugfix in Bindgen Templates

**Trigger:** When adding new FFI features, fixing bugs in code generation, or adapting templates  
**Command:** `/edit-template`

1. Edit one or more files in `bindgen/templates/` (e.g., `ObjectTemplate.go`, `Helpers.go`).
2. Optionally edit Rust code in `bindgen/src/gen_go/` to support the template changes.
3. Update or add tests in `binding_tests/` and/or `fixtures/`.

**Example:**
```go
// bindgen/templates/ObjectTemplate.go
func (o *Object) NewMethod() error { ... }
```

---

### Add or Update Binding Test

**Trigger:** When ensuring new or fixed FFI features are tested from the Go side  
**Command:** `/add-binding-test`

1. Add or update `*_test.go` files in `binding_tests/`.
2. Optionally update `fixtures/` to provide new Rust-side test cases.
3. Run tests to verify changes.

**Example:**
```go
// binding_tests/object_test.go
func TestObject_NewMethod(t *testing.T) { ... }
```

---

## Testing Patterns

- **Test Framework:** Not explicitly specified; follows Go's standard testing conventions.
- **Test File Pattern:** Files named `*_test.go` in the `binding_tests/` directory.
- **Typical Test Example:**
    ```go
    package binding_tests

    import "testing"

    func TestFeatureX(t *testing.T) {
        result := FeatureX()
        if result != expected {
            t.Errorf("unexpected result: %v", result)
        }
    }
    ```
- **Integration with Fixtures:** Some tests depend on Rust fixtures in the `fixtures/` directory.

---

## Commands

| Command           | Purpose                                                        |
|-------------------|----------------------------------------------------------------|
| /upgrade-uniffi   | Upgrade UniFFI and related dependencies, adapt code/templates  |
| /bump-version     | Bump version numbers and update release metadata               |
| /add-fixture      | Add or update a test fixture for a new FFI scenario           |
| /edit-template    | Implement or fix a feature in Go templates or Rust generator  |
| /add-binding-test | Add or update Go tests for new features or bugfixes           |
```
