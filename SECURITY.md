# Security Policy

Security is a core part of how I build software. I appreciate the work of researchers and users who help keep my projects and their users safe, and I am committed to handling every report responsibly.

## Supported Versions

Security fixes are applied to the latest release and the default branch (`main`) of each public repository.

| Version                   | Supported          |
| ------------------------- | ------------------ |
| Latest release / `main`   | :white_check_mark: |
| Older releases            | :x:                |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues, discussions or pull requests.**

Report them privately through GitHub's private vulnerability reporting:

1. Open the affected repository.
2. Go to the **Security** tab.
3. Click **Report a vulnerability** and fill in the advisory form.

Only the maintainer can see the report until a fix is published.

### What to include

A clear, reproducible report helps me resolve the issue faster. Where possible, please include:

- The affected repository, component and version or commit
- The type of issue (for example XSS, SQL injection, authentication bypass, information disclosure)
- Step-by-step instructions to reproduce it
- Proof-of-concept code, requests or screenshots
- The potential impact and how an attacker could exploit it
- Any suggested fix or mitigation

## Response Process

| Stage                         | Target time                    |
| ----------------------------- | ------------------------------ |
| Acknowledgement of the report | Within 3 business days         |
| Initial assessment and triage | Within 7 business days         |
| Fix for critical issues       | As soon as possible            |
| Fix for other issues          | Within 90 days of the report   |

You will be kept informed of progress. Once the issue is fixed, a security advisory is published on GitHub and, with your permission, you are credited for the discovery.

## Coordinated Disclosure

Please give me reasonable time to investigate and release a fix before sharing any details publicly. I will coordinate the disclosure date with you and aim to publish within 90 days of the original report.

## Safe Harbor

I will not pursue or support legal action against anyone who, in good faith:

- Reports a vulnerability through the private channel above
- Avoids privacy violations, data destruction and service disruption
- Only accesses the data needed to demonstrate the issue, and does not keep or share it
- Does not exploit the issue beyond what is required to confirm it

## Out of Scope

- Vulnerabilities in third-party dependencies that are already publicly known (please report these upstream)
- Findings from automated scanners without a demonstrated impact
- Social engineering, phishing or physical attacks
- Denial-of-service attacks

---

Thank you for helping keep these projects and their users safe.
