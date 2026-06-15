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
timeline rather than only a wish list.

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

## Milestone v1.2: ergonomics and reporting

The theme of this milestone is making everyday tests easier to write and easier
to read in CI.

1. [ ] **Latency assertions** with `expectResponseTime(maxMs)` so a test can
   fail when an endpoint gets slow, not only when it is wrong.
2. [ ] **Multipart and file upload helpers** for testing endpoints that accept
   `multipart/form-data`.
3. [ ] **Parallel requests** with a `go.all` style helper and a concurrency
   limit, for fan out checks without hand rolled `Promise.all`.
4. [ ] **Richer failure diffs** that point at the exact JSON path that did not
   match, with the expected and actual values side by side.
5. [ ] **JUnit XML reporter** so results show up natively in CI dashboards.
6. [ ] **Custom matcher API** so teams can register project specific assertions
   once and reuse them across suites.

## Milestone v1.3: protocols and data

This milestone widens what two-go can test beyond plain JSON over HTTP.

7. [ ] **Streaming and Server Sent Events assertions** for endpoints that send
   chunked or `text/event-stream` responses.
8. [ ] **WebSocket testing** for connect, send, and receive flows.
9. [ ] **GraphQL variables and error path checks** so query inputs and the
   `errors` array are first class, not raw body lookups.
10. [ ] **Data driven cases** that read inputs from a JSON or CSV fixture and run
    the same assertions across every row.
11. [ ] **Response time budget per session** so a whole flow can assert a total
    latency ceiling, not only single requests.

## Milestone v2.0: types and stability

This milestone is the line where the public API is locked in and typed.

12. [ ] **First class TypeScript types** shipped as `.d.ts`, with the chain fully
    typed end to end.
13. [ ] **Type tests with `tsd`** so the published types are verified in CI and
    cannot silently regress.
14. [ ] **Stable plugin interface** for matchers, reporters, and importers, with
    a documented contract and a deprecation policy.
15. [ ] **OpenAPI 3.1 and JSON Schema 2020-12** support in the importer and the
    schema validators.

## Reporting and observability

These can ship across milestones. They make test runs easier to read and trace.

16. [ ] **HTML report** with a request and response timeline per test.
17. [ ] **OpenTelemetry export** so each request can emit a span and join an
    existing trace during integration runs.
18. [ ] **Coverage of assertions report** that shows which endpoints and which
    status codes a suite actually exercised.

## Ecosystem

Work that lives in the sibling repositories rather than the core library.

19. [ ] **create-two-go** gains a TypeScript template and a monorepo template in
    addition to the current starter.
20. [ ] **two-go-action** adds a Node version matrix, dependency caching, and
    automatic upload of the JUnit and HTML reports as artifacts.
21. [ ] **two-go-vscode** adds a CodeLens to run a single test from the editor
    and shows the result inline.
22. [ ] **two-go-docs** publishes a searchable API reference generated from the
    source so it never drifts from the code.
23. [ ] **two-go-claude** adds a debugging subagent and documents how to drive
    two-go through its MCP server from an agent.

## Engineering health

Internal work that keeps the project trustworthy.

24. [ ] **CI matrix** across active Node LTS versions and Linux, macOS, and
    Windows.
25. [ ] **Benchmark suite** with a regression guard so performance does not slip
    release to release.
26. [ ] **Mutation testing** on the assertion core to confirm the tests really
    catch broken logic.

## How to propose a change

Open an issue describing the problem first, not only the solution. Explain the
testing pain it removes. If it fits an existing milestone, say which one. Small,
focused proposals move faster than large ones.
