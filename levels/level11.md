# What I Learned – OverTheWire Natas 11

## Objective
The goal of Natas 11 was to manipulate an encrypted cookie so that the server would set:

```json
{"showpassword":"yes","bgcolor":"#ffffff"}
```

When the PHP application receives this value, it executes:

```php
if ($data["showpassword"] == "yes") {
    print "The password for natas12 is ...";
}
```

---

## Understanding the Cookie

The application stored user preferences inside a cookie.

From the source code, I learned that the cookie was created in the following order:

```
JSON
↓
XOR Encryption
↓
Base64 Encoding
↓
Cookie
```

The default JSON stored by the application was:

```json
{"showpassword":"no","bgcolor":"#ffffff"}
```

---

## Why This Could Be Attacked

The PHP source code revealed both the encryption algorithm (XOR) and the default plaintext JSON.

Since I knew:

- The encrypted cookie from the browser.
- The original plaintext JSON from the source code.

I could perform a **known-plaintext attack**.

Using the XOR property:

```
Ciphertext XOR Plaintext = Key (Keystream)
```

I recovered the XOR keystream used to encrypt the cookie.

---

## Attack Process

1. Copy the cookie from the browser.
2. Base64-decode the cookie to obtain the encrypted bytes.
3. XOR the encrypted bytes with the known default JSON.
4. Recover the XOR keystream.
5. Create a new JSON:

```json
{"showpassword":"yes","bgcolor":"#ffffff"}
```

6. XOR the new JSON with the recovered keystream to generate new encrypted bytes.
7. Base64-encode the new encrypted bytes.
8. Replace the original cookie in the browser.
9. Refresh the page to satisfy the PHP condition and reveal the password.

---

## Concepts I Learned

- Reading and understanding PHP source code.
- How web applications store data inside cookies.
- JSON encoding and decoding.
- Difference between Base64 encoding and encryption.
- XOR encryption and why it is reversible.
- Known-plaintext attacks.
- Working with raw bytes instead of plain text.
- Using Linux tools like `base64`, `xxd`, `printf`, and Python to manipulate binary data.

---

## Mistakes I Learned From

While solving this challenge, I made several mistakes that helped me understand the concepts better:

- I initially thought Base64 was encryption.
- I accidentally Base64-encoded hexadecimal text instead of raw binary bytes.
- I used `echo`, which added an unwanted newline to my JSON.
- I confused hexadecimal data, Base64 strings, and raw binary bytes.
- I learned to verify every transformation instead of assuming the previous step was correct.

---

## Key Takeaway

Natas 11 demonstrated that encryption alone does not guarantee security. If an attacker knows the encryption algorithm and part of the plaintext, a weak implementation such as repeating-key XOR can be manipulated. This challenge taught me how understanding the application's source code is often more valuable than blindly attacking it.
