# Case study: turning security training into reusable AI coding rules

## Motivation
A software security training included diagnostics and good practices. The idea is to translate the lessons into project-level Bob rules, then ask Bob to inspect a codebase and continue applying those rules while implementing changes.

## Source-derived categories
The provided training-derived Markdown covers package support and vulnerabilities, container provenance and non-root execution, TLS and network exposure, secrets, encryption, identity, authorization, logging, input validation, error handling and security testing. The document also includes organization-specific mandates (for example particular image registries, tools and remediation timelines).

## Public framework adaptation
The portable rule file `.bob/rules/02-security-baseline.md` retains broadly applicable principles, but does **not** publish the training verbatim or present its company-specific mandates as universal security requirements. For example, use an approved trusted registry rather than hard-coding one vendor for all projects; allow justified externally bound services behind appropriate network controls; select supported compatible dependencies rather than blindly upgrading everything.

## Proposed diagnostic experiment (NOT YET RUN)
1. Pick an authorized, synthetic demo repository with deliberate non-production issues.
2. Record baseline findings before enabling the security rule.
3. Enable `.bob/rules/02-security-baseline.md` and ask Bob to assess the same repository.
4. Compare detected findings, false positives, actionable remediation and evidence.
5. Ask Developer to implement an approved change and review whether security guidance is applied proactively.
6. Run independent static/dependency scans and unit tests; compare their findings against Bob's output.
7. Publish only anonymized, approved examples and measured results.

## Limitations
Rules guide model behavior but do not replace CI policy gates, scanners, human security review or organization-approved controls. Do not paste company-confidential training materials into public articles.
