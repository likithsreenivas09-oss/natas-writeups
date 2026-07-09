# Natas Level 10

## Objective

Analyze the application's search functionality and identify why the implemented security filter can still be bypassed.

## What I Observed

The application accepts user input through the `needle` parameter and executes the following command:

```php
passthru("grep -i $key dictionary.txt");
```

Before executing the command, the application checks whether the user input contains the following characters:

```php
preg_match('/[;|&]/', $key)
```

If any of these characters are detected, the application blocks the request.

## My Analysis

The developer attempted to prevent command injection by blacklisting a few special characters. However, the user input was still passed directly into the `grep` command without being safely handled.

Although executing additional commands using `;`, `|`, or `&` was prevented, it was still possible to manipulate the arguments passed to the existing `grep` command. This allowed the application to search unintended files on the server.

This demonstrates that blocking only a few dangerous characters is not a complete security solution.

## Security Concept

This level demonstrates **Argument Injection**.

Instead of executing a new command, the attacker changes the arguments of an existing command, causing it to behave in an unintended way.

## Prevention

- Never pass untrusted user input directly to shell commands.
- Avoid relying on blacklist-based input validation.
- Use strict input validation (whitelisting) where appropriate.
- Escape shell arguments when external commands must be used.
- Prefer built-in programming language functions instead of executing shell commands whenever possible.

## Skills Practiced

- Reading PHP source code
- Understanding `preg_match()`
- Understanding blacklist-based validation
- Understanding Linux `grep`
- Identifying Argument Injection
- Secure input validation principles

## Takeaway

This level taught me that blocking only a few dangerous characters does not make an application secure. Even with input validation in place, applications remain vulnerable if user-controlled data is passed directly to shell commands. Secure applications should avoid executing shell commands with untrusted input or safely validate and escape user input before execution.
