# Natas Level 8

## Objective
Recover the original secret by analyzing the encoding function and use it to obtain the password for the next level.

## What I Observed

The application did not store the secret in plain text. Instead, it stored an encoded version and used the following function to encode user input before comparison:

```php
function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```

## My Analysis

Instead of guessing the secret, I analyzed how the application transformed the input.

The encoding process was:

1. Convert the original secret to Base64.
2. Reverse the Base64 string.
3. Convert the reversed string into hexadecimal.

Since the encoding algorithm was visible in the source code, I reversed each operation in the opposite order:

1. Convert hexadecimal back to its original bytes.
2. Reverse the string.
3. Decode the Base64 value.

This recovered the original secret, which matched the application's expected input.

## Security Lesson

This level demonstrates that **encoding is not encryption**. Simply transforming data into another format does not protect sensitive information. If an attacker understands the encoding process, they can reverse it and recover the original value.

## Skills Practiced

- Source code analysis
- Understanding PHP functions
- Base64 encoding and decoding
- Hexadecimal conversion
- Reversing an encoding algorithm
- Logical analysis of application behavior

## Takeaway

Always assume that any encoding algorithm visible in the application's source code can be reversed. Sensitive data should be protected using proper cryptographic techniques rather than simple encoding.
