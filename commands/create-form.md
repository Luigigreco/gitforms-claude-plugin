# /create-form

Create a complete HTML form that submits to GitHub Issues via GitForms.

## Usage

```
/create-form [form-name] [field1,field2,...]
```

## Examples

```bash
# Basic contact form
/create-form contact-form name,email,message

# Lead capture with qualification
/create-form lead-capture name,email,company,budget,timeline

# Event registration
/create-form event-registration name,email,company,attendees
```

## What it creates

1. **HTML Form** - Complete form with validation
2. **Schema Definition** - Field types and validation rules
3. **Email Notifications** - Automated alerts on submission
4. **GitHub Actions Workflow** - Automated issue creation
5. **Spam Protection** - Honeypot fields + rate limiting

## Form Configuration

The command generates:

```html
<form action="https://gitforms.io/submit/YOUR_REPO" method="POST">
  <input type="text" name="name" required>
  <input type="email" name="email" required>
  <textarea name="message" required></textarea>
  <button type="submit">Submit</button>
</form>
```

Plus:
- `.gitforms/schema.json` - Validation rules
- `.github/workflows/gitforms.yml` - Auto-processing
- `FORM_CONFIG.md` - Setup instructions

## Advanced Options

```bash
# With custom labels
/create-form lead-capture "Full Name,Email Address,Company Name"

# With conditional fields
/create-form quote-request "Service Type→If 'Enterprise'→Team Size"

# Multi-step form
/create-form onboarding --multi-step "Step1:name,email|Step2:company,role|Step3:goals"
```

## Integration

The form submits to GitHub Issues with labels:
- `contact` - Auto-applied to all submissions
- `lead` - Applied if budget/timeline provided
- `urgent` - Applied if priority field checked

## Security

- Server-side validation via GitHub Actions
- Rate limiting: 10 submissions/hour per IP
- Honeypot fields for spam detection
- CORS whitelist configuration
- GitHub Secrets for sensitive config

## Output

Creates these files in your repository:
- `forms/[form-name].html` - Form markup
- `.gitforms/[form-name]-schema.json` - Validation
- `.github/workflows/gitforms-[form-name].yml` - Automation

**Ready to deploy in 2 minutes!**
