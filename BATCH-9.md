### Seat Booking API (10 Minutes)

You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.

### Task

Build a seat-booking API for a small movie screening in any language.

### Database

Use Any Database in Docker:

```bash
docker run -d --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=booking -p 5432:5432 postgres:16
```

Connection: `postgres://postgres:secret@localhost:5432/booking`

The database is empty. Your app must create its own table(s) on startup, seeded with **20 seats** (`A1`–`A10`, `B1`–`B10`).

> **No Docker available?** Use an in-memory data structure instead (e.g., a dict/map/hashmap in your app process) seeded with the same 20 seats. All the same rules and status codes below still apply — only the storage layer changes.

### Endpoints

**1. `POST /seats/hold`**: temporarily hold a seat

```json
{ "seat": "A5", "user": "9876543210" }
```

- A seat can only be held or booked by one user at a time.
- A hold **expires after 60 seconds** if not confirmed.
- Holding an already-held (unexpired) or already-booked seat returns `409`.
- Invalid seat ID → `404`.
- Returns `{ "held_until": "..." }`.

**2. `POST /seats/confirm`**: confirm a booking

```json
{ "seat": "A5", "user": "9876543210" }
```

- Confirms only if the *same user* currently holds that seat and the hold hasn't expired.
- Wrong user trying to confirm → `403`.
- Hold expired → `410`.
- No active hold on that seat → `404`.
- Already booked → `409`.

**3. `GET /seats`**: list all seats with status (`available`, `held`, `booked`) for each.

---
