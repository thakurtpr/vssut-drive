### Task

Build a small wallet API in any language. You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.

### Database

Use PostgreSQL in Docker/PODMAN. This command is ready to run:

```bash
docker run -d --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=wallet -p 5432:5432 postgres:16
```

Connection: `postgres://postgres:secret@localhost:5432/wallet`

The database is empty. Your app must create its own table on startup.

### Endpoints

**1. `POST /wallets`**: create a wallet

```json
{ "user_name": "ravi" }
```

- The user name must be unique. `Ravi` and `ravi` count as the same user.
- A new wallet starts with a balance of 0.
- Return the `wallet_id` and the balance.

**2. `POST /wallets/{id}/topup`**: add money

```json
{ "amount": 500.25 }
```

- The amount must be greater than 0 with at most 2 decimal places.

**3. `POST /wallets/{id}/pay`**: pay from the wallet

```json
{ "amount": 200 }
```

- A payment must never make the balance go negative. Return `409` if the balance is too low.

### Expected Status Codes

`201` for a created wallet, `200` for success, `400` for bad input, `404` for an unknown wallet, `409` for a duplicate user or insufficient balance.

---
