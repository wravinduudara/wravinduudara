# Broken brute-force protection, IP block

**Platform:** PortSwigger Web Security Academy
**Topic:** Authentication vulnerabilities
**Date completed:** 30 Sep 2026

## What the vulnerability is
The login page tries to stop brute-force attacks by blocking an IP address after too many failed logins. But the logic is flawed: the failed-attempt counter resets when a login succeeds. That means the protection can be bypassed.

## How I found it
- (Describe what you noticed when you tested the login page: how many wrong attempts triggered the block, and what happened after.)
- (Describe what you noticed about the counter, and what made you think of using a successful login.)

## How I solved it
- (Your steps in your own words: which tool you used, what you sent, how you arranged the requests, and how you knew you found the right password.)
- (Add 1-2 screenshots with any real credentials or session tokens hidden.)

## Why it works
The server tracks failures per IP but clears the count on any successful login, even one for a different account. Because I could log in to my own account between guesses, the counter never reached the limit, so the block never triggered.

## How to fix it
- Count failed attempts per account and per IP, and don't reset the account's counter just because a different login succeeded.
- Use account lockouts or increasing delays after repeated failures.
- Add CAPTCHA or multi-factor authentication.
- Use rate limiting that can't be reset by the attacker's own actions.

## What I learned
(One or two sentences about what surprised you or what you'd test for on a real login page.)
