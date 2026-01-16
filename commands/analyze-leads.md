# /analyze-leads

AI-powered analysis of form submissions with insights and recommendations.

## Usage

```
/analyze-leads [--report full|summary|trends]
```

## Examples

```bash
# Quick summary
/analyze-leads

# Full analysis report
/analyze-leads --report full

# Trend analysis
/analyze-leads --report trends --period 30d

# Quality scoring
/analyze-leads --score --threshold 7.0
```

## Analysis Output

### Lead Quality Score
```
📊 LEAD QUALITY ANALYSIS

Overall Score: 8.2/10

Breakdown:
  🟢 High Quality (8-10):  45% (18 leads)
  🟡 Medium Quality (5-7): 35% (14 leads)
  🔴 Low Quality (0-4):    15% (6 leads)
  ⚫ Spam:                  5% (2 leads)
```

### Conversion Patterns
```
🎯 CONVERSION PATTERNS

Top Sources:
  1. Website form:        60% (24 leads)
  2. LinkedIn campaign:   25% (10 leads)
  3. Email signature:     15% (6 leads)

Best Time to Submit:
  🕐 Peak: Tuesday 2-4 PM (12 submissions)
  📉 Low: Weekend (3 submissions)

Budget Distribution:
  💰 $50k+:    6 leads (15%)
  💵 $10-50k: 14 leads (35%)
  💸 <$10k:   20 leads (50%)
```

### Recommendations
```
💡 ACTIONABLE INSIGHTS

1. PRIORITY ACTIONS
   → Follow up with 6 enterprise leads ($50k+ budget)
   → Re-engage 8 leads inactive >7 days

2. FORM OPTIMIZATION
   → Add "Company Size" field (missing in 40%)
   → Simplify "Timeline" field (30% skip rate)

3. SALES STRATEGY
   → Focus on Tuesday PM campaigns (+200% conversion)
   → Create enterprise-specific landing page
```

## Report Types

### Summary (default)
- Quality score distribution
- Top 5 actionable insights
- Quick stats (total/new/replied)

### Full
- Complete breakdown by field
- Individual lead scoring
- Conversion funnel analysis
- Time-series trends
- Geographic distribution (if available)

### Trends
```
📈 30-DAY TREND ANALYSIS

Submissions: ▁▂▃▄▅▆▇█ (+45% vs previous period)
Quality:     ▃▃▄▅▅▆▆▇ (improving)
Response:    ▇▆▅▄▃▃▂▁ (declining - ACTION NEEDED)

⚠️ WARNING: Response time increased from 4h → 12h
   Recommendation: Set up auto-responder
```

## Scoring Algorithm

Lead quality based on:
- Budget indicated (weight: 30%)
- Timeline urgency (weight: 20%)
- Company size (weight: 20%)
- Contact completeness (weight: 15%)
- Previous interactions (weight: 15%)

## Integration

```bash
# Export analysis
/analyze-leads --format json --output analysis.json

# Schedule weekly reports
/analyze-leads --schedule weekly --email team@company.com

# Slack notifications
/analyze-leads --notify slack #sales-team
```

## Advanced Filters

```bash
# Analyze specific segment
/analyze-leads --company "Enterprise*" --budget ">50000"

# Compare time periods
/analyze-leads --period 30d --compare previous

# A/B test analysis
/analyze-leads --form contact-v1 --compare contact-v2
```

## AI Insights

The analyzer uses AI to:
- Detect spam patterns
- Identify qualified leads
- Suggest follow-up timing
- Predict conversion probability
- Recommend form improvements

**Turn data into deals with AI-powered insights!**
