## Question: Simple Coupon Code API (10 Minutes)

You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.

### Task

Build a coupon code API in any language.

### Database

Use PostgreSQL in Docker:

```bash
docker run -d --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=coupons -p 5432:5432 postgres:16
```

Connection: `postgres://postgres:secret@localhost:5432/coupons`

The database is empty. Your app must create its own table on startup.

> **No Docker available?** Use an in-memory data structure instead (e.g., a dict/map/hashmap or list in your app process). All the same rules and status codes below still apply — only the storage layer changes.

### Endpoints

**1. `POST /coupons`**: create a coupon

```json
{ "code": "SAVE10", "discount_percent": 10, "max_uses": 3 }
```

- `discount_percent` must be an integer from **1 to 100**; reject otherwise with `400`.
- `max_uses` must be a positive integer.
- `code` must be unique (case-insensitive); duplicate → `409`.
- Returns `{ "code": "SAVE10", "discount_percent": 10, "max_uses": 3, "used": 0 }`.

**2. `POST /coupons/apply`**: apply a coupon to an order

```json
{ "code": "save10", "amount": 500 }
```

- Coupon lookup is **case-insensitive**.
- Unknown code → `404`.
- Coupon already used `max_uses` times → `410`.
- On success, increment the coupon's `used` count and return `{ "original_amount": 500, "discount_percent": 10, "final_amount": 450 }`.
- `final_amount` should be rounded to the nearest whole number.

**3. `GET /coupons/<code>`**: check coupon status

- Case-insensitive lookup.
- Returns `{ "code": "...", "discount_percent": N, "max_uses": N, "used": N, "remaining": N }`.
- Unknown code → `404`.

---
