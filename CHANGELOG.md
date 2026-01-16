# Changelog

All notable changes to GitForms Claude Code Plugin will be documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-16

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

### Planned for v1.1.0
- OAuth flow implementation
- SECURITY.md and PRIVACY.md for Anthropic submission
- MCP wrapper for official marketplace
- Advanced analytics dashboard
- CRM integration (Salesforce, HubSpot)
- A/B testing support
- Custom branding removal (Pro tier)
- Multi-language form support
- Real-time submission notifications
- Advanced spam detection with ML

### Future Considerations
- Mobile app for form management
- Zapier integration
- Slack notifications
- Discord webhooks
- GDPR compliance tools
- Data retention policies
- Form templates library
- Visual form builder

---

**Installation:** `/plugin install gitforms`
**Repository:** https://github.com/Luigigreco/gitforms-claude-plugin
**Issues:** https://github.com/Luigigreco/gitforms-claude-plugin/issues
**Author:** Luigi Greco (l.greco77@gmail.com)
