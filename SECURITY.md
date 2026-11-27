# Security Policy

This policy applies to every public repository owned by [@baranakgull](https://github.com/baranakgull), unless a repository ships its own `SECURITY.md`. In that case the repository's file takes precedence.

Most of my projects are AI-powered applications: voice assistants, RAG pipelines, LLM agents and automation tools. Besides classic web and infrastructure flaws, this policy covers the issues that are specific to those systems.

---

## 1. Supported versions

| Version | Supported |
| --- | --- |
| Default branch (`main` / `master`) | ✅ |
| Latest tagged release | ✅ |
| Older releases and tags | ❌ (please upgrade first and check whether the issue still reproduces) |
| Archived repositories | ❌ |
| Forks owned by other people | ❌ (report to the fork's owner) |

---

## 2. How to report

**Do not report vulnerabilities in public issues, discussions, pull requests, commit comments or social media.**

Report privately through GitHub's private vulnerability reporting:

1. Open the affected repository.
2. Go to the **Security** tab.
3. Click **Report a vulnerability** and fill in the advisory form.

Only the maintainer and you can see the report until an advisory is published.

If the **Report a vulnerability** button is missing, open a public issue that says only *"I would like to report a security issue, please contact me"*. Do not include any details. I will reach out and give you a private channel.

### What to include

The more of this you provide, the faster I can fix it:

- **Where:** repository, file or component, branch and commit hash or release version.
- **What:** vulnerability type, ideally with a CWE identifier (for example CWE-79 XSS, CWE-89 SQL injection, CWE-611 XXE, CWE-1427 prompt injection).
- **How:** minimal step-by-step reproduction, proof-of-concept code, HTTP requests, input files or prompts.
- **Environment:** OS, runtime version (Python, Node, .NET), container image, model and provider if relevant.
- **Impact:** what an attacker gains (code execution, data access, privilege escalation, cost abuse) and under which preconditions.
- **Severity estimate:** a CVSS v3.1 or v4.0 vector if you have one.
- **Fix idea:** optional, but welcome.
- **Credit:** the name or handle you want to be credited with, or a request to stay anonymous.

Please send one report per issue. If several issues chain together, describe the chain in one report and link the parts.

---

## 3. What happens next

| Stage | Target time |
| --- | --- |
| Acknowledgement of your report | 3 business days |
| Triage: confirmed / not reproducible / out of scope, with severity | 7 business days |
| Status updates while the fix is in progress | at least every 14 days |
| Fix released — **Critical** | 7 days after triage |
| Fix released — **High** | 30 days after triage |
| Fix released — **Medium** | 60 days after triage |
| Fix released — **Low** | 90 days or next planned release |

These are targets for a project maintained by one person, not contractual guarantees. If a target will be missed, I will tell you why and give a new date.

### Severity

Severity follows CVSS, adjusted for real-world impact in the project's intended deployment:

- **Critical:** unauthenticated remote code execution; leakage of secrets (API keys, tokens, credentials); full read or write access to user data.
- **High:** authentication or authorization bypass; injection (SQL, command, template); prompt injection that makes an agent run tools, exfiltrate data or act on behalf of the user; stored XSS.
- **Medium:** reflected XSS; CSRF on state-changing actions; SSRF with limited reach; sensitive data in logs; denial of service that a single request can trigger.
- **Low:** missing security headers; verbose error messages; issues that need unlikely preconditions.

### After the fix

1. A fix is merged to the default branch, and a release is tagged if the project uses releases.
2. A GitHub Security Advisory is published, with a CVE requested through GitHub when the issue warrants one.
3. You are credited in the advisory, unless you asked to stay anonymous.
4. Each fix comes with a regression test that reproduces the original issue.

---

## 4. Coordinated disclosure

- Please keep details private until the advisory is published, or until 90 days after your report, whichever comes first.
- If the issue is being actively exploited, I may publish sooner, and I will tell you before I do.
- If you need an earlier date (a conference talk, for example), tell me and we will agree on one.
- If I stop responding for 30 days despite reminders, you may disclose responsibly.

---

## 5. Scope

### In scope

**Application and web**
- Injection: SQL, NoSQL, OS command, template, LDAP.
- XSS, CSRF, open redirects, clickjacking on sensitive actions.
- Authentication, session and cookie flaws; broken access control and IDOR.
- SSRF, path traversal, unsafe file upload, XXE, insecure deserialization.
- Exposed API endpoints that lack authentication or rate limiting.

**AI, LLM and RAG specific**
- **Direct and indirect prompt injection:** malicious text in a user message, a retrieved document, a web page, an email or a file that makes the model ignore its instructions, call tools, or leak data.
- **Tool and agent abuse:** an agent executing commands, writing files, sending messages or calling APIs beyond its intended permissions.
- **System prompt or secret disclosure:** the system prompt, hidden instructions or credentials leaking through model output.
- **RAG data leakage:** retrieval returning documents that the requesting user is not allowed to see; cross-tenant leakage in vector stores.
- **Data and memory poisoning:** inputs that persistently corrupt embeddings, memory stores, few-shot examples or fine-tuning data.
- **Unsafe output handling:** model output rendered as HTML, executed as code or used in queries without validation.
- **Cost and resource abuse:** inputs that force unbounded token use, recursion or model calls.
- **Voice and audio paths:** spoofed wake words, audio-borne injection, or unauthorized device control in voice assistants.

**Infrastructure and supply chain**
- Secrets committed to a repository or baked into a container image.
- Insecure defaults in `Dockerfile`, `docker-compose.yml`, CI workflows or deployment config.
- Vulnerable dependencies **when they are actually exploitable** in my code.
- GitHub Actions workflow flaws: script injection, overly broad `GITHUB_TOKEN` permissions, `pull_request_target` misuse.

**Privacy**
- Personal data processed or stored in ways that conflict with **KVKK** (Turkish Personal Data Protection Law) or **GDPR**: missing minimization, logging of personal data, retention without purpose.

### Out of scope

- Known vulnerabilities in third-party dependencies that are not reachable from my code (please report them upstream).
- Reports generated by automated scanners without a demonstrated, reproducible impact.
- Model "jailbreaks" that only produce offensive or off-topic text **without** a security impact such as data access, tool execution or bypassing an authorization check. Report harmful model behavior to the model provider instead.
- Hallucinations or factually wrong answers, unless they cause a security impact.
- Missing best practices with no exploitable consequence (for example a missing `X-Powered-By` removal).
- Social engineering, phishing or physical attacks against me or any user.
- Volumetric denial of service (flooding, load testing).
- Issues in demo, example or test code clearly marked as not for production.
- Issues that require an already compromised device, a malicious browser extension, or root access.
- Vulnerabilities in services I do not operate (GitHub, cloud providers, model APIs).

---

## 6. Testing rules (safe harbor)

I will not pursue or support legal action against anyone who acts in good faith and follows these rules:

- Test only against **your own local or self-hosted copy** of a project. Do not test against any deployment run by me or by other users without written permission.
- Do not access, modify, delete or keep data that is not yours. If you reach real personal data by accident, stop, do not copy it, and include only what is needed to prove the issue in your report.
- Do not degrade service availability or run denial-of-service tests.
- Do not use social engineering, phishing or physical access.
- Do not run up costs on paid APIs (LLM, cloud) that belong to someone else.
- Give me reasonable time to fix the issue before disclosure, as described in §4.
- Comply with applicable law, including KVKK and GDPR.

If you are unsure whether something is allowed, ask in your report before testing further.

This safe harbor covers my own projects only. It cannot grant permission on behalf of third parties such as GitHub, cloud providers or model providers.

---

## 7. How I keep projects secure

- **Secrets:** never committed; loaded from environment variables or an OS credential store; `.env` and credential files are in `.gitignore`.
- **Dependencies:** Dependabot alerts and security updates are enabled where available; lockfiles are committed.
- **Code scanning:** CodeQL or an equivalent static analyzer on public repositories where the language is supported.
- **Secret scanning and push protection:** enabled on public repositories.
- **AI systems:** retrieved documents, files, emails and web pages are treated as data, never as instructions; agents run with least-privilege tool allowlists; model output is validated before it is rendered, executed or stored.
- **Containers:** minimal base images, non-root users, no secrets in image layers.
- **Fixes:** every security fix ships with a regression test.

---

## 8. No bug bounty

I do not offer monetary rewards. I am grateful for every good-faith report, and I credit reporters publicly in the advisory unless they ask to stay anonymous.

---

*Last updated: 2026-11-27*
