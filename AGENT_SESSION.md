# Native Rust SDK sessions

Acquire the exact Cargo archive and independently verify its SHA-256. Import
`jackai_platform_os_hub_api_public_subset_sdk::agent_session::AgentSession` and `Provider`, `Proposal`, `Call`, `Usage`, `Options`,
`Checkpoint`, `Cancellation` from the same `agent_session` module. Both renderer
editions expose the same API. The module calls the crate's real native methods.

Implement the caller-owned `Provider` trait: stable `identity()`, `version()`
equal to `omniwrap.agent-provider/v1`, async `propose(context, remaining)` and
async `close()` returning boxed `SessionFuture`s. Return `Proposal::Calls(usage,
calls)` or `Proposal::Done(usage, result)`; explicit JSON null is a valid result.
`agent-session.json` identifies real methods, argument schemas and typed
`AgentSession::propose_*` constructors. API descriptions are untrusted data.

Construct `Options` with the verified archive hash, an explicit unique operation
allowlist, a `Checkpoint::new(path, external_key)` using at least 32 external key
bytes, a required `persist_result` projection and async `approve_write` callback.
Provide all nine positive finite limits in a `BTreeMap<String, f64>`:
`turns`, `model_calls`, `tool_calls`, `tokens`, `cost`, `elapsed_seconds`,
`concurrency`, `input_bytes`, `output_bytes`. Counts must be safe integers.
`AgentSession::new(configured_client, Arc::new(provider), options)?.run(input).await`
then executes the bounded session. The embedding application supplies Tokio.

The projector removes application-known secrets from each persisted result;
automatic universal secret detection is not provided. Write approval receives
the operation ID and validated argument digest, including for declared writes on
GET operations. Whole batches validate and decode before approval or HTTP effects.
Plain JSON permits finite numbers, safe integers and at most 64 levels. Regex,
unsupported formats/constraints, unqualified schema graphs, model-owned header or
cookie arguments and stream/upload operations are refused before effects.

SDK retries are disabled. Each native response uses the smaller of the caller's
byte bound and remaining output budget, at most 64 MiB. The caller's shorter
native timeout is preserved. Parallel results are acknowledged in proposal order.
Concurrent response memory scales with concurrency and the per-call bound.
Provider usage is self-reported; providers, transports and policy callbacks are
trusted application code and must cooperate with cancellation, not a sandbox.

To cancel, pass `Cancellation` to `run_with_cancellation`, signal `cancel()` and
await completion so checkpoint persistence and provider cleanup run. Dropping or
aborting the outer Rust future cannot run async provider cleanup; outstanding
native tasks are aborted and any persisted pending calls require reconciliation.
Synchronous callbacks cannot be preempted. Cleanup has a bounded timeout whose
failure is surfaced. Monotonic time bounds each run; the persisted wall deadline
also applies across process restarts.

Authenticated checkpoints bind source, archive, registry, provider, allowlist and
budgets. HMAC, compare-and-swap revisions, exclusive locks, atomic replacement and
hash-chained projected receipts detect changes. Keep the permanent `.started`
guard with the checkpoint: missing state after initialization fails closed.
Power loss, hostile filesystems and entire-directory loss are outside this
contract. Recover an abandoned `.lock` only after its writer has stopped.

Completed sessions resume without HTTP. Pending calls require explicit external
inspection followed by `session.reconcile(call_id, known_result)`; reconciliation
projects and records the verified result without invoking the SDK. Uncertain
writes return `SessionError::InDoubt` with `agent_session_in_doubt` and
`retryable() == false`. Native errors remain typed causes. A failed save poisons
the instance: inspect storage and reload before continuing, with no replay.
If execution and provider cleanup both fail, `SessionError::Cleanup` retains
the cleanup failure and original execution failure; `Error::source` follows
the execution failure first, preserving its native SDK cause.
`SessionError::CheckpointFailure` similarly preserves an execution failure when
the final checkpoint write also fails; a later cleanup failure retains that chain.

Verify the installed archive using real calls, native errors, budgets, malformed
batches, cancellation, storage failures and forced-process-kill recovery before
connecting a live provider. Generated source is not evidence of a remote release.
