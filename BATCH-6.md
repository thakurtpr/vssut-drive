### Task

You may use any AI tool. You have **10 minutes**, and you'll be asked to explain your code at the end.



Common Setup 
Run the database in Docker using docker run or docker compose.
The app reads the connection details from environment variables such as DATABASE_URL or REDIS_URL. They must never be hard-coded.
On startup, the app creates its tables if they don't exist, so it runs against a completely empty database.
If the database is not reachable, the API returns 503 with the message Database unavailable rather than crashing.
Bonus: put the app itself in the same docker-compose.yml, so docker compose up starts everything.



Problem 1: Record a Debit or Credit (PostgreSQL)

Build POST /txns, which accepts account_id, amount, and type (debit/credit).

Database

On startup, create a table ledger with the columns txn_id (primary key), account_id, type, amount (numeric with 2 decimals), and created_at (defaults to the current time).

Rules

amount must be greater than 0, and type must be debit or credit. Otherwise return 400.
Generate a unique txn_id and insert the row into ledger.
Return 201 with the saved row, including the created_at value the database generated.

Sample request

json
{ "account_id": "ACC001", "amount": 1500.50, "type": "credit" }

Done when: after 3 calls, SELECT COUNT(*) FROM ledger returns 3.











