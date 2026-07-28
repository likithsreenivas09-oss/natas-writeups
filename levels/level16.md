# Natas Level 16

## Objective

Analyze the application's search functionality and understand why filtering a small set of special characters is not sufficient to secure shell command execution.

## What I Observed

The application accepts user input through the `needle` parameter and executes the following command:

```php
passthru("grep -i \"$key\" dictionary.txt");
```

Before executing the command, the application checks whether the input contains any of the following characters:

```php
preg_match('/[;|&`\'"]/', $key)
```

If any of these characters are detected, the request is rejected.

## My Analysis

The developer attempted to secure the application by blacklisting a few shell metacharacters before passing user input to a shell command.

Although the blacklist blocks several commonly used special characters, the application still relies on passing user-controlled input directly to the shell. This demonstrates that blacklisting individual characters is not a reliable security mechanism because shell parsing is complex and many features remain available.

The root issue is not the blacklist itself—it is executing a shell command using untrusted user input.

## Security Concept

This level demonstrates the dangers of **Command Injection** and why **blacklist-based input validation** is an ineffective defense.

Applications should never assume that blocking a few special characters makes shell command execution safe.

## Prevention

- Never pass untrusted user input directly to shell commands.
- Avoid blacklist-based input validation.
- Use allowlist (whitelist) validation whenever possible.
- Escape shell arguments using appropriate functions such as `escapeshellarg()` when external commands are required.
- Prefer built-in programming language functions instead of executing shell commands.

## Skills Practiced

- Reading PHP source code
- Understanding `preg_match()`
- Understanding `passthru()`
- Understanding HTTP GET requests
- Understanding PHP string interpolation
- Understanding shell command construction
- Understanding blacklist-based validation
- Secure input validation principles

## Takeaway

This level reinforced that application security should not depend on blocking a handful of dangerous characters. Whenever user-controlled data is passed to a shell, the safest approach is to avoid shell execution entirely or properly validate and escape all inputs. Understanding how PHP constructs shell commands and how the operating system interprets them is essential for writing secure applications.
