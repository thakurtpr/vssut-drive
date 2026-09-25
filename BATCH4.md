Before an account can be used, the bank needs the customer's details on record.

Build POST /customers, which accepts name, email, phone, and city.

Rules

name must be at least 2 characters long.
email must look valid: text, then @, then text, then ., then text.
phone must be exactly 10 digits and start with 6, 7, 8, or 9.
city is optional and defaults to Unknown.
Emails are unique. If one already exists in customers.csv, return 409. Compare emails without regard to case.

On success

Generate a customer_id such as CUST0001, incrementing from the last ID in the file.
Append the customer to customers.csv, creating the file with headers if needed.
Return 201 with the saved customer.