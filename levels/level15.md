# Natas Level 14

## Goal
Get the password for Natas Level 15.

## Procedure
1. Logged into the website using the credentials provided for Natas Level 14.
2. Inspected the PHP source code of the login page.
3. Identified that the SQL query was constructed by directly concatenating user input into the query string.
4. Recognized this as a classic SQL Injection vulnerability.
5. Used a SQL injection payload to manipulate the `WHERE` condition so that it evaluated to true, bypassing the authentication check.
6. Successfully logged in without knowing the actual password and obtained the password for Natas Level 15.

## Knowledge Acquired
- Learned how SQL queries are built using user input.
- Understood that directly concatenating user input into SQL queries is highly insecure.
- Learned how SQL Injection can alter the logic of a query and bypass authentication.
- Understood the purpose of conditions such as `1=1` or `"1"="1"`, which always evaluate to `TRUE`.
- Learned that the application only checked whether the query returned at least one row using `mysqli_num_rows()`, allowing authentication to succeed when the injected condition returned a matching row.
- Learned that the proper defense against SQL Injection is to use prepared statements (parameterized queries) instead of concatenating user input directly into SQL queries.
