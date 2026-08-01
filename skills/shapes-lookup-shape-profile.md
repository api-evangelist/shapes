---
name: Look up a public Shape profile
description: Retrieve a Shape's public profile (name, description, tags, stats, avatar) by username — no authentication required.
api: shapes
operations:
  - getPublicShape
---

# Look up a public Shape profile

Fetch public metadata about any Shape by its username.

## Steps

1. Take the Shape's `username` (e.g. `tenshi`).
2. Call `getPublicShape` (`GET /shapes/public/{username}`) — this endpoint requires **no** authentication.
3. Read fields from the returned `ShapeProfile`, such as `name`, `search_description`, `search_tags_v2`,
   `category`, `character_universe`, `user_count`, `message_count`, `avatar_url`, `example_prompts`, and
   `enabled`.

## Rules & conventions

- Public, unauthenticated, read-only endpoint; standard rate limits apply.
- Returns `404` when the Shape does not exist.
- See the entity graph in `data-model/shapes-data-model.yml`.

## Example

```bash
curl "https://api.shapes.inc/shapes/public/tenshi"
```
