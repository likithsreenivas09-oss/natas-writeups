# Natas Level 13

## Goal
Get the password for Natas Level 14.

## Procedure
1. Accessed the website using the provided credentials.
2. Read and analyzed the PHP source code to understand the file upload process.
3. Identified the validation checks performed before accepting an uploaded file.
4. Learned that the application used `exif_imagetype()` to identify uploaded files as images by checking their file signature (magic bytes).
5. Observed that the uploaded file was saved using the extension supplied by the client.
6. Analyzed the application's security assumptions and determined that image identification alone was not sufficient validation.
7. After understanding the upload logic, successfully bypassed the upload restriction and accessed the next level.

## Problems Faced
- Initially misunderstood the purpose of `exif_imagetype()`.
- Learned the difference between file extensions and file signatures (magic bytes).
- Had to understand how PHP handles file uploads using `$_FILES`.
- Faced browser connectivity issues while accessing the challenge and resolved them before continuing.

## Knowledge Acquired
- How PHP processes file uploads.
- The purpose of `$_FILES`, `pathinfo()`, and `move_uploaded_file()`.
- How `exif_imagetype()` identifies image files using their file signature.
- The difference between file identification and complete file validation.
- The importance of tracing user-controlled input through the application before drawing conclusions.

## Lesson in Cybersecurity
File upload functionality should never rely on a single validation mechanism. Identifying a file as an image does not guarantee that it is safe. Secure upload systems require multiple layers of validation, careful handling of user-controlled input, and secure server-side configuration.

## Skills Improved
- PHP source code analysis
- File upload security concepts
- Reading official documentation
- Identifying user-controlled input
- Security-focused code review
- Debugging and analytical thinking
