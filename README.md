# Authentication Bypass via Client-Controlled Session Cookie

## Overview

Platform: DUCKERZ

Lab: Cookies with milk

Category:
Authentication / Authorization

Difficulty:
Beginner

## Overview

This writeup documents the analysis of an authentication and authorization issue caused by insecure handling of client-controlled session data.

The goal of the assessment was to identify whether a regular user could access functionality intended for privileged users.

## Vulnerability Classification

- CWE-639: Authorization Bypass Through User-Controlled Key
- CWE-862: Missing Authorization
- OWASP Top 10: A01 - Broken Access Control

## Reconnaissance

Initial testing was performed to understand the application's authentication flow and available functionality.

The application exposed a login form. After submitting test credentials, the response behavior and session handling mechanisms were analyzed.

## Objective

The objective of this assessment was to analyze the authentication mechanism and determine whether authorization decisions relied on client-controlled session data.

## Methodology

The assessment included:

1. Initial application reconnaissance
2. Authentication testing
3. Session cookie analysis
4. Authorization validation

## Findings

The application used client-controlled session data containing authorization-related information.

The server failed to properly validate the integrity of this data, which allowed unauthorized access to privileged functionality.

## Impact

An attacker may modify session-related data and gain access to restricted application functionality.

## Remediation

Recommended fixes:

- Store session information server-side.
- Use signed session tokens.
- Validate authorization on every request.
- Do not trust client-controlled data.

## Lessons Learned

- Authentication and authorization should be tested separately.
- Session mechanisms require careful analysis after login.
- Client-controlled values must not determine user privileges.
