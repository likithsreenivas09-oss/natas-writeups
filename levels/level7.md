## What I Learned

This level taught me that many web applications use URL parameters such as:

```
?page=home
```

The value of the parameter is often retrieved on the server using PHP, for example:

```php
include($_GET['page']);
```

If the application does not validate or restrict the user input, an attacker may be able to replace the expected page with the path of another file that exists on the server.

Example:

```
?page=/etc/natas_webpass/natas8
```

Instead of loading a normal webpage, the application attempts to read that file. If the server has permission to access it, the file contents are returned to the user.

## Security Lesson

- Never trust user-controlled input in file inclusion functions.
- Validate input using a whitelist of allowed files.
- Avoid allowing arbitrary file paths from user input.
- Store sensitive files securely and prevent direct access.
