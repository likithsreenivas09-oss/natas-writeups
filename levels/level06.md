# Natas Level 6

## Objective
Find the correct secret value to obtain the password for the next level.

## What I Observed

The PHP source code includes another file:

```php
include "includes/secret.inc";
```

The application compares the user input with the `$secret` variable stored inside `secret.inc`.

```php
if ($secret == $_POST['secret']) {
    print "Access granted.";
}
```

## Key Learning

The secret value is not stored directly in the main PHP file but is loaded from an external file using PHP's `include` statement.

This level demonstrates the importance of protecting files that contain sensitive information. If a file containing secrets is stored in a web-accessible location and is not properly protected, an attacker may be able to access it directly and retrieve confidential information.

## Security Concept

- Never store sensitive information in publicly accessible files.
- Do not rely on hidden filenames as a security mechanism.
- Store secrets outside the web root or restrict direct access using proper server configuration.
- Sensitive configuration files should never be exposed to users.

## Skills Practiced

- Reading PHP source code
- Understanding the `include` statement
- Identifying external configuration files
- Recognizing insecure storage of sensitive information
- Basic web application security analysis

## Takeaway

Security is not just about hiding information in separate files. Sensitive data must be stored securely and protected from direct access through proper server configuration and secure application design.
