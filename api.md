# JackAI Platform OS Hub API (public subset) Rust API

<!-- omniwrap-api-reference eyJjb250cmFjdF9maW5nZXJwcmludCI6ImM3Y2E1ZTVlYmI0YzA5MjkxMGVjNzJiMzcxZTE4ODMwMzM1OGM1ZTM0ZDI5MDhjMGE4OGY3ODJhMjQxMTYyY2YiLCJvcGVyYXRpb25fY291bnQiOjgsInJlbmRlcmVyIjoicnVzdCIsInZlcnNpb24iOiIxLjUuMCJ9 -->

This generated index is tied to Semantic IR `1.14.0` and contract fingerprint `c7ca5e5ebb4c092910ec72b371e188303358c5e34d2908c0a88f782a241162cf`. Every operation below is rendered from the same semantic contract and artifact-attested public member allocation as the SDK.

SDK maturity: **experimental**  
Artifact evidence: [`omniwrap-artifact.json`](omniwrap-artifact.json) binds this file by SHA-256 and is revalidated by the package gate.

## Client hooks and tracing

`ClientBuilder::hooks(RequestHooks::new()...)` registers four callbacks. Every attempt starts with `before_request` and ends with exactly one of `on_retry` (another attempt follows), `after_response` (the success the call returns) or `on_error` (the failure the call reports). Each receives the operation id, the HTTP method, the URL, the request headers, the attempt number (from 1), the time elapsed since the call started and, once the server answered, the HTTP status. No context carries a credential: `Authorization`, `Proxy-Authorization`, `Cookie`, every API-key header and API-key query parameter, and any configured credential value read `[redacted]`. Every hook borrows an immutable `HookContext`: no hook can change the request.

`ClientBuilder::tracer(...)` opens one span per call through the tracer interface this SDK defines, named after the operation id, with `http.request.method`, `http.response.status_code` and `http.request.resend_count`. It needs no tracing library; README.md maps it onto the OpenTelemetry API.

## Resource `health()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJoZWFsdGgoKS5nZXQiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJnZXRIZWFsdGgiLCJwYXRoIjoiL2hlYWx0aCIsInJlc291cmNlIjoiaGVhbHRoKCkiLCJzZWN0aW9uX3NoYTI1NiI6IjcwMDk4MjhlZTQ3NmMzMjkwMThmYWRhMmIxNjIwY2U1MjM3OTU3ZGZkZmQ3MGI2MTU5N2RmNDY1MWMzMTY1NzAiLCJzaWduYXR1cmVfc2hhMjU2IjoiNzc0YWYyMTE2MzVjNzQ1MDc5ZDg0ZGY1NTNiMjMxMzg2YWVlYmFiN2M0OWMxOWMwMTIwYmZkYzk2MjBlOTc4OCJ9 -->
### `client.health().get`

Operation ID: `getHealth`  
Route: `GET` `/health`  
Equivalent member: `client.get_health`  

#### Signature

```rust
pub async fn get(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Hub liveness status | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.health().get().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRIZWFsdGgifQ -->

## Resource `kernel()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJrZXJuZWwoKS5mYWlsX3VzYWdlX3F1b3RhIiwibWV0aG9kIjoiUE9TVCIsIm9wZXJhdGlvbl9pZCI6ImZhaWxVc2FnZVF1b3RhIiwicGF0aCI6Ii92MS9rZXJuZWwvdXNhZ2UvZmFpbCIsInJlc291cmNlIjoia2VybmVsKCkiLCJzZWN0aW9uX3NoYTI1NiI6ImU4MGY3ZTAzMWI0N2E1NGViZWI2YzhjZTJkYTVkZmQxYWFjNjMzYTVlOTA1MWQ0NGFjY2UwY2IxYWIwMDAwNmEiLCJzaWduYXR1cmVfc2hhMjU2IjoiNDI5OWM5NDljZjYwYjA5MTk1NTI2YTllOTgzNGJkNTVhZTk5YWFhOWM1MzQ0OGYxNzNiMTVkYjQzYjBlOTEwNiJ9 -->
### `client.kernel().fail_usage_quota`

Operation ID: `failUsageQuota`  
Route: `POST` `/v1/kernel/usage/fail`  
Equivalent member: `client.fail_usage_quota`  

#### Signature

