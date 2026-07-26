# Natas Level 15

## Goal
Get the password for Natas Level 16.

## Procedure
1. Logged into the website using the credentials provided for Natas Level 15.
2. Inspected the PHP source code of the page.
3. Identified that user input was directly concatenated into an SQL query, making the application vulnerable to SQL Injection.
4. Observed that the application did not display the query results. Instead, it only returned either **"This user exists."** or **"This user doesn't exist."**
5. Recognized this as a Boolean-based Blind SQL Injection vulnerability.
6. Wrote a Python script using the `requests` library to automate HTTP requests to the web server.
7. The script tested one character at a time for each position of the password by sending a crafted SQL query.
8. Checked the server's response after each request. When the response contained **"This user exists."**, the script identified the correct character and appended it to the password.
9. Repeated the process until all 32 characters of the password were recovered.
10. Successfully obtained the password for Natas Level 16.

## Knowledge Acquired
- Learned how Boolean-based Blind SQL Injection works.
- Understood that applications can still leak sensitive information even when they do not display database query results directly.
- Learned how to automate repetitive web requests using Python.
- Learned how to use the `requests` library to communicate with a web server.
- Understood how to analyze HTTP responses and use them to make decisions in an automation script.
- Improved understanding of Python concepts such as loops, conditional statements, string manipulation, variables, and functions.
- Learned that SQL Injection vulnerabilities can be prevented by using prepared statements and parameterized queries instead of directly concatenating user input into SQL queries.
