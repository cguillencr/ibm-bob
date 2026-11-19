# Portable security-by-default rules (all modes)
This is a general engineering baseline, not an official organizational policy or a replacement for organizational standards. Apply controls proportionately to project risk; document justified exceptions for review.
- Dependency hygiene: prefer supported, maintained, patched releases; verify versions, license, vulnerabilities and compatibility rather than assuming the latest is safe. Use appropriate lockfiles and dependency scanning.
- Containers: prefer minimal trusted images, non-root execution, least privilege, image scanning and pinned immutable digests for reproducible deployments. Evaluate registry requirements per organization.
- Network: use TLS, certificate verification, timeouts and least-exposed interfaces. Bind to 0.0.0.0 only when the deployment requires it and network controls protect exposure; flag and document the risk.
- Secrets: never hardcode, commit or expose secrets. Use approved vaults or secure runtime injection; keep .env files out of Git. Rotate compromised credentials.
- Data protection: protect sensitive data in transit and at rest using established cryptography and key management; never invent encryption algorithms.
- Identity: use appropriate standard authentication, server-side authorization and least privilege; secure sessions and require MFA where risk warrants it.
- Inputs/outputs: validate inputs server-side, use parameterized queries and context-aware output encoding; avoid eval of untrusted input.
- Observability: structured logs with appropriate levels; do not log tokens, passwords or personal data; secure access and retention.
- Error handling: return safe client-facing errors while retaining sanitized diagnostics in controlled channels.
- Assurance: propose SAST, SCA, security tests and CI checks; distinguish proposed scans from scans actually run. Escalate findings with severity, evidence and remediation guidance.
- If a security check cannot be performed, state NOT VERIFIED and provide the required command, tool or human approval.
