# Read public guidance with curl

This optional manual walkthrough sends five requests to CLE's public, read-only MCP service. It installs nothing and does not configure an agent or test a native client integration. Use generic questions; do not send names, citation numbers, account details or other private case information.

Run each command separately and inspect its response before continuing. Use a curl version that supports `--fail-with-body`. Headers are included so you can check the HTTP status and content type.

## 1. Initialize

```sh
curl --fail-with-body --silent --show-error --max-time 30 --include \
  --request POST 'https://traffic.californialicensingeducation.com/mcp' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json, text/event-stream' \
  --data '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{},"clientInfo":{"name":"cle-public-doc-example","version":"1.0.0"}}}'
```

On November 14, 2026, CLE returned protocol `2025-06-18` and no `Mcp-Session-Id` header. This example targets that stateless endpoint. Check that the returned protocol still matches before continuing; if a session ID is now issued, use a client that handles the updated session flow.

The successful request responses currently use Server-Sent Events (SSE): an `event: message` line followed by a `data:` line containing the JSON-RPC response. Inspect the JSON after `data:`; the entire SSE body is not a JSON document.

## 2. Send the initialized notification

```sh
curl --fail-with-body --silent --show-error --max-time 30 --include \
  --request POST 'https://traffic.californialicensingeducation.com/mcp' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json, text/event-stream' \
  --header 'MCP-Protocol-Version: 2025-06-18' \
  --data '{"jsonrpc":"2.0","method":"notifications/initialized"}'
```

This notification has no request ID. The observed successful response is HTTP `202` with an empty body, so there is no JSON to parse.

## 3. Discover the tools

```sh
curl --fail-with-body --silent --show-error --max-time 30 --include \
  --request POST 'https://traffic.californialicensingeducation.com/mcp' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json, text/event-stream' \
  --header 'MCP-Protocol-Version: 2025-06-18' \
  --data '{"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}'
```

Read `result.tools` and confirm the current input schemas for `search_guidance` and `get_guidance` before using them.

## 4. Search for a topic

```sh
curl --fail-with-body --silent --show-error --max-time 30 --include \
  --request POST 'https://traffic.californialicensingeducation.com/mcp' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json, text/event-stream' \
  --header 'MCP-Protocol-Version: 2025-06-18' \
  --data '{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"search_guidance","arguments":{"query":"traffic school cost","limit":3}}}'
```

Look in `result.structuredContent.data.results` for topic IDs and exact article URLs. The verified response included `course-cost` and `traffic-school-overview`; results may change. Search is a topic lookup, not an answer. Its score is internal relevance, not a Google ranking.

## 5. Read the selected answer and sources

Run this command only if your search returned `course-cost`. Otherwise, choose an ID actually returned by the service and use the verified tool schema.

```sh
curl --fail-with-body --silent --show-error --max-time 30 --include \
  --request POST 'https://traffic.californialicensingeducation.com/mcp' \
  --header 'Content-Type: application/json' \
  --header 'Accept: application/json, text/event-stream' \
  --header 'MCP-Protocol-Version: 2025-06-18' \
  --data '{"jsonrpc":"2.0","id":4,"method":"tools/call","params":{"name":"get_guidance","arguments":{"id":"course-cost"}}}'
```

In `result.structuredContent`, read `data.answer`, `data.sources` and `meta.reviewedAt` together. Open the returned school page for the complete explanation and the cited official sources for current court instructions. Preserve each returned citation URL, including its fragment; a guidance ID is not a URL. `meta.checkedAt` is response assembly time, not a fresh verification of those sources. This example copies no price or eligibility claim from a past response.

## Handle errors and incomplete results

`--fail-with-body` catches HTTP failures, but HTTP `200` can still carry a JSON-RPC `error` or a tool result with `result.isError: true`. Inspect both before using an answer. An unavailable service or empty search is not proof that no guidance exists; empty searches may supply `availableGuidanceIds`. Read the response and use CLE's public-browser fallback when needed rather than inventing an answer or citation.
