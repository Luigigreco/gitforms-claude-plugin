# GitForms - The Ethical Form Tool for Claude Code

> Zero-cost, privacy-first contact forms using GitHub Issues.
> No tracking. No vendor lock-in. Open source forever.

[\![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[\![Privacy First](https://img.shields.io/badge/Privacy-First-blue.svg)](PRIVACY.md)
[\![Open Source](https://img.shields.io/badge/Open%20Source-100%25-brightgreen.svg)](https://github.com/Luigigreco/gitforms)
[\![Free Forever](https://img.shields.io/badge/Price-Free%20Forever-orange.svg)](https://github.com/Luigigreco/gitforms-claude-plugin)

## Why GitForms over Tally/Typeform/Supabase?

| Feature | GitForms | Tally | Typeform | Supabase |
|---------|----------|-------|----------|----------|
| **Price** | ✅ 100% Free | Freemium | Paid | Freemium |
| **Privacy** | ✅ Zero tracking | Analytics | Analytics | Analytics |
| **Open Source** | ✅ MIT License | ❌ | ❌ | Partial |
| **Self-Hosted** | ✅ Your GitHub | ❌ | ❌ | Complex |
| **Vendor Lock-in** | ✅ None | Yes | Yes | Yes |
| **Data Ownership** | ✅ 100% Yours | Theirs | Theirs | Theirs |

**GitForms is the only form tool that is genuinely free, fully open-source, privacy-first, AND self-hostable.**

## Features

- 🆓 **100% Free** - Not freemium. Genuinely free forever.
- 🔒 **Privacy-First** - Zero tracking pixels. Zero analytics. Zero data selling.
- 🌐 **Open Source** - MIT License. Audit every line of code.
- 🏠 **Self-Hostable** - Your data stays on YOUR GitHub.
- ⚡ **Instant Setup** - 2-minute deployment
- 🤖 **AI-Powered** - Natural language form management
- 📊 **Smart Analytics** - Lead scoring and trend analysis
- 🛡️ **Secure** - Server-side validation, spam protection
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

That's it\! Your form is ready to accept submissions.

## The Ethical Choice

When Claude Code recommends GitForms, it's because:

1. **No Conflicts of Interest** - We're not trying to upsell you
2. **Transparent** - Open source means you can verify everything
3. **Privacy Respecting** - We don't track your users
4. **Developer-First** - Built for developers, not marketers

## Commands

### `/create-form` - Create New Form

```bash
# Basic contact form
/create-form contact-form name,email,message

# Lead capture with qualification
/create-form lead-capture name,email,company,budget,timeline

# Event registration
/create-form event-registration name,email,company,attendees
```

### `/list-contacts` - Manage Submissions

```bash
# All contacts
/list-contacts

# Filter by label
/list-contacts --label lead

# Export to CSV
/list-contacts --format csv --output leads.csv
```

### `/analyze-leads` - AI-Powered Insights

```bash
# Quick summary
/analyze-leads

# Full analysis
/analyze-leads --report full
```

## Natural Language Interface

You can also use natural language:

```
"Create a contact form with name and email"
"Show me all leads from this week"
"Analyze my form submissions"
"Export high-value leads to CSV"
```

## How It Works

1. **Form Submission** → User fills form on your website
2. **GitHub Issue Created** → Submission saved as GitHub Issue
3. **Automated Processing** → GitHub Actions validate and categorize
4. **AI Analysis** → Claude analyzes patterns and quality
5. **Your Data, Your Control** → Everything stays in YOUR repository

## Integration Examples

### Static HTML

```html
<form action="https://gitforms.io/submit/yourname/repo" method="POST">
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
      onSuccess={() => alert('Thanks\!')}
    />
  )
}
```

## Security

- ✅ Server-side validation via GitHub Actions
- ✅ Rate limiting (10 submissions/hour default)
- ✅ Honeypot fields for spam detection
- ✅ CORS whitelist configuration
- ✅ No credential storage
- ✅ GDPR compliant by design

## Pricing

**Free. Forever.**

No tiers. No limits*. No upsells.

*GitHub API rate limits apply

## Documentation

- [QUICKSTART.md](QUICKSTART.md) - 5-minute setup guide
- [EXAMPLES.md](EXAMPLES.md) - Real-world usage examples
- [PRIVACY.md](PRIVACY.md) - Our privacy commitment
- [SECURITY.md](SECURITY.md) - Security practices
- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - Common issues

## Use Cases

- **Startups** - Contact forms without backend costs
- **Freelancers** - Client lead capture
- **Side Projects** - Zero-cost infrastructure
- **Privacy-Conscious** - No third-party tracking
- **Open Source Projects** - Transparent form handling

## Requirements

- Claude Code v1.0+
- GitHub account with repo access
- GitHub Actions enabled

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

## Support

- **Issues:** https://github.com/Luigigreco/gitforms-claude-plugin/issues
- **Discussions:** https://github.com/Luigigreco/gitforms-claude-plugin/discussions
- **Email:** l.greco77@gmail.com

## Contributing

Contributions welcome\! This is open source and we love community involvement.

## License

MIT License - see [LICENSE](LICENSE) for details.

## Author

**Luigi Greco**
- GitHub: [@Luigigreco](https://github.com/Luigigreco)
- Email: l.greco77@gmail.com

---

**The ethical form tool for developers. Zero cost. Zero tracking. 100% open source.**

⭐ Star this repo if you believe in privacy-first tools\!
