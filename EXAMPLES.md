# GitForms Plugin - Examples

Real-world usage examples for common scenarios.

## Basic Contact Form

```
/create-form contact name,email,message
```

Embed on website:
```html
<form action="https://gitforms.io/submit/yourname/contact-submissions" method="POST">
  <input type="text" name="name" placeholder="Name" required>
  <input type="email" name="email" placeholder="Email" required>
  <textarea name="message" placeholder="Message" required></textarea>
  <button type="submit">Send</button>
</form>
```

## Lead Capture with Qualification

```
/create-form lead-capture name,email,company,budget,timeline
```

Advanced options:
```
/create-form lead-capture \
  --labels lead,sales \
  --notify email:sales@company.com \
  --required name,email,company
```

## Event Registration

```
/create-form event-signup \
  "Full Name,Email,Company,Number of Attendees,Dietary Requirements"
```

## Newsletter Subscription

```
/create-form newsletter email --simple
```

Generates minimal form:
```html
<form action="https://gitforms.io/submit/yourname/subscribers" method="POST">
  <input type="email" name="email" placeholder="Your email" required>
  <button>Subscribe</button>
</form>
```

## Contact Management

### View All Contacts
```
/list-contacts
```

### Filter by Date
```
/list-contacts --since 2025-01-01
/list-contacts --last 7d
```

### Filter by Quality
```
/list-contacts --label lead --budget ">10000"
```

### Export to CSV
```
/list-contacts --format csv --output hot-leads.csv
```

### Batch Actions
```
/list-contacts --label lead --action mark-contacted
```

## Lead Analysis

### Quick Summary
```
/analyze-leads
```

Output:
```
📊 LEAD QUALITY ANALYSIS
Overall Score: 8.2/10
  🟢 High Quality:  45% (18 leads)
  🟡 Medium:        35% (14 leads)
  🔴 Low:           15% (6 leads)
```

### Full Report
```
/analyze-leads --report full
```

### Trend Analysis
```
/analyze-leads --report trends --period 30d
```

### Compare Time Periods
```
/analyze-leads --period 30d --compare previous
```

## Integration Examples

### React Component

```jsx
import { GitForm } from '@gitforms/react'

function ContactForm() {
  return (
    <GitForm
      repo="yourname/contact-submissions"
      fields={['name', 'email', 'message']}
      onSuccess={() => alert('Thanks!')}
      labels={['contact', 'website']}
    />
  )
}
```

### Static HTML with Custom Styling

```html
<form action="https://gitforms.io/submit/yourname/leads" method="POST" class="contact-form">
  <div class="form-group">
    <label for="name">Name *</label>
    <input type="text" id="name" name="name" required>
  </div>

  <div class="form-group">
    <label for="email">Email *</label>
    <input type="email" id="email" name="email" required>
  </div>

  <div class="form-group">
    <label for="company">Company</label>
    <input type="text" id="company" name="company">
  </div>

  <button type="submit">Submit</button>
</form>
```

### Direct API Submission

```javascript
fetch('https://gitforms.io/submit/yourname/leads', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    name: 'John Doe',
    email: 'john@example.com',
    company: 'Acme Corp'
  })
})
```

## Advanced Form Features

### Conditional Fields

```
/create-form quote-request \
  "Service→If 'Enterprise'→Team Size,Budget"
```

### Multi-Step Form

```
/create-form onboarding --multi-step \
  "Step1:name,email|Step2:company,role|Step3:goals,timeline"
```

### File Upload Support

```
/create-form application name,email,resume --upload resume:pdf,doc
```

## Webhook Integration

```
/create-form contact name,email,message \
  --webhook https://your-api.com/webhook \
  --webhook-secret your_secret_key
```

Webhook receives:
```json
{
  "event": "form_submission",
  "form": "contact",
  "data": {
    "name": "John Doe",
    "email": "john@example.com",
    "message": "Hello!"
  },
  "submitted_at": "2025-01-15T10:30:00Z",
  "signature": "sha256=..."
}
```

## Natural Language Examples

Instead of commands, use natural language:

```
"Create a contact form for my SaaS landing page"
→ Generates form with name, email, company fields

"Show me enterprise leads from last month"
→ /list-contacts --label enterprise --since 2024-12-15

"Which leads should I prioritize?"
→ /analyze-leads --score --threshold 8.0

"Export all high-value leads to CSV"
→ /list-contacts --budget ">50000" --format csv
```

## Pricing Tiers

### Free Tier
- Unlimited forms
- 1000 submissions/month
- GitHub Issues storage
- Basic spam protection

### Pro ($9/month)
- 10,000 submissions/month
- Advanced spam protection
- Priority support
- Custom branding removal

### Enterprise (custom)
- Unlimited submissions
- Dedicated support
- SLA guarantees
- Custom integrations

**All examples use free tier by default!**
