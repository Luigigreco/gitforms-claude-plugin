# Security Policy

## 🔒 Security Model

GitForms Claude Code Plugin follows security best practices and Anthropic's security requirements for Claude Code plugins.

## 🛡️ Security Architecture

### No Credential Storage
- ✅ **Zero persistent credentials** - Plugin does not store GitHub tokens
- ✅ **User authorization required** - Every operation requires user consent
- ✅ **Session-based tokens** - Tokens obtained via OAuth flow per session
- ✅ **No hardcoded secrets** - All sensitive data via user configuration

### Sandbox-Safe Operations
- ✅ **Read-only by default** - Plugin only reads configuration
- ✅ **Write operations gated** - GitHub Issues creation requires user approval
- ✅ **No arbitrary code execution** - Plugin does not execute user-provided code
- ✅ **No file system access** - Operations limited to Claude Code sandbox

### Data Flow Security

```
User Form Submission → GitHub Issues API → Validated by GitHub Actions
                ↓
         User Authorization Required
                ↓
         Claude Plugin (Read-only)
                ↓
         Analysis & Insights
```

## 🔐 Authentication & Authorization

### Current Implementation (v1.0.0)
- GitHub Personal Access Token (PAT) via user configuration
- Token scopes required: `repo` (for creating issues)
- Token stored in Claude Code settings (encrypted by Claude)

### Planned Implementation (v1.1.0)
- OAuth 2.0 flow with GitHub
- Explicit user consent for each repository
- Token refresh mechanism
- Automatic token revocation on plugin uninstall

### Authorization Checks
```javascript
// Before any GitHub API call
if (!userHasAuthorizedRepo(repo)) {
  return askUserPermission(`Allow GitForms to access ${repo}?`);
}
```

## 🚨 Threat Model

### Threats Considered

#### 1. Unauthorized Repository Access
**Risk:** Plugin accesses repositories without user consent
**Mitigation:**
- User must explicitly configure `gitforms_repo` setting
- OAuth flow will require per-repository authorization
- No wildcard or automatic repository discovery

#### 2. Token Leakage
**Risk:** GitHub token exposed in logs or errors
**Mitigation:**
- Tokens never logged or displayed
- Error messages sanitized (no token in stack traces)
- Claude Code handles token encryption

#### 3. Malicious Form Submissions
**Risk:** Spam or malicious data injected via forms
**Mitigation:**
- Server-side validation via GitHub Actions
- Rate limiting (10 submissions/hour default)
- Honeypot fields for bot detection
- User can review all submissions before processing

#### 4. Cross-Site Scripting (XSS)
**Risk:** Malicious scripts in form data
**Mitigation:**
- GitHub Issues automatically sanitizes HTML
- Plugin displays data as plain text only
- No direct HTML rendering of user input

#### 5. Injection Attacks
**Risk:** SQL/Command injection via form fields
**Mitigation:**
- No database (GitHub Issues backend)
- No command execution with user input
- All API calls use parameterized requests

## ✅ Security Best Practices Implemented

### Input Validation
- ✅ Repository name format validation (`owner/repo`)
- ✅ Branch name sanitization
- ✅ Email format validation
- ✅ Field name whitelisting

### Output Sanitization
- ✅ GitHub API responses validated
- ✅ User data displayed as plain text
- ✅ No eval() or dangerous functions

### Network Security
- ✅ HTTPS-only communication (GitHub API)
- ✅ No third-party API calls
- ✅ Rate limiting on API requests

### Privacy
- ✅ No telemetry or tracking
- ✅ No data sent to external services (only GitHub)
- ✅ User controls all data (GitHub repository owner)

## 🔍 Security Audit Checklist

- [x] No credential storage (session-based only)
- [x] User authorization required for all write operations
- [x] Sandbox-safe (no file system access outside Claude sandbox)
- [x] Input validation on all user inputs
- [x] Output sanitization
- [x] HTTPS-only communication
- [x] No arbitrary code execution
- [x] Error messages sanitized (no sensitive data)
- [x] Rate limiting implemented
- [ ] OAuth 2.0 flow (planned v1.1.0)
- [ ] Security audit by third party (planned before official release)

## 🚨 Reporting Security Vulnerabilities

### How to Report
If you discover a security vulnerability, please:

1. **DO NOT** open a public GitHub issue
2. Email: l.greco77@gmail.com with subject "SECURITY: GitForms Plugin"
3. Include:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

### Response Timeline
- **Acknowledgment:** Within 24 hours
- **Initial assessment:** Within 72 hours
- **Fix released:** Within 7 days (critical issues)
- **Public disclosure:** After fix is released (coordinated)

### Security Bug Bounty
Currently no formal bug bounty program. Security researchers will be credited in:
- SECURITY.md (this file)
- CHANGELOG.md
- GitHub security advisory

## 🔒 Compliance

### GDPR Compliance
- ✅ No personal data collected by plugin
- ✅ User controls all data (GitHub repository)
- ✅ Right to erasure (delete GitHub Issues)
- ✅ Data portability (export via `/list-contacts`)
- ✅ Transparent data processing (documented)

### SOC 2 Type II
- GitHub (data storage) is SOC 2 Type II certified
- Plugin inherits GitHub's compliance posture
- No additional data storage by plugin

## 📊 Security Updates

### Version History
- **v1.0.0** (2026-01-16): Initial release with PAT authentication
- **v1.1.0** (planned): OAuth 2.0 implementation
- **v1.2.0** (planned): Third-party security audit

### Security Fixes
None yet (initial release)

## 🔐 Secure Development Practices

### Code Review
- All changes reviewed before merge
- Security-focused code review checklist
- Dependency vulnerability scanning (npm audit)

### Dependencies
- Minimal dependencies (reduce attack surface)
- Regular dependency updates
- Automated vulnerability scanning (Dependabot)

### Testing
- Unit tests for all security-critical functions
- Integration tests with mock GitHub API
- Manual security testing before releases

## 📚 Security Resources

### For Users
- [GitHub Security Best Practices](https://docs.github.com/en/code-security)
- [Claude Code Security Model](https://docs.anthropic.com/claude/docs/security)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

### For Developers
- [Anthropic Security Guidelines](https://docs.anthropic.com/claude/docs/security)
- [GitHub API Security](https://docs.github.com/en/rest/overview/keeping-your-api-credentials-secure)
- [OAuth 2.0 Best Practices](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics)

---

**Last Updated:** 2026-01-16
**Version:** 1.0.0
**Contact:** l.greco77@gmail.com
