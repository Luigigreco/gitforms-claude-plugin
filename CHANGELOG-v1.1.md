# Changelog

All notable changes to GitForms Claude Code Plugin will be documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-01-16 (Preparation for Official Submission)

### Added
- **SECURITY.md** - Comprehensive security policy and threat model
- **PRIVACY.md** - Privacy policy with GDPR compliance details
- Enhanced README with detailed installation instructions
- Verification documentation for plugin structure

### Changed
- Updated documentation for official Anthropic marketplace submission
- Improved installation instructions with multiple methods

### Security
- Documented security architecture and threat model
- Outlined OAuth 2.0 implementation plan (v1.2.0)
- Added security vulnerability reporting process
- Defined GDPR compliance measures

### Privacy
- Documented data handling practices
- Clarified user data rights (access, deletion, portability)
- Confirmed zero third-party data sharing
- Added privacy-by-design principles

### Planned for v1.2.0 (Official Marketplace Release)
- OAuth 2.0 flow implementation
- MCP wrapper for protocol consistency
- Third-party security audit
- Enhanced token management

## [1.0.0] - 2026-01-16 (Community Plugin Release)

### Added
- Initial release of GitForms Claude Code Plugin
- `/create-form` command for generating contact forms
- `/list-contacts` command for managing submissions
- `/analyze-leads` command for AI-powered lead analysis
- `gitforms-assistant` skill for natural language interaction
- Support for GitHub Issues as form backend
- Automated spam protection with honeypot fields
- Rate limiting (10 submissions/hour default)
- CSV/JSON export functionality
- Lead quality scoring algorithm
- Conversion pattern analysis
- Trend tracking and visualization
- Webhook integration support
- Multi-step form support
- Conditional field logic
- File upload capabilities
- Email notification system
- GitHub Actions workflow automation
- Comprehensive documentation (README, QUICKSTART, EXAMPLES, TROUBLESHOOTING)

### Configuration
- `gitforms_repo` - Target repository for submissions
- `gitforms_branch` - Branch for form data (default: main)

### Pricing
- Free tier: Unlimited forms, 1000 submissions/month
- Pro tier: $9/month, 10k submissions/month
- Enterprise: Custom pricing for high-volume

### Known Issues
- MCP GitHub tool may require authentication refresh
- Large contact lists (>1000) may have pagination delays
- File uploads limited to 5MB per file

### Security
- Server-side validation via GitHub Actions
- CORS whitelist configuration
- GitHub Secrets for sensitive data
- No credential storage (user authorization required)
- Sandbox-safe operations only

### Dependencies
- Claude Code v1.0+
- GitHub account with repo access
- GitHub Actions enabled on target repo

## [Unreleased]

### Planned for v1.2.0 (Official Marketplace)
- OAuth 2.0 flow implementation (replace PAT)
- MCP protocol wrapper
- Advanced analytics dashboard
- CRM integration (Salesforce, HubSpot)
- A/B testing support
- Custom branding removal (Pro tier)
- Multi-language form support
- Real-time submission notifications
- Advanced spam detection with ML
- Third-party security audit report

### Future Considerations (v2.0+)
- Mobile app for form management
- Zapier integration
- Slack notifications
- Discord webhooks
- GDPR compliance tools (enhanced)
- Data retention policies
- Form templates library
- Visual form builder
- White-label solution (Enterprise)
- Self-hosted option

---

**Installation:** `/plugin add Luigigreco/gitforms-claude-plugin`
**Repository:** https://github.com/Luigigreco/gitforms-claude-plugin
**Issues:** https://github.com/Luigigreco/gitforms-claude-plugin/issues
**Author:** Luigi Greco (l.greco77@gmail.com)

**Submission Status:**
- ✅ v1.0.0 - Community Plugin (LIVE)
- 📋 v1.1.0 - Security & Privacy Documentation (READY)
- ⏳ v1.2.0 - Official Anthropic Marketplace (IN PROGRESS)
