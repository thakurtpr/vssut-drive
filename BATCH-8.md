## AI-Assisted Coding Interview: OTP Verification API (10 Minutes)

You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.
---

## Part 1: Candidate Sheet (hand this over)

### Task

Build an OTP (one-time password) API in any language. You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.

### Database

Use PostgreSQL in Docker:

```bash
docker run -d --name pg -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=otp -p 5432:5432 postgres:16
```

Connection: `postgres://postgres:secret@localhost:5432/otp`

The database is empty. Your app must create its own table on startup.

### Endpoints

**1. `POST /otp/send`**: generate an OTP

```json
{ "phone": "9876543210" }
```

- The phone must be a 10-digit Indian mobile number starting with 6, 7, 8, or 9. Also accept it with a `+91` prefix.
- Generate a **6-digit** OTP that is valid for **2 minutes**.
- Sending again for the same phone replaces the old OTP.
- Return the OTP in the response (this is a mock; no real SMS is sent).

**2. `POST /otp/verify`**: check an OTP

```json
{ "phone": "9876543210", "otp": "048213" }
```

- A correct OTP returns `200`. **Each OTP can be used only once.**
- A wrong OTP returns `401`. After **3 wrong attempts**, the OTP is blocked, and even the correct one fails.
- An expired OTP returns `410`.
- A phone with no OTP returns `404`.

---
