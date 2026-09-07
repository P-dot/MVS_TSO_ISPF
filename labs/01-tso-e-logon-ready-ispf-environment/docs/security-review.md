# Publication Security Review — Lab 01

## Review status

**PASS — sanitized evidence set prepared for public GitHub publication.**

## Actions performed

1. Excluded the source screenshot that displayed an ADCD user/password table.
2. Redacted the upper-right network/terminal identification area from the initial ADCD screen.
3. Redacted the same area from the final return-to-ADCD screen.
4. Confirmed visually that the retained TSO/E LOGON panel does not show the entered password.
5. No screenshot intentionally exposes an IP address, MAC address, host adapter name or VTAM terminal identifier.

## Evidence deliberately not published

The credential/reference banner captured during the source session is not part of the repository evidence set.

## Text-file scan

Before commit, the accompanying Git Bash workflow includes a recursive pattern scan over repository text files for common private-IP and MAC-address formats. Image evidence has been visually reviewed because pixel content is not reliably checked with ordinary `grep`.
