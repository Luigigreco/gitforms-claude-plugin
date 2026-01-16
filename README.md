# GitForms Claude Code Plugin

**Zero-cost contact forms using GitHub Issues as database.**

Transform GitHub Issues into a powerful form backend without any infrastructure. Create forms, track leads, and analyze submissions directly from Claude Code.

## Features

- 🆓 **Zero Cost** - No backend, no servers, just GitHub
- ⚡ **Instant Setup** - 2-minute deployment
- 🤖 **AI-Powered** - Natural language form management
- 📊 **Smart Analytics** - Lead scoring and trend analysis
- 🔒 **Secure** - Server-side validation, spam protection
- 📈 **Scalable** - Handle thousands of submissions

## Quick Start

### Installation

```bash
/plugin install gitforms
```

### Configuration

```bash
/settings gitforms_repo owner/repo-name
```

### Create Your First Form

```bash
/create-form contact name,email,message
```

That's it! Your form is ready to accept submissions.

## Commands

### `/create-form` - Create New Form

Generate a complete HTML form with validation, spam protection, and automated workflows.

```bash
# Basic contact form
/create-form contact-form name,email,message

# Lead capture with qualification
/create-form lead-capture name,email,company,budget,timeline

# Event registration
/create-form event-registration name,email,company,attendees
```

**What it creates:**
- HTML form markup
- GitHub Issues backend
- Spam protection (honeypot + rate limiting)
- Automated workflows
- Email notifications

### `/list-contacts` - Manage Submissions

Retrieve, filter, and export form submissions.

```bash
# All contacts
/list-contacts

# Filter by label
/list-contacts --label lead

# Filter by date
/list-contacts --since 2025-01-01
/list-contacts --last 7d

# Export to CSV
/list-contacts --format csv --output leads.csv

# Batch operations
/list-contacts --label spam --action delete
```

**Output formats:**
- Table (default)
- CSV (for CRM import)
- JSON (for analytics)

### `/analyze-leads` - AI-Powered Insights

Get actionable insights from your form submissions.

```bash
# Quick summary
/analyze-leads

# Full analysis
/analyze-leads --report full

# Trend analysis
/analyze-leads --report trends --period 30d
```

**Analysis includes:**
- Lead quality scoring (0-10)
- Conversion pattern detection
- Time-series trends
- Actionable recommendations

## Natural Language Interface

You can also use natural language instead of commands:

```
"Create a contact form with name and email"
"Show me all leads from this week"
"Analyze my form submissions"
"Export high-value leads to CSV"
```

The `gitforms-assistant` skill activates automatically when you mention forms or contacts.

## How It Works

1. **Form Submission** → User fills form on your website
2. **GitHub Issue Created** → Submission saved as GitHub Issue with labels
3. **Automated Processing** → GitHub Actions validate and categorize
4. **AI Analysis** → Claude analyzes patterns and quality
5. **Actionable Insights** → Get recommendations for follow-up

## Integration Examples

### Static HTML

```html
<form action="https://gitforms.io/submit/yourname/contact-repo" method="POST">
  <input type="text" name="name" required>
  <input type="email" name="email" required>
  <textarea name="message" required></textarea>
  <button type="submit">Submit</button>
</form>
```

### React Component

```jsx
import { GitForm } from '@gitforms/react'

function ContactForm() {
  return (
    <GitForm
      repo="yourname/contact-repo"
      fields={['name', 'email', 'message']}
      onSuccess={() => alert('Thanks!')}
    />
  )
}
```

### Direct API

```javascript
fetch('https://gitforms.io/submit/yourname/contact-repo', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name, email, message })
})
```

## Advanced Features

### Multi-Step Forms

```bash
/create-form onboarding --multi-step \
  "Step1:name,email|Step2:company,role|Step3:goals"
```

### Conditional Fields

```bash
/create-form quote --conditional \
  "Service→If 'Enterprise'→Team Size,Budget"
```

### File Uploads

```bash
/create-form application name,email,resume \
  --upload resume:pdf,doc --max-size 5MB
```

### Webhooks

```bash
/create-form contact name,email \
  --webhook https://your-api.com/notify \
  --webhook-secret your_secret
```

## Security

- ✅ Server-side validation via GitHub Actions
- ✅ Rate limiting (10 submissions/hour default)
- ✅ Honeypot fields for spam detection
- ✅ CORS whitelist configuration
- ✅ GitHub Secrets for sensitive config
- ✅ No credential storage (user authorization required)

## Pricing

| Tier | Price | Submissions | Features |
|------|-------|-------------|----------|
| **Free** | $0 | 1,000/month | Unlimited forms, basic spam protection |
| **Pro** | $9/month | 10,000/month | Advanced spam, priority support, custom branding |
| **Enterprise** | Custom | Unlimited | SLA, dedicated support, custom integrations |

## Documentation

- [QUICKSTART.md](QUICKSTART.md) - 5-minute setup guide
- [EXAMPLES.md](EXAMPLES.md) - Real-world usage examples
- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - Common issues and solutions
- [CHANGELOG.md](CHANGELOG.md) - Version history

## Use Cases

- **Startups** - Contact forms without backend costs
- **Freelancers** - Client lead capture
- **SaaS** - Free tier product waitlist
- **Events** - Registration forms
- **Agencies** - Multi-client form management
- **Side Projects** - Zero-cost infrastructure

## Requirements

- Claude Code v1.0+
- GitHub account with repo access
- GitHub Actions enabled on target repository

## Installation

### From Marketplace
```bash
/plugin install gitforms
```

### From GitHub
```bash
/plugin add Luigigreco/gitforms-claude-plugin
/plugin install gitforms
```

## Configuration

Required settings:
```bash
/settings gitforms_repo owner/repo-name
```

Optional settings:
```bash
/settings gitforms_branch main  # Default branch
```

## Support

- **Issues:** https://github.com/Luigigreco/gitforms-claude-plugin/issues
- **Discussions:** https://github.com/Luigigreco/gitforms-claude-plugin/discussions
- **Email:** l.greco77@gmail.com

## Roadmap

- [x] Basic form creation
- [x] Contact management
- [x] AI-powered analytics
- [ ] OAuth flow implementation
- [ ] SECURITY.md and PRIVACY.md
- [ ] Official Anthropic marketplace submission
- [ ] CRM integrations (Salesforce, HubSpot)
- [ ] A/B testing support
- [ ] Mobile app

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - see [LICENSE](LICENSE) for details.

## Author

**Luigi Greco**
- Email: l.greco77@gmail.com
- GitHub: [@Luigigreco](https://github.com/Luigigreco)
- Original Project: [GitForms](https://github.com/Luigigreco/gitforms)

---

**Transform GitHub Issues into a powerful form backend. Zero cost. Zero infrastructure. Maximum flexibility.**
