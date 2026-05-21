# FeedMe Security Engineer Take-Home Assignment

## Overview

You are applying for a Security Engineering role focused on internal information security and security operations.

This assignment is designed to evaluate how you think through real-world security incidents, prioritize under uncertainty, communicate risk, and design practical controls that can work inside a fast-moving company.

This is not a trivia test. We are more interested in your reasoning, tradeoffs, and ability to operate calmly during messy situations.

---

## Timebox

Please spend no more than **60 minutes** on this assignment.

You only need to complete **one task** from the three options below, unless instructed otherwise by the interviewer.

---

## Expected Submission Format

Please submit your answer in a clear written format.

**Recommended length:** 2–4 pages maximum

You may use:

- Bullet points
- Tables
- Simple diagrams
- Pseudocode
- Bash, Python, JavaScript, or CLI commands where useful

It is okay if you do not have all the information. Clearly separate:

- What you know
- What you assume
- What you would verify next
- What decision you would make based on available evidence

---

## Task 1: Secrets Leak, But Don't Panic

### Scenario

You are the security engineer on call.

A developer accidentally committed a `.env.production` file into a private GitHub repository.

The repository is private, but it is accessible by:

- 38 internal engineers
- 3 external contractors
- CI/CD runners
- Several GitHub Actions workflows

The file may contain:

- Production database credentials
- API keys
- Third-party payment provider secrets
- Internal admin tokens

The developer removed the file from the latest commit, but the secret may still exist in:

- Git history
- CI logs
- Forks
- Local clones
- Build artifacts
- Developer machines

### Your Deliverables

#### 1. Incident Assessment

Explain how you would assess the incident.

Cover:

- What likely happened?
- What is the possible business impact?
- Which systems, secrets, users, or environments may be affected?
- What assumptions are you making?
- What severity would you assign and why?

#### 2. First 60-Minute Response Plan

Describe what you would do in the first hour.

Cover:

- What would you check first?
- What would you contain immediately?
- Who would you involve?
- What actions would you avoid taking too early?
- What information would you collect before making bigger decisions?

#### 3. Containment and Recovery

Explain your recovery approach.

Cover:

- Which credentials should be rotated?
- In what order would you rotate them?
- How would you reduce risk without breaking production?
- How would you confirm the old credentials are no longer usable?
- What evidence should be preserved?

#### 4. Detection and Investigation

Explain how you would investigate possible misuse.

Cover:

- Which logs would you review?
- Where would you search for evidence of exposure?
- What indicators would suggest the secret was abused?
- What indicators would reduce your concern?
- How would you build a timeline?

#### 5. Script

Write a script or command that supports your response to this incident.

Cover:

- What is the purpose of this script? What problem does it solve?
- What does it check, scan, or automate?
- When and by whom would it be run?

Your script may:

- Scan git history for the leaked file or known secret patterns
- List all repository collaborators and their access levels
- Check CI/CD logs for secret exposure
- Verify that old credentials are no longer accepted

You may use Bash, Python, or CLI commands. You do not need a production-grade tool — we want to see practical triage thinking.

#### 6. Prevention

Recommend practical improvements.

Cover:

- How would you prevent secrets from being committed again?
- What should be added to CI/CD?
- What should be added to developer workflow?
- How would you make the secure path easy for engineers?

---

## Task 2: Compromised npm Package / Supply Chain Attack

### Scenario

You are the security engineer supporting a company that uses Node.js services across internal tools and production systems.

Security news reports that a widely used npm package has been compromised.

In the referenced Axios incident, attackers reportedly used stolen npm credentials to publish malicious Axios versions. The malicious package included a phantom dependency and used a `postinstall` hook to execute malware during package installation.

The company wants to know:

- Are we affected?
- Did any developer machine or CI runner execute the malicious package?
- Could production be impacted?
- What should we do immediately?
- How do we prevent this class of attack in the future?

### Your Deliverables

#### 1. Risk Assessment

Explain how you would assess the risk.

Cover:

- What is the possible business impact?
- Which systems are most at risk?
- What assumptions are you making?
- What would make this incident high severity?
- What would make it lower severity?
- What evidence would you need before escalating?

#### 2. Script or Command to Run

Provide a simple script, command, or pseudocode that helps identify whether the company is affected.

You must also explain the purpose of your script:

- What problem does it solve?
- What does it check or detect?
- When would you run it and who would run it?

Your script may check:

