# two-go roadmap

This is the public roadmap for the two-go testing ecosystem. It lists what is
planned, in progress, and shipped across the core library and the surrounding
tools. Items are grouped by release milestone and by area so it is clear what
belongs together and why.

Nothing here is a hard promise on dates. Order can change based on feedback and
real usage. If you want to push an item up, open an issue and make the case.

Status legend:

- [ ] planned, not started yet
- [~] in progress
- [x] shipped

## Shipped

These are done and released. They are kept here so the roadmap reads as a single
timeline rather than only a wish list. The current release is **v2.0.0**.

- [x] **Fluent request chain** with `go()`, verb helpers, headers, and `bearer`.
- [x] **Core expectations** for status, headers, and JSON body paths.
- [x] **Sessions with `extract`** so a token from one response flows into later
  requests through `{{token}}` placeholders.
- [x] **Polling with `eventually` and `pollUntil`** for eventually consistent
  endpoints instead of fixed sleeps.
- [x] **Snapshot testing** through `toMatchSnapshot`.
- [x] **Schema tooling** with `inferSchema`, `toSchema`, and `expectJsonSchema`,
  including real validation and rejection of `NaN`.
- [x] **Fake data** helpers for generating request payloads.
- [x] **Importers** from OpenAPI and Postman with `fromOpenapi` and
  `fromPostman`.
- [x] **GraphQL helper** for query and mutation requests.
- [x] **Request retry with backoff** for flaky upstreams.
- [x] **Cookie jar** so session cookies carry across requests.
- [x] **Latency assertion** with `expectTimeBelow(ms)`.
- [x] **Parallel requests** with `parallel`, `parallelLimit`, and `mapLimit`.
- [x] **JUnit and JSON reporters** through `toJUnit` / `toJSON` and the CLI
  `--reporter junit|json` flag.
- [x] **BDD layer** in `two-go/bdd` with `Given`, `When`, `Then`, and `And`.
- [x] **TypeScript declarations** shipped as `.d.ts` for every module, checked
  against the runtime exports in CI without a TypeScript dependency (v2.0.0).
- [x] **AI layer and MCP server** for test generation, failure explanation,
  review, fuzzing, and agent-driven runs.

## Milestone v2.1: ergonomics and reporting

The theme of this milestone is making everyday tests easier to write and easier
to read in CI.

1. [ ] **Multipart and file upload helpers** for testing endpoints that accept
   `multipart/form-data`.
2. [ ] **Richer failure diffs** that point at the exact JSON path that did not
   match, with the expected and actual values side by side.
3. [ ] **Custom matcher API** so teams can register project specific assertions
   once and reuse them across suites.

## Milestone v2.2: protocols and data

This milestone widens what two-go can test beyond plain JSON over HTTP.

4. [ ] **Streaming and Server Sent Events assertions** for endpoints that send
   chunked or `text/event-stream` responses.
5. [ ] **WebSocket testing** for connect, send, and receive flows.
6. [ ] **GraphQL variables and error path checks** so query inputs and the
   `errors` array are first class, not raw body lookups.
7. [ ] **Data driven cases** that read inputs from a JSON or CSV fixture and run
   the same assertions across every row.
8. [ ] **Response time budget per session** so a whole flow can assert a total
   latency ceiling, not only single requests.

## Milestone v3.0: stability

This milestone is the line where the public API is locked in.

9. [ ] **Signature-level type checks** that verify parameter and return types of
   the `.d.ts` files, still without adding a dependency to the package.
10. [ ] **Stable plugin interface** for matchers, reporters, and importers, with
    a documented contract and a deprecation policy.
11. [ ] **OpenAPI 3.1 and JSON Schema 2020-12** support in the importer and the
    schema validators.

## Reporting and observability

These can ship across milestones. They make test runs easier to read and trace.

12. [ ] **HTML report** with a request and response timeline per test.
13. [ ] **OpenTelemetry export** so each request can emit a span and join an
    existing trace during integration runs.
14. [ ] **Coverage of assertions report** that shows which endpoints and which
    status codes a suite actually exercised.

## Ecosystem

Work that lives in the sibling repositories rather than the core library.

15. [ ] **create-two-go** gains a TypeScript template and a monorepo template in
    addition to the current starter.
16. [ ] **two-go-action** adds a Node version matrix, dependency caching, and
    automatic upload of the JUnit and HTML reports as artifacts.
17. [ ] **two-go-vscode** adds a CodeLens to run a single test from the editor
    and shows the result inline.
18. [ ] **two-go-docs** publishes a searchable API reference generated from the
    source so it never drifts from the code.
19. [ ] **two-go-claude** adds a debugging subagent and documents how to drive
    two-go through its MCP server from an agent.

## Engineering health

Internal work that keeps the project trustworthy.

20. [~] **CI matrix** across active Node LTS versions (18, 20, 22 on Linux today)
    and macOS and Windows.
21. [ ] **Benchmark suite** with a regression guard so performance does not slip
    release to release.
22. [ ] **Mutation testing** on the assertion core to confirm the tests really
    catch broken logic.

## How to propose a change

Open an issue describing the problem first, not only the solution. Explain the
testing pain it removes. If it fits an existing milestone, say which one. Small,
focused proposals move faster than large ones.
