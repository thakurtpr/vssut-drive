## Question: Simple Counter API (10 Minutes)

You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.

### Task

Build a named-counter API in any language.

### Database

Use **any database of your choice** (PostgreSQL, MySQL, SQLite, MongoDB, Redis, etc.) or an in-memory data structure (e.g., a dict/map/hashmap in your app process) if you'd rather skip setup entirely. All the rules and status codes below apply regardless of storage choice — the counter's value must simply persist for the duration of the app's run.

*Example, if you want Postgres via Docker:*

```bash
docker run -d --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=counters -p 5432:5432 postgres:16
```

The database (if any) starts empty. Your app must create its own table/collection/schema on startup.

### Endpoints

**1. `POST /counters/<name>/increment`**: increase a counter by 1

- If the counter doesn't exist yet, create it starting at 0, then increment.
- Returns `{ "name": "...", "value": N }`.

**2. `POST /counters/<name>/reset`**: reset a counter to 0

- If the counter doesn't exist, create it at 0.
- Returns `{ "name": "...", "value": 0 }`.

**3. `GET /counters/<name>`**: get current value

- Unknown counter → `404`.
- Returns `{ "name": "...", "value": N }`.

**4. `GET /counters`**: list all counters and their values

