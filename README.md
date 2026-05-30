# legal-ai-incident-card-profile

> **LegalTech Incident Card — Spec #5 of the LegalTech 6-pack.** Profile of the [AI Incident Card spec](https://github.com/mizcausevic-dev/incident-card-spec) scoped to legal-AI incidents at law firms, in-house legal departments, public defenders, and legal-AI vendors. Covers privilege breaches, work-product doctrine violations, Mata v. Avianca-class court-sanctioned hallucinations, conflict-check bypasses, UPL violations, and AI vendor training-data-use violations.

Part of the [Kinetic Gain Protocol Suite](https://suite.kineticgain.com).

> Status: v0.1 draft. Profile at [`profile.json`](./profile.json).

## What this profile is

A **structured incident-record format** signed by the supervising attorney, sufficient for the firm's General Counsel, Managing Partner, outside ethics counsel, state bar disciplinary counsel, and (where required) the affected tribunal to triage and respond.

**18 event types** covering the full surface where a legal AI tool can produce a reportable incident:

- privileged-disclosure-to-unauthorized-recipient
- work-product-doctrine-violation
- cross-matter-information-leak
- conflict-check-bypass
- engagement-letter-out-of-scope-action
- **court-sanctioned-hallucination-class** (Mata v. Avianca)
- bar-discipline-trigger
- unauthorized-practice-of-law
- attorney-supervisor-bypass
- client-deepfake-impersonation-attempt
- ai-vendor-training-data-use-violation
- privilege-log-incomplete-due-to-ai-tagging
- ediscovery-tar-coding-error-systematic
- ediscovery-spoliation-by-ai-retention-policy
- bar-association-investigation-opened
- court-standing-order-violation
- billing-misconduct-ai-time-fraud
- cross-border-data-residency-violation

**4 severities** (S1-low → S4-critical), each with named escalation pathways.

**10 referral pathways** including LegalTech-distinctive: outside ethics counsel engagement, state bar disciplinary counsel notification, court disclosure (where the AI incident reached a tribunal), professional liability insurer notification, criminal-defense effective-assistance disclosure.

## LegalTech-distinctive design

**Privilege waiver risk taxonomy (6 codes)** — `no-privilege-risk-applicable` → `low-vendor-channel-only` → `moderate-third-party-but-recoverable` (Fed. R. Evid. 502(d) clawback) → `high-waiver-likely` → `critical-cross-matter-or-subject-matter`. No sibling-vertical Incident Card has anything like this — privilege waiver mechanics are unique to LegalTech. Filing an Incident Card without a privilege-waiver-risk assessment is malpractice-adjacent.

**Signature REQUIRED, not optional.** Most sibling-vertical Incident Cards make the ed25519 signature optional. LegalTech requires it because Incident Cards reach state bar disciplinary counsel + tribunals — there has to be an attesting attorney whose name is on the line, and the signature establishes that the card was issued by them and not retroactively altered.

**Criminal-defense effective-assistance disclosure pathway.** Triggered when the affected matter is criminal defense AND severity ≥ S2-moderate. Surfaces a Sixth Amendment obligation no sibling vertical has — the *defendant* (and any appellate counsel) need to know an AI tool was implicated in a moderate-or-higher incident on their matter.

**Court disclosure pathway** as a first-class referral channel — for `court-sanctioned-hallucination-class` and `court-standing-order-violation`. The incident isn't fully addressed until the affected tribunal has been notified.

## Use

```bash
# Validate the profile is well-formed
node -e "JSON.parse(require('fs').readFileSync('profile.json','utf8'))"
```

## What this is NOT

- Not a bar discipline outcome — documents the incident; the bar's separate process determines discipline.
- Not a malpractice waiver — filing does not waive defenses the firm may have.
- Not itself privilege-waiving — filing should be done with privilege-preservation review.

## Composes with

- [`incident-card-spec`](https://github.com/mizcausevic-dev/incident-card-spec) — the upstream spec this profile conforms to
- [`matter-decision-record-audit-stream`](https://github.com/mizcausevic-dev/matter-decision-record-audit-stream) — emits `legaltech_ai_incident.filed` / `.remediated` / `.regulator_referred` / `.court_disclosed` / `.client_notified` events
- [`aba-rule-1-6-readiness-evidence-bundle`](https://github.com/mizcausevic-dev/aba-rule-1-6-readiness-evidence-bundle) — sibling compliance Evidence Bundle
- [`legal-applicant-bias-coverage-lab`](https://github.com/mizcausevic-dev/legal-applicant-bias-coverage-lab) — sibling bias Evidence Bundle
- [`state-bar-ai-disclosure-tracker`](https://github.com/mizcausevic-dev/state-bar-ai-disclosure-tracker) — sibling state-bar lifecycle tracker
- [Kinetic Gain Protocol Suite](https://suite.kineticgain.com) — umbrella

## Compliance posture

**Incident-readiness scaffolding** for law firms + legal-AI vendors. Card format does not establish bar compliance, does not waive privilege, does not constitute discipline. Per the standing public-language guardrail across the Suite.

## License

Profile + supporting documentation: MIT.
