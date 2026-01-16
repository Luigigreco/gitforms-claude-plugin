# GitForms Plugin - Troubleshooting

Common issues and solutions.

## Installation Issues

### Plugin Not Found
```
Error: Plugin 'gitforms' not found in marketplace
```

**Solution:**
Install from GitHub directly:
```
/plugin add Luigigreco/gitforms-claude-plugin
/plugin install gitforms
```

### Configuration Missing
```
Error: gitforms_repo not configured
```

**Solution:**
Set your target repository:
```
/settings gitforms_repo owner/repo-name
```

## Form Submission Issues

### Form Not Appearing in /list-contacts

**Possible causes:**
1. Wrong repository configured
2. GitHub Actions not enabled
3. Submission label mismatch

**Solution:**
```bash
# Verify configuration
/settings get gitforms_repo

# Check GitHub Actions status
gh run list --repo owner/repo-name

# Check labels
/list-contacts --label contact
```

### Spam Submissions

**Solution:**
Enable advanced spam protection:
```
/create-form contact name,email,message \
  --spam-protection advanced \
  --rate-limit 5/hour
```

This adds:
- Honeypot fields
- reCAPTCHA v3
- IP rate limiting
- Disposable email blocking

### Submissions Going to Wrong Repository

**Solution:**
Check form action URL:
```html
<!-- Should be -->
<form action="https://gitforms.io/submit/YOUR_USER/YOUR_REPO">

<!-- Not -->
<form action="https://gitforms.io/submit/wrong-repo">
```

Update with:
```
/settings gitforms_repo correct-owner/correct-repo
```

## GitHub Integration Issues

### Permission Denied

```
Error: Resource not found: Not Found
```

**Solution:**
Ensure GitHub token has `repo` scope:
```bash
gh auth login --scopes repo
```

### Workflow Not Triggering

**Possible causes:**
1. GitHub Actions disabled on repository
2. Workflow file missing

**Solution:**
```bash
# Enable Actions
gh api repos/owner/repo -X PATCH -f has_issues=true

# Check workflow exists
gh workflow list --repo owner/repo
```

### Rate Limiting

```
Error: API rate limit exceeded
```

**Solution:**
- Wait 1 hour for reset
- Or upgrade to GitHub Pro ($4/month) for 5000 requests/hour

## Command Issues

### /create-form Not Working

**Error:**
```
Command /create-form not recognized
```

**Solution:**
Plugin not properly installed:
```
/plugin list  # Check if gitforms is listed
/plugin reload gitforms  # Reload plugin
```

### /list-contacts Empty Results

**Possible causes:**
1. No submissions yet
2. Wrong filter applied
3. Wrong repository

**Solution:**
```bash
# Check without filters
/list-contacts

# Check specific repo
/settings gitforms_repo owner/repo
/list-contacts
```

### /analyze-leads No Data

**Solution:**
Need at least 5 submissions for analysis:
```
/list-contacts  # Check submission count
```

## Natural Language Not Working

**Issue:**
Plugin doesn't activate on natural language

**Solution:**
Use explicit trigger keywords:
```
# Instead of: "create form"
# Use: "create a contact form with GitForms"

# Instead of: "show contacts"
# Use: "show me GitForms contacts"
```

## Performance Issues

### Slow Form Loading

**Solution:**
Enable caching:
```
/create-form contact name,email \
  --cache 5m
```

### Large Contact List

**Solution:**
Use pagination:
```
/list-contacts --limit 100 --page 1
```

## Data Migration

### Moving from Another Form Provider

**Typeform/Tally/Google Forms:**
```bash
# Export from current provider to CSV
# Import to GitForms
/import-contacts contacts.csv \
  --map "Name→name,Email→email"
```

### Changing Repository

```bash
# Export current
/list-contacts --format json --output backup.json

# Update config
/settings gitforms_repo new-owner/new-repo

# Import
/import-contacts backup.json
```

## Security Concerns

### Protecting Sensitive Data

**Solution:**
Use private repository:
```bash
gh repo create owner/secure-forms --private
/settings gitforms_repo owner/secure-forms
```

### Preventing Spam

**Solution:**
Multi-layer protection:
```
/create-form contact name,email,message \
  --honeypot \
  --rate-limit 10/hour \
  --require-email-verification
```

### GDPR Compliance

**Solution:**
Enable data retention policy:
```
/settings gitforms_retention 30d
/settings gitforms_gdpr_delete_on_request true
```

## Getting Help

### Check Logs
```
/plugin logs gitforms
```

### Report Bug
https://github.com/Luigigreco/gitforms-claude-plugin/issues

### Community Support
- GitHub Discussions
- Discord: discord.gg/gitforms

### Contact Developer
luigi.greco@proton.me

## Common Workarounds

### API Limits
Use webhook instead of polling:
```
/create-form contact name,email \
  --webhook https://your-api.com/notify
```

### Large Files
Enable file upload limits:
```
/create-form application name,email,resume \
  --upload-max-size 5MB
```

### Custom Domains
Configure CNAME:
```
forms.yourdomain.com → gitforms.io
```

**Still having issues? Create an issue on GitHub!**