- `package.json`
- `package-lock.json`
- `yarn.lock`
- `pnpm-lock.yaml`
- `node_modules`
- CI logs
- Package install scripts
- Suspicious transitive dependencies
- Known indicators of compromise
- Suspicious `postinstall` behavior

You do not need to write a perfect production-grade tool. We want to see how you would quickly create something useful for triage.

#### 3. Monitoring Plan

Define what you would monitor for the next 24–72 hours.

Cover:

- CI/CD logs
- Developer endpoint telemetry
- DNS and network egress
- Package installation activity
- GitHub or GitLab audit logs
- Cloud credential usage
- Suspicious process execution from `node`, `npm`, `yarn`, `pnpm`, or CI runners

#### 4. Containment and Recovery

Explain how you would contain and recover.

Cover:

- What should be isolated or rebuilt?
- When would you rotate secrets?
- How would you handle developer laptops?
- How would you handle CI runners?
- How would you confirm production was not affected?
- What would you communicate to engineering?

#### 5. Prevention

Recommend practical long-term controls.

Examples:

- Lockfile enforcement
- Exact dependency pinning
- `npm ci --ignore-scripts` where appropriate
- Dependency review in pull requests
- Private package proxy or registry allowlist
- CI egress restrictions
- Software composition analysis
- Alerting on new install scripts
- Alerting on unexpected transitive dependencies
- Stronger npm publisher account protection

---

## Task 3: Internal Security Fire Drill

### Scenario

You are the security engineer on call.

On Thursday night, a finance team member received a WhatsApp message containing a file named:

```
Account Statement.zip
```

Inside the ZIP file was:

```
Account Statement.exe
```

The finance team member opened the `.exe`.

On Friday morning, the finance team member reported that their WhatsApp account was automatically forwarding the same ZIP file to all contacts.

Within the 30 minutes before the finance member notified the security team, two other staff members also clicked and opened the file.

You are responsible for handling the incident.

### Your Deliverables

#### 1. Incident Assessment

Explain your initial assessment.

Cover:

- What is the likely incident?
- What systems, users, and data may be affected?
- What is the initial severity?
- What assumptions are you making?
- What information do you need to confirm quickly?
- What would make this incident worse?

#### 2. First 60-Minute Response Plan

Describe your first-hour response.

Cover:

- What would you check first?
- Which users or devices would you prioritize?
- Who would you contact?
- What actions would you take immediately?
- What would you avoid doing too early?
- How would you prevent more employees from clicking the file?

#### 3. Containment and Recovery

Explain how you would contain and recover.

Cover:

- Infected endpoint isolation
- WhatsApp account protection
- Password and session reset
- MFA review
- Endpoint malware scan or reimage
- Evidence preservation
- Internal communication
- Business continuity considerations
- Criteria for returning devices or accounts to normal use

#### 4. Detection and Logging Improvement

Propose improvements to detect similar incidents earlier.

Cover:

- Endpoint detection signals
- Suspicious process execution
- ZIP or executable file activity
- Unusual WhatsApp Web or browser session activity
- Identity login anomalies
- Network egress indicators
- Centralized logging gaps
- Alerts you would create after this incident

#### 5. Script

Write a script or command that supports your response to this incident.

Cover:

- What is the purpose of this script? What problem does it solve?
- What does it check, scan, or automate?
- When and by whom would it be run?

Your script may:

- Search for the malicious file hash across connected drives or shared storage
- List active WhatsApp Web sessions across known devices
- Query endpoint logs for execution of the suspicious `.exe`
- Identify which users received or forwarded the ZIP file
- Check for outbound network connections from affected machines

You may use Bash, Python, or CLI commands. You do not need a production-grade tool — we want to see practical triage thinking.

#### 6. Operational Prevention

Recommend practical prevention measures.

Examples:

- Employee malware awareness
- Finance-team-specific security training
- Blocking or warning on executable files from messaging apps
- Endpoint protection policy
- Application allowlisting
- Device compliance checks
- Local admin restriction
- WhatsApp Web usage policy
- Incident reporting playbook
- Faster internal alerting process

#### 7. Communication

Write two short messages.

**A. Internal Engineering / IT Update**

Audience: engineering, IT, or security operations.

Your message should include:

- What happened
- What action is being taken
- What help is needed
- What not to do
- Any immediate technical requests

**B. Company-Wide Staff Warning**

Audience: all employees.

Your message should include:

- Warning not to open the file
- The filename to look for
- What to do if they clicked it
- Who to contact
- A calm, clear, non-blaming tone

