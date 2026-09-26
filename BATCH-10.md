## Question: Simple To-Do List API (10 Minutes)

You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.

### Task

Build a to-do list API in any language.

### Database

Use PostgreSQL in Docker:

```bash
docker run -d --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=todos -p 5432:5432 postgres:16
```

Connection: `postgres://postgres:secret@localhost:5432/todos`

The database is empty. Your app must create its own table on startup.

> **No Docker available?** Use an in-memory data structure instead (e.g., a dict/map/hashmap or list in your app process). All the same rules and status codes below still apply — only the storage layer changes.

### Endpoints

**1. `POST /todos`**: create a to-do

```json
{ "title": "Buy groceries" }
```

- `title` must be non-empty; reject with `400` otherwise.
- Returns `{ "id": 1, "title": "Buy groceries", "done": false }`.

**2. `GET /todos`**: list all to-dos

- Returns an array of all to-dos, each with `id`, `title`, `done`.
- Supports an optional query param `?done=true` or `?done=false` to filter.

**3. `PATCH /todos/<id>`**: update a to-do

```json
{ "done": true }
```

- Marks the to-do as done/not done.
- Unknown `id` → `404`.

**4. `DELETE /todos/<id>`**: delete a to-do

- Unknown `id` → `404`; otherwise `204`.

---