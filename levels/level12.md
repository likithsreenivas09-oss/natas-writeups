# Natas Level 12 – What I Learned

## Objective
Understand how insecure file upload functionality can lead to remote code execution when the server trusts client-controlled input.

## What I Learned

- Learned how PHP handles file uploads using the `$_FILES` superglobal.
- Understood how `genRandomString()` generates a random 10-character filename using a `for` loop and `mt_rand()`.
- Learned that the application replaces the original filename with a randomly generated filename to prevent filename collisions.
- Understood how `makeRandomPath()` ensures every uploaded file has a unique filename by checking `file_exists()`.
- Learned how `pathinfo()` extracts the file extension from a filename.
- Understood that uploaded files are first stored in a temporary location (`$_FILES['uploadedfile']['tmp_name']`) before being moved to the final upload directory using `move_uploaded_file()`.
- Learned that the application limits uploads to files smaller than 1000 bytes.

## Vulnerability

- Identified that the application **trusts the hidden `filename` POST parameter** instead of the uploaded file's actual filename.
- Discovered that the hidden field is generated as:

```html
<input type="hidden" name="filename" value="<?php print genRandomString(); ?>.jpg">
```

- Learned that hidden HTML form fields are **client-controlled** and can be modified before the request reaches the server.
- Understood that changing the hidden `filename` value changes the extension that the server assigns to the uploaded file.

## Security Lessons

- Never trust client-side input, including hidden form fields.
- Validate file extensions on the server using a whitelist.
- Verify the actual file type instead of relying only on the filename extension.
- Store uploaded files in locations where server-side scripts cannot be executed.
- Always treat all client-supplied data as untrusted.
