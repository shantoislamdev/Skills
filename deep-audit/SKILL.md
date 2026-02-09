---
name: deep-audit
description: Universal security and robustness scanner for any codebase. Use when auditing code for vulnerabilities, security issues, bugs, or robustness problems. Automatically detects tech stack, creates custom audit plans, and performs recursive deep analysis.
---

# Deep Audit

## Phase 1: Discovery

Map the entire codebase. Leave nothing unexplored.

**Actions:**
1. Recursively list all directories and files
2. Identify: languages (by extension), frameworks (by config files), dependencies (by manifests)
3. Locate entry points: main files, route handlers, API endpoints, CLI parsers
4. Map trust boundaries: where external input enters, where data exits

**Output:** Mental model of architecture, data flow, and attack surface.

## Phase 2: Audit Plan

Build a targeted checklist. Prioritize by risk.

| Category | Hunt for |
|----------|----------|
| Injection | Unsanitized input → command execution, query construction, path building, template rendering |
| Auth/AuthZ | Missing checks, weak tokens, session fixation, privilege escalation, IDOR |
| Crypto | Broken algorithms, hardcoded keys, predictable randomness, missing encryption |
| Secrets | Credentials in code, keys in configs, tokens in logs, env vars with defaults |
| Validation | Type confusion, integer overflow, buffer issues, missing bounds checks |
| Errors | Stack traces exposed, debug flags, verbose logging, unhandled exceptions |
| Data | PII in logs, sensitive data unencrypted, insecure deserialization |
| Dependencies | Known CVEs, outdated packages, typosquatting |
| Concurrency | Race conditions, TOCTOU, deadlocks, shared state mutations |
| Logic | Business logic bypasses, state machine violations, trust assumption failures |

**Rank by:** Exploitability × Impact × Exposure

## Phase 3: Deep Analysis

Hunt relentlessly. Every file. Every function. Every input path.

### 3.1 Secrets Scan
Search entire codebase for:
- `password`, `secret`, `api_key`, `token`, `credential`, `auth`
- `-----BEGIN`, `PRIVATE KEY`, `ssh-rsa`
- Base64 blobs (40+ chars), hex strings (32+ chars)
- Connection strings, DSNs, URIs with credentials

**Verify each hit.** False positive? Move on. Real secret? Flag as CRITICAL.

### 3.2 Injection Analysis
Trace every input source to every dangerous sink:
- **Sources:** HTTP params, headers, body, files, env vars, CLI args, database reads, IPC
- **Sinks:** Command execution, SQL/NoSQL queries, file operations, template engines, serializers, network calls

For each source→sink path: Is there sanitization? Is it sufficient? Can it be bypassed?

### 3.3 Auth & Access Control
- Find all endpoints/functions requiring auth. Verify enforcement.
- Check for horizontal privilege escalation (user A accessing user B's data)
- Check for vertical privilege escalation (user becoming admin)
- Look for auth bypasses: default credentials, magic parameters, debug routes

### 3.4 Crypto Review
- List all crypto operations. Verify algorithms are current.
- Check key generation: is randomness cryptographically secure?
- Check key storage: hardcoded? plaintext? properly protected?
- Verify encryption modes (no ECB), proper IV/nonce usage, authenticated encryption

### 3.5 Error & Exception Handling
- Search for exception handlers. Are they too broad? Do they leak info?
- Check HTTP error responses for stack traces, internal paths, versions
- Look for debug/dev mode flags still enabled
- Find logging statements with sensitive data

### 3.6 Dependency Audit
- Extract all dependencies with versions
- Check each against known vulnerability databases
- Flag outdated packages (>1 year without update = suspicious)
- Look for vendored/copied code that may have unpatched vulns

### 3.7 Logic & State
- Identify state machines. Can states be skipped or forced?
- Check financial/critical operations for race conditions
- Verify atomic operations where needed
- Look for time-of-check-time-of-use issues in file/resource access

## Phase 4: Report

No fluff. Facts only.

```markdown
# Security Audit Report

## Executive Summary
- CRITICAL: [count]
- HIGH: [count]
- MEDIUM: [count]
- LOW: [count]

## Findings

### [CRITICAL] Title
**File:** `path/to/file:line`
**Issue:** [One sentence]
**Evidence:**
[Code block]
**Impact:** [What attacker gains]
**Fix:** [Specific remediation]

[Repeat for each finding, highest severity first]

## Attack Scenarios
[2-3 realistic attack chains combining findings]
```

## Rules

**Do not act like typical AI slop.** No lazy pattern matching. No surface-level scanning. No generic findings.

### Bug or Feature?

Before flagging ANYTHING, run this verification:

1. **Context check.** Read surrounding code. Read comments. Read commit history if available.
2. **Intent check.** Could this be deliberate? Is there a security/usability tradeoff being made?
3. **Documentation check.** Is this behavior documented? Is it a known limitation?
4. **Pattern check.** Does similar code exist elsewhere? Is this project's convention?
5. **Edge case check.** Does this only fail under unrealistic conditions?

**Ask yourself:** *Is this really a bug, or am I misunderstanding the design?*

Only flag when you can answer:
- Why this is NOT intentional
- Why existing mitigations (if any) are insufficient
- What realistic attack scenario exploits this

### Core Rules

1. **Verify everything.** Read the actual code. No guessing.
2. **Trace data flow.** Follow inputs to outputs. Miss nothing.
3. **Attack mindset.** What would you exploit? How?
4. **Quality over quantity.** One confirmed vuln > ten maybes.
5. **Precision.** File:line, exact code, specific impact.
6. **Actionable.** Every finding has a concrete fix.
7. **No false positives.** When uncertain, investigate deeper—don't flag.
