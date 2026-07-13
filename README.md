# Authentication Bypass via Client-Controlled Session Cookie

## Overview

Platform: DUCKERZ

Lab: Cookies with milk

Category:
Authentication / Authorization

Difficulty:
Beginner

This writeup documents the analysis of an authentication and authorization issue caused by insecure handling of client-controlled session data.

The goal of the assessment was to identify whether a regular user could access functionality intended for privileged users.

## Vulnerability Classification

- CWE-639: Authorization Bypass Through User-Controlled Key
- CWE-862: Missing Authorization
- OWASP Top 10: A01 - Broken Access Control

## Severity

High

The vulnerability allows privilege escalation by bypassing intended authorization controls.

## Tools Used

- curl — HTTP request analysis and response inspection.
- Browser Developer Tools — application behavior and session analysis.
- Base64 decoding utilities — analysis of encoded session data.
- Git — version control for documentation.

## Reconnaissance

Initial testing was performed to understand the application's authentication flow and available functionality.

The application exposed a login form. After submitting test credentials, the response behavior and session handling mechanisms were analyzed.

## Testing Methodology

The application was tested using manual HTTP request analysis and session inspection.

Tools used:

- curl — for sending HTTP requests and analyzing server responses.
- Browser developer tools — for inspecting application behavior and session data.
- Base64 decoding utilities — for analyzing encoded session information.

Initial testing included:

- Reviewing HTTP responses and status codes.
- Analyzing authentication behavior.
- Inspecting session-related data returned by the application.
- Verifying whether authorization decisions were properly enforced by the server.

## Authentication Flow Analysis

The authentication mechanism was reviewed to understand how user identity and session state were managed.

During testing, the application accepted user input through the login form and generated a session after authentication attempts.

The next step was to analyze how the application stored and validated session information between client and server.

## Session Analysis

The session management mechanism was analyzed to determine whether authorization decisions were performed securely.

During the review, session-related data provided by the client was inspected. The analysis showed that sensitive authorization information was stored in a format that could be interpreted by the client.

This indicated that the application relied on client-controlled data when determining user privileges.

Further validation confirmed that the authorization mechanism lacked proper server-side verification.

## Vulnerability Details

The application contained an authorization weakness caused by insufficient validation of client-controlled session data.

Authorization decisions should always be performed based on trusted server-side information. In this case, the application relied on data supplied by the client when determining user privileges.

An attacker who can manipulate session-related data may be able to bypass intended access restrictions and access functionality assigned to a higher privilege level.

## Security Impact

The vulnerability allows unauthorized privilege escalation from a lower-privileged user context to a higher-privileged context.

Potential impact:

- Unauthorized access to restricted functionality
- Privilege escalation
- Exposure of sensitive application resources
- Loss of access control integrity

## Remediation

To prevent this type of vulnerability, authorization decisions should not rely on client-controlled data.

Recommended security improvements:

- Store authorization information on the server side and reference it using a secure session identifier.
- Validate user privileges on every protected endpoint.
- Implement server-side access control checks.
- Avoid trusting sensitive values received from the client.
- Apply the principle of least privilege when assigning user permissions.

## Lessons Learned

This assessment highlighted the importance of analyzing how applications manage authentication and authorization separately.

A successful login does not guarantee secure authorization. Session handling and access control mechanisms must always be reviewed for improper trust of client-side data.

## Disclaimer

AI tools were used as an assistant for documentation and language improvement. All testing decisions, findings, and technical analysis were performed by the author.
