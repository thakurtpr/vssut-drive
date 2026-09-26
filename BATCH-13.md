## Question: Simple Bookmark API (10 Minutes)

You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.

### Task

Build a bookmark-saving API in any language.

### Database

Use **any database of your choice** (PostgreSQL, MySQL, SQLite, MongoDB, Redis, etc.) or an in-memory data structure (e.g., a dict/map/hashmap or list in your app process) if you'd rather skip setup entirely. All the rules and status codes below apply regardless of storage choice.

*Example, if you want Postgres via Docker:*

```bash
docker run -d --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=bookmarks -p 5432:5432 postgres:16
```

The database (if any) starts empty. Your app must create its own table/collection/schema on startup.

### Endpoints

**1. `POST /bookmarks`**: save a bookmark

```json
{ "url": "https://example.com/article", "tags": ["reading", "tech"] }
```

- `url` must be a valid `http`/`https` URL; reject anything else with `400`.
- `tags` is optional; defaults to an empty list if omitted.
- Saving the same `url` again should **update its tags** rather than create a duplicate entry.
- Returns `{ "id": 1, "url": "...", "tags": [...] }`.

**2. `GET /bookmarks`**: list bookmarks

- Returns all bookmarks by default.
- Supports an optional query param `?tag=reading` to filter by tag (only bookmarks containing that tag).

**3. `DELETE /bookmarks/<id>`**: delete a bookmark

- Unknown `id` → `404`; otherwise `204`.

---
