# Natas Level 9

## Objective
Analyze the application's search functionality and identify the security vulnerability to obtain the password for the next level.

## What I Observed

The application accepts user input through a search field and executes the following PHP code:

```php
$key = "";

if (array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if ($key != "") {
    passthru("grep -i $key dictionary.txt");
}
```

The application takes the user's input and inserts it directly into a Linux command executed by the server.

## My Analysis

I first understood how the application processes user input:

1. Check whether the `needle` parameter exists.
2. Store the user input in the `$key` variable.
3. Pass the value directly into the `grep` command using `passthru()`.

Because the application does not validate or safely handle the user's input before executing the shell command, it becomes vulnerable to **OS Command Injection**.

## Security Concept

This level demonstrates **OS Command Injection**.

The vulnerability occurs because user-controlled input is directly concatenated into an operating system command. An attacker can inject additional shell commands, causing the server to execute unintended commands.

## Prevention

- Never trust user-controlled input.
- Validate and sanitize all user input.
- Avoid passing user input directly to shell commands.
- Use built-in programming language functions whenever possible instead of executing system commands.
- If external commands are required, properly escape shell arguments and restrict allowed input.

## Skills Practiced

- Reading PHP source code
- Understanding `$_REQUEST`
- Understanding `array_key_exists()`
- Understanding `passthru()`
- Linux `grep` command
- Identifying OS Command Injection vulnerabilities
- Secure coding principles

## Takeaway

This level taught me that applications should never execute operating system commands using untrusted user input. Improper input handling can allow attackers to execute arbitrary commands on the server, leading to serious security risks.
