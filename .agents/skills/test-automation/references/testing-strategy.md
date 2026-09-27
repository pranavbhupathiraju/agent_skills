# Testing Strategy & Best Practices

## 1. Test Categorization & Runner Defaults

| Ecosystem | Recommended Framework | Test Location | Execution Command |
| :--- | :--- | :--- | :--- |
| **Python** | `pytest` + `unittest.mock` | `tests/test_*.py` | `pytest -v` |
| **TypeScript / JS** | `vitest` or `jest` | `tests/**/*.test.ts` | `npx vitest run` / `npm test` |
| **Go** | Standard `testing` package | `*_test.go` | `go test -v ./...` |
| **Rust** | Built-in `cargo test` | `tests/` or unit in module | `cargo test` |

---

## 2. Test Structure: The AAA Pattern
Every unit and integration test should follow the three-phase structure:
1. **Arrange**: Set up test fixtures, input objects, mock expectations, and environment state.
2. **Act**: Invoke the target function, method, or API endpoint.
3. **Assert**: Validate outputs, side effects, and state mutations against expectations.

---

## 3. High-Priority Edge Cases Checklist
When authoring test suites, systematically verify:
- [ ] **Empty / Zero Inputs**: Empty strings (`""`), empty arrays (`[]`), empty dictionaries/maps (`{}`), zero (`0`), negative values.
- [ ] **Nullability**: `None` / `null` / `undefined` passed to non-nullable or optional parameters.
- [ ] **Type & Format Validation**: Malformed JSON, non-numeric strings where floats/ints expected.
- [ ] **Idempotency**: Executing an operation twice does not duplicate state or corrupt storage.
- [ ] **Network / External Timeouts**: Simulated socket drops, HTTP 500/503 responses, delayed answers.
- [ ] **Concurrency & Race Conditions**: Simultaneous read/write access to shared caches or state.

---

## 4. Mocking Guidelines
- **Mock at the boundary**: Mock the HTTP client (e.g. `requests`, `axios`, `fetch`) or database driver, rather than internal business logic.
- **Avoid over-mocking**: Do not mock utility functions, pure algorithms, or standard library data structures.
- **Reset mocks**: Ensure mocks are cleaned up after each test execution to prevent cross-test contamination.
