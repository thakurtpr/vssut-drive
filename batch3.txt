Build POST /txns, which accepts account_id, amount, and type (debit/credit).

Reject an amount of 0 or less, or any type other than debit/credit, with 400.
Generate a txn_id and a timestamp, then append the transaction to ledger.csv, creating the file with headers if it is missing.
Return the saved row.

Done when: 3 calls produce 3 rows, each with a unique txn_id.