# GitForms Plugin - Quick Start

Get started with GitForms in 5 minutes!

## Installation

```bash
# Install from Claude Code marketplace
/plugin install gitforms

# Or install from GitHub
/plugin add Luigigreco/gitforms-claude-plugin
```

## Configuration

Set your GitHub repository for form submissions:

```
/settings gitforms_repo owner/repo
```

Example:
```
/settings gitforms_repo Luigigreco/contact-submissions
```

## Create Your First Form

```
/create-form contact-form name,email,message
```

This generates:
- HTML form ready to embed
- GitHub Issues backend
- Automated workflows
- Spam protection

## Test It

1. Copy the generated HTML
2. Add to your website
3. Submit a test form
4. Check `/list-contacts` to see submission

## View Submissions

```
/list-contacts
```

## Analyze Leads

```
/analyze-leads
```

## Natural Language

You can also use natural language:

```
"Create a contact form with name and email"
"Show me all leads from this week"
"Analyze my form submissions"
```

## Next Steps

- Check [EXAMPLES.md](EXAMPLES.md) for advanced usage
- Read [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues
- See [README.md](README.md) for complete documentation

**You're all set! 🎉**
