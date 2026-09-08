# Claude API Postman Playground

A Postman collection covering 5 different Claude API calls, each testing a distinct capability of the /v1/messages endpoint.

## How to use
Import `claude-api-playground.postman_collection.json` into Postman (File → Import). Set a `model` collection variable (e.g. `claude-sonnet-4-5`) and your API key, then run any request.

## Requests

### 1 — Basic Call
Tests a minimal, no-frills request — no system prompt, no examples, no tools, no formatting constraints. Confirms basic authentication and endpoint connectivity work correctly.
**Expected response:** A JSON body with a `content` array containing one `text` block (a short haiku), and `stop_reason: "end_turn"`.

### 2 — System Prompt
Tests the `system` parameter — sets a persistent behavioral/tone instruction that applies across the whole conversation, separate from the user's actual question.
**Expected response:** A bullet-point list of 5 Postman benefits, written in a more formal/consultant tone than the equivalent request without a system prompt.

### 3 — Few-Shot Example
Tests few-shot prompting — the request includes example user/assistant message pairs before the final query, steering the model's output format and behavior without an explicit written instruction.
**Expected response:** A single-word sentiment classification (e.g. "Neutral") matching the pattern established by the prior examples, with no extra explanation.

### 4 — JSON Output
Tests structured JSON output — the prompt explicitly instructs the model to return only valid JSON with specific keys (`name`, `age`, `city`).
**Expected response:** A clean JSON object, e.g. `{"name": "John", "age": 29, "city": "Austin"}`, with no surrounding prose. Note: the model may occasionally wrap it in a sentence or code fence without a strict JSON schema.

### 5 — Streaming Response
Tests the `stream: true` parameter — the response is returned incrementally as server-sent events (SSE) instead of a single JSON blob.
**Expected response:** A sequence of `data: {...}` events, including multiple `content_block_delta` chunks, ending in a `message_stop` event.
