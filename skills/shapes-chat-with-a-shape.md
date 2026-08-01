---
name: Chat with a Shape
description: Send a message to a named Shape (social AI character) and get its reply using the OpenAI-compatible Shapes API.
api: shapes
operations:
  - createChatCompletion
---

# Chat with a Shape

Run a Shape as the model on the OpenAI-compatible Shapes API.

> Note: the Shapes developer API was deprecated 2025-09-25. Shapes remain available as a consumer product at https://shapes.inc.

## Prerequisites

- A Shapes API key from https://shapes.inc/developer, sent as `Authorization: Bearer <API-key>`.
- The target Shape's username, addressed as the model `shapesinc/<shape-username>`.

## Steps

1. Choose the Shape and build the model string `shapesinc/<shape-username>`.
2. Call `createChatCompletion` (`POST /v1/chat/completions`) with a `messages` array. Content may be a
   plain string or content parts including one `image_url` **or** one `audio_url` (not both).
3. For user-facing apps, set `X-User-Id` (per-user memory isolation) and, when needed, `X-Channel-Id`
   (per-conversation context) headers.
4. Read the reply from `choices[0].message.content` in the standard OpenAI-compatible response.

## Rules & conventions

- No system messages, no streaming, no client-side temperature/parameter control — personality and
  settings come from the Shape's shapes.inc configuration (see `conventions/shapes-conventions.yml`).
- Default rate limit is 20 requests/minute.
- Premium-engine Shapes consume credits when accessed via the API.

## Example

```bash
curl -X POST https://api.shapes.inc/v1/chat/completions \
  -H "Authorization: Bearer $SHAPESINC_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"shapesinc/tenshi","messages":[{"role":"user","content":"Hello"}]}'
```
