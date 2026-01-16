# /list-contacts

Retrieve and manage form submissions from GitHub Issues.

## Usage

```
/list-contacts [filters] [--format table|csv|json]
```

## Examples

```bash
# All contacts
/list-contacts

# Filter by label
/list-contacts --label lead
/list-contacts --label urgent

# Filter by date
/list-contacts --since 2025-01-01
/list-contacts --last 7d

# Export to CSV
/list-contacts --format csv --output leads.csv

# Filter by field value
/list-contacts --company "Acme Corp"
/list-contacts --budget ">10000"
```

## Output Formats

### Table (default)
```
┌─────┬──────────────┬────────────────────┬────────────┬──────────┐
│ ID  │ Name         │ Email              │ Company    │ Status   │
├─────┼──────────────┼────────────────────┼────────────┼──────────┤
│ #42 │ John Doe     │ john@example.com   │ Acme Corp  │ Open     │
│ #41 │ Jane Smith   │ jane@startup.io    │ Startup Co │ Replied  │
└─────┴──────────────┴────────────────────┴────────────┴──────────┘
```

### CSV
```csv
id,name,email,company,submitted_at,status
42,John Doe,john@example.com,Acme Corp,2025-01-15T10:30:00Z,open
41,Jane Smith,jane@startup.io,Startup Co,2025-01-14T15:45:00Z,closed
```

### JSON
```json
[
  {
    "id": 42,
    "name": "John Doe",
    "email": "john@example.com",
    "company": "Acme Corp",
    "submitted_at": "2025-01-15T10:30:00Z",
    "status": "open",
    "labels": ["contact", "lead"]
  }
]
```

## Batch Operations

```bash
# Mark multiple as contacted
/list-contacts --label lead --action mark-contacted

# Delete spam submissions
/list-contacts --label spam --action delete

# Export high-value leads
/list-contacts --budget ">50000" --format csv --output hot-leads.csv

# Assign to team member
/list-contacts --company "Enterprise*" --action assign @sales-team
```

## Filters

| Filter | Example | Description |
|--------|---------|-------------|
| `--label` | `--label lead` | Filter by GitHub label |
| `--since` | `--since 2025-01-01` | Submissions after date |
| `--last` | `--last 30d` | Last N days/weeks/months |
| `--status` | `--status open` | Open/closed issues |
| `--company` | `--company "Acme*"` | Wildcard company search |
| `--budget` | `--budget ">10000"` | Numeric comparisons |
| `--email` | `--email "@gmail.com"` | Email domain filter |

## Integration

Works with:
- **CRM Export**: CSV format for Salesforce/HubSpot import
- **Email Marketing**: Export emails for Mailchimp/SendGrid
- **Analytics**: JSON format for data analysis
- **Zapier**: Webhook integration for automation

## Performance

- Fetches up to 1000 contacts per query
- Caches results for 5 minutes
- Pagination support for large datasets
- Rate limit: 100 requests/hour

**Manage your leads without leaving Claude!**