```rust
pub async fn fail_usage_quota(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Reservation released | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.kernel().fail_usage_quota().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJmYWlsVXNhZ2VRdW90YSJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJrZXJuZWwoKS5maW5hbGl6ZV91c2FnZV9xdW90YSIsIm1ldGhvZCI6IlBPU1QiLCJvcGVyYXRpb25faWQiOiJmaW5hbGl6ZVVzYWdlUXVvdGEiLCJwYXRoIjoiL3YxL2tlcm5lbC91c2FnZS9maW5hbGl6ZSIsInJlc291cmNlIjoia2VybmVsKCkiLCJzZWN0aW9uX3NoYTI1NiI6IjJiZWI2YzM3Y2MzNTg0ZmRjNTJkYmVhYjU4MjE4YTg0OGM1NDIwMzY3ODVjZGQ4NDE3M2QyZTc1MTFjZDM2YWIiLCJzaWduYXR1cmVfc2hhMjU2IjoiOGNjOTVhZWY4NzU1M2YxMDA5YWI5Y2JkMzdhN2NhNWUzYTc5MDNmYWMzOTA4MWQ4YTIxZDU2NGQ4NjJmNGM2ZCJ9 -->
### `client.kernel().finalize_usage_quota`

Operation ID: `finalizeUsageQuota`  
Route: `POST` `/v1/kernel/usage/finalize`  
Equivalent member: `client.finalize_usage_quota`  

#### Signature

```rust
pub async fn finalize_usage_quota(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Reservation finalized | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.kernel().finalize_usage_quota().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJmaW5hbGl6ZVVzYWdlUXVvdGEifQ -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJrZXJuZWwoKS5yZXNlcnZlX3VzYWdlX3F1b3RhIiwibWV0aG9kIjoiUE9TVCIsIm9wZXJhdGlvbl9pZCI6InJlc2VydmVVc2FnZVF1b3RhIiwicGF0aCI6Ii92MS9rZXJuZWwvdXNhZ2UvcmVzZXJ2ZSIsInJlc291cmNlIjoia2VybmVsKCkiLCJzZWN0aW9uX3NoYTI1NiI6IjU2ZjAxZDA1NmRiYzdjMGU4MGM2MGMxMDRhNDU4MDZmNzZmNzA1MDIxZjhiYjljN2Q2ZjljMTE2MGM3YTM4YjciLCJzaWduYXR1cmVfc2hhMjU2IjoiOTMyZjE3ZTZkNTMyMDZmZTI3NGQ2NTgyYjhiY2FjZTJkMGY1YjBiMDk2Yzk4YmQ3NTBiNzQ2ZmE5YTdmNjBkMyJ9 -->
### `client.kernel().reserve_usage_quota`

Operation ID: `reserveUsageQuota`  
Route: `POST` `/v1/kernel/usage/reserve`  
Equivalent member: `client.reserve_usage_quota`  

#### Signature

```rust
pub async fn reserve_usage_quota(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Reservation lease created | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.kernel().reserve_usage_quota().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJyZXNlcnZlVXNhZ2VRdW90YSJ9 -->

## Resource `user()`

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJ1c2VyKCkuZ2V0X2N1cnJlbnQiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJnZXRDdXJyZW50VXNlciIsInBhdGgiOiIvdXNlci9tZSIsInJlc291cmNlIjoidXNlcigpIiwic2VjdGlvbl9zaGEyNTYiOiIxMDM3YWY2MzJlZjc1NDc3YzUyYmIxOWQ3NjNkMDNlN2JmOWFiOWRkYTYzMTY0ZjEyNTA3NTBkMWM5NmY3ZTBmIiwic2lnbmF0dXJlX3NoYTI1NiI6ImJmYmU4NzdhMzU0MGY3NmYwNmJlNDdiNTMxYTM0MDdhYWIyZmI3Mzc2ZDg1YmMwMmFjZjQ2Y2FmNWExZjI0YzgifQ -->
### `client.user().get_current`

Operation ID: `getCurrentUser`  
Route: `GET` `/user/me`  
Equivalent member: `client.get_current_user`  

#### Signature

```rust
pub async fn get_current(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Current user context | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.user().get_current().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRDdXJyZW50VXNlciJ9 -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJ1c2VyKCkuZ2V0X3NpZ251cF9wb2xpY3kiLCJtZXRob2QiOiJHRVQiLCJvcGVyYXRpb25faWQiOiJnZXRTaWdudXBQb2xpY3kiLCJwYXRoIjoiL3VzZXIvYXV0aC9zaWdudXAtcG9saWN5IiwicmVzb3VyY2UiOiJ1c2VyKCkiLCJzZWN0aW9uX3NoYTI1NiI6IjEyNzM2Njk2MmNlNTUxY2VjOTBhOGQzZjMzNjFmMWE3M2M5YjNlNjU0YzdkODgzMjQwMjJjNTUxNjM4YjI1ZWUiLCJzaWduYXR1cmVfc2hhMjU2IjoiYzJlMjNjZWVhMDgzNTRlNWVkYTNmZjk3YjE3ZmYxMDRhYTViNTI4MDk2NWU1Nzg1N2ZhYTE4OWExODY4OTA2NyJ9 -->
### `client.user().get_signup_policy`

Operation ID: `getSignupPolicy`  
Route: `GET` `/user/auth/signup-policy`  
Equivalent member: `client.get_signup_policy`  

#### Signature

```rust
pub async fn get_signup_policy(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Current signup policy | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.user().get_signup_policy().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJnZXRTaWdudXBQb2xpY3kifQ -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJ1c2VyKCkubG9naW4iLCJtZXRob2QiOiJQT1NUIiwib3BlcmF0aW9uX2lkIjoibG9naW5Vc2VyIiwicGF0aCI6Ii91c2VyL2F1dGgvbG9naW4iLCJyZXNvdXJjZSI6InVzZXIoKSIsInNlY3Rpb25fc2hhMjU2IjoiM2I1ZGQ0OTVmYWUxYjY0NzAzOWQ5MThmYmM1ZTg0MzdkYjFkZmViNzcwOTcxOThjOWY2YjkwNGY1MWVhNzg1MSIsInNpZ25hdHVyZV9zaGEyNTYiOiI3NzAzMzM4MzFmZjA2MGUwYjVkYjdhMWU4ODdjZDY2ZDA5M2ExM2Y4MzQyNjNiZjc0NTdiMjI4NTAzMjY3ZGI5In0 -->
### `client.user().login`

Operation ID: `loginUser`  
Route: `POST` `/user/auth/login`  
Equivalent member: `client.login_user`  

#### Signature

```rust
pub async fn login(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `200` | Authenticated session or MFA challenge | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.user().login().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJsb2dpblVzZXIifQ -->

<!-- omniwrap-api-operation eyJleGFtcGxlX3JlYXNvbiI6bnVsbCwiZXhhbXBsZV9zdGF0dXMiOiJnZW5lcmF0ZWQiLCJtZW1iZXIiOiJ1c2VyKCkuc3VibWl0X3dhaXRsaXN0X3JlcXVlc3QiLCJtZXRob2QiOiJQT1NUIiwib3BlcmF0aW9uX2lkIjoic3VibWl0V2FpdGxpc3RSZXF1ZXN0IiwicGF0aCI6Ii91c2VyL2F1dGgvd2FpdGxpc3QiLCJyZXNvdXJjZSI6InVzZXIoKSIsInNlY3Rpb25fc2hhMjU2IjoiNjdhOWUwNDFhMWY0NDU0NzU3ZGEwYTdmMjljYTNlOGVmNDJkNzZmZjVlNWU4MWVkZTc4ZjVjMWY0ZTdmNGU4MCIsInNpZ25hdHVyZV9zaGEyNTYiOiIzY2YzNDQ5YzRkMWQzMzVkNmRlOTdiZGE2Y2NmN2QxYmQ4ODc1NDI2NDFlN2RjZWZlOGVjNjAzNWNiOTQyZGVlIn0 -->
### `client.user().submit_waitlist_request`

Operation ID: `submitWaitlistRequest`  
Route: `POST` `/user/auth/waitlist`  
Equivalent member: `client.submit_waitlist_request`  

#### Signature

```rust
pub async fn submit_waitlist_request(&self, request_options: Option<RequestOptions>) -> Result<(), ApiError>
```

#### Parameters

| Name | In | Required | Contract type | Description |
| --- | --- | --- | --- | --- |
| _none_ | | | | |

#### Responses

| Status | Description | Content |
| --- | --- | --- |
| `202` | Waitlist request recorded with an opaque WL- reference | none |

#### Canonical required-input example

```json
{
  "parameters": []
}
```

#### SDK call example

Example status: `generated`  
```rust
let result = client.user().submit_waitlist_request().await?;
```

<!-- omniwrap-api-operation-end eyJvcGVyYXRpb25faWQiOiJzdWJtaXRXYWl0bGlzdFJlcXVlc3QifQ -->

