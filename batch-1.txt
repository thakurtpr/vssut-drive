Build POST /payments, which accepts account_id, amount, and an Idempotency-Key request header.

On the first request with a given key, generate a txn_id, append the payment to payments.csv (create the file with headers if it is missing), and store the full response in idempotency.json against that key.
On any repeat request with the same key and the same body, return the stored response without writing a new row.
If the same key arrives with a different body, return 422.
A request with no key returns 400.
Keys expire after 24 hours.

Done when: sending the same request 5 times produces exactly 1 row in payments.csv and 5 identical responses.