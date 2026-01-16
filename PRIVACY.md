# Privacy Policy

**Effective Date:** January 16, 2026
**Version:** 1.0.0

## 📋 Overview

GitForms Claude Code Plugin ("the Plugin") is designed with privacy as a core principle. This document explains how the Plugin handles data and protects user privacy.

## 🎯 Key Privacy Principles

1. **No Data Collection** - Plugin does not collect, store, or transmit user data to any service except GitHub
2. **User Control** - All data is stored in user's GitHub repository (user has full control)
3. **Transparency** - All data flows are documented and visible
4. **Minimal Access** - Plugin only requests necessary permissions

## 📊 Data Handling

### What Data Does the Plugin Access?

#### User-Provided Configuration
- **GitHub Repository Name** (`gitforms_repo` setting)
  - Purpose: Target repository for form submissions
  - Storage: Claude Code settings (local, encrypted)
  - Retention: Until user changes/removes setting

- **Branch Name** (`gitforms_branch` setting, optional)
  - Purpose: Specify branch for submissions
  - Storage: Claude Code settings (local, encrypted)
  - Retention: Until user changes/removes setting

#### Form Submission Data (Read-Only)
- **GitHub Issues Content**
  - Purpose: Display form submissions to user
  - Storage: GitHub (user's repository)
  - Access: Read-only via GitHub API
  - Retention: Controlled by user (GitHub Issues retention policy)

### What Data Does the Plugin NOT Access?

- ❌ GitHub repository code
- ❌ Private repositories (unless explicitly configured)
- ❌ User's email or personal information (beyond what's in GitHub Issues)
- ❌ Other Claude Code plugins or settings
- ❌ File system outside Claude sandbox

## 🔒 Data Storage

### Local Storage (Claude Code)
- **Configuration settings** (`gitforms_repo`, `gitforms_branch`)
- **Storage location:** Claude Code settings database (encrypted)
- **Encryption:** Handled by Claude Code platform
- **Access:** Only the Plugin and user

### External Storage (GitHub)
- **Form submissions** (GitHub Issues)
- **Storage location:** User's GitHub repository
- **Access control:** Controlled by user (GitHub permissions)
- **Retention:** Controlled by user

### No Third-Party Storage
- ✅ Plugin does not send data to any server except GitHub API
- ✅ No analytics or telemetry collected
- ✅ No tracking cookies
- ✅ No external databases

## 🌐 Data Transmission

### GitHub API Communication
- **Protocol:** HTTPS only (encrypted in transit)
- **Authentication:** GitHub Personal Access Token (user-provided)
- **Endpoints used:**
  - `GET /repos/{owner}/{repo}/issues` - Read form submissions
  - `POST /repos/{owner}/{repo}/issues` - Create issues (via form submission, not by plugin directly)
- **Data sent:** Repository name, query parameters
- **Data received:** GitHub Issues content (form submissions)

### No Other External Communication
- ✅ No calls to analytics services
- ✅ No calls to advertising networks
- ✅ No calls to external APIs (except GitHub)

## 👤 User Rights (GDPR Compliance)

### Right to Access
Users can access all their data via:
```bash
/list-contacts --format json
```
This exports all form submissions in JSON format.

### Right to Erasure
Users can delete data by:
1. **Individual submissions:** Close/delete GitHub Issues
2. **All data:** Delete GitHub repository or remove issues
3. **Plugin configuration:** `/settings delete gitforms_repo`

### Right to Data Portability
Users can export data in multiple formats:
```bash
/list-contacts --format csv --output leads.csv
/list-contacts --format json --output leads.json
```

### Right to Rectification
Users can modify data directly in GitHub Issues.

### Right to Restriction of Processing
Users can:
- Remove plugin: `/plugin uninstall gitforms`
- Revoke GitHub token access
- Change repository to private (restrict access)

## 🔐 Privacy by Design

### Minimal Data Collection
- Plugin only accesses data explicitly needed for functionality
- No "just in case" data collection
- No profiling or behavioral tracking

### User Consent
- User must explicitly configure repository (`gitforms_repo`)
- No automatic data access
- OAuth flow (planned v1.1.0) requires explicit per-repository consent

### Data Minimization
- Only form submission data accessed (name, email, message fields)
- No access to repository code or other GitHub data
- Queries limited to configured repository only

## 📍 Data Location

### GitHub Data Centers
- Form submissions stored in GitHub's infrastructure
- GitHub is SOC 2 Type II certified
- See [GitHub Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement)

### Local Data
- Plugin configuration stored locally (Claude Code settings)
- No cloud synchronization by plugin

## 👨‍💻 Third-Party Services

### GitHub (Required)
- **Purpose:** Store form submissions as GitHub Issues
- **Data shared:** Repository name, query parameters
- **Privacy policy:** https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement
- **User relationship:** User has direct account with GitHub

### Claude Code (Platform)
- **Purpose:** Plugin runtime environment
- **Data shared:** Plugin configuration (encrypted)
- **Privacy policy:** https://www.anthropic.com/privacy
- **User relationship:** User has direct account with Anthropic

### No Other Third Parties
- ✅ No analytics services (Google Analytics, etc.)
- ✅ No advertising networks
- ✅ No CDNs or external assets
- ✅ No payment processors (free plugin)

## 🧒 Children's Privacy

Plugin is not directed at children under 13. We do not knowingly collect data from children. If you are a parent and believe your child has used this plugin, please contact us.

## 🌍 International Data Transfers

- Form data stored in GitHub (user's GitHub account region)
- Plugin configuration stored locally (no cross-border transfer)
- GitHub may transfer data internationally (see GitHub Privacy Statement)

## 🔔 Privacy Policy Changes

### How We Notify Users
- Updates published to this PRIVACY.md file
- Version number updated
- Major changes announced in CHANGELOG.md
- GitHub repository watchers notified via commit

### User Action Required
- No action required for minor clarifications
- Major changes: Users should review updated policy

## 📧 Contact Information

### Privacy Questions
**Email:** luigi.greco@proton.me
**Subject:** "PRIVACY: GitForms Plugin"

### Data Subject Requests
For GDPR/privacy requests (access, deletion, correction):
1. Email luigi.greco@proton.me
2. Include: Request type, repository name, timeline
3. Response within 30 days

### Plugin Maintainer
**Name:** Luigi Greco
**GitHub:** [@Luigigreco](https://github.com/Luigigreco)
**Repository:** https://github.com/Luigigreco/gitforms-claude-plugin

## 📊 Privacy Summary (TL;DR)

✅ **We DO:**
- Store configuration locally (encrypted by Claude Code)
- Access GitHub Issues in your configured repository
- Transmit data over HTTPS to GitHub API only

❌ **We DON'T:**
- Collect analytics or telemetry
- Send data to third parties (except GitHub)
- Store your GitHub token (handled by Claude Code)
- Track your behavior
- Sell or share your data

🔒 **Your Control:**
- You own all data (stored in your GitHub repository)
- You can export data anytime
- You can delete data anytime
- You can uninstall plugin anytime

## 🔗 Related Documents

- [SECURITY.md](SECURITY.md) - Security practices and threat model
- [README.md](README.md) - Plugin functionality and features
- [CHANGELOG.md](CHANGELOG.md) - Version history and updates

---

**Last Updated:** 2026-01-16
**Version:** 1.0.0
**Contact:** luigi.greco@proton.me

**This privacy policy complies with:**
- GDPR (General Data Protection Regulation)
- CCPA (California Consumer Privacy Act)
- Anthropic Claude Code Plugin Guidelines
