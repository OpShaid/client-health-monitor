# AI-Powered Client Health Monitoring System(demo showcase)

A comprehensive SaaS customer success platform that uses AI to track client activity, analyze sentiment, predict churn risk, and generate actionable insights.

## Features

### 🎯 Core Capabilities

- **Real-time Health Scoring**: AI-powered analysis of client health across multiple dimensions
- **Sentiment Analysis**: Automatic sentiment detection across emails, meetings, and feedback
- **Churn Prediction**: ML-based probability scoring for customer churn risk
- **Activity Tracking**: Comprehensive monitoring of emails, payments, meetings, and feedback
- **Actionable Insights**: AI-generated recommendations for customer success teams

### 📊 Dashboard Features

- **Client Portfolio View**: Visual cards showing health scores and risk levels
- **Health Score Trends**: Historical charts tracking engagement and satisfaction
- **Churn Risk Gauge**: Visual representation of churn probability
- **Activity Timeline**: Chronological view of all client interactions
- **Alert System**: Real-time notifications for at-risk clients

### 🔌 Integrations (Mock APIs)

#### Slack Integration
\`\`\`bash
POST /api/integrations/slack
{
  "clientId": "client-1",
  "alertType": "churn_risk"
}
\`\`\`

#### CRM Sync
\`\`\`bash
POST /api/integrations/crm
{
  "clientId": "client-1"
}
\`\`\`

#### Webhook Alerts
\`\`\`bash
POST /api/webhooks/client-at-risk
{
  "clientId": "client-1",
  "threshold": 0.5
}
\`\`\`

## API Endpoints

### Client Analysis

**Analyze Single Client**
\`\`\`bash
POST /api/analyze-client
{
  "clientId": "client-1"
}
\`\`\`

**Batch Analysis**
\`\`\`bash
POST /api/batch-analyze
{
  "clientIds": ["client-1", "client-2", "client-3"]
}
\`\`\`

**Sentiment Analysis**
\`\`\`bash
POST /api/analyze-sentiment
{
  "text": "I'm frustrated with the slow response times",
  "context": "Support ticket"
}
\`\`\`

**Generate Insights**
\`\`\`bash
POST /api/generate-insights
{
  "clientId": "client-1",
  "focusArea": "engagement"
}
\`\`\`

### Alert Management

**Get Alerts**
\`\`\`bash
GET /api/alerts?severity=critical&acknowledged=false
\`\`\`

**Create Alert**
\`\`\`bash
POST /api/alerts
{
  "clientId": "client-1",
  "type": "churn_risk",
  "severity": "critical",
  "message": "Client showing multiple churn signals"
}
\`\`\`

**Acknowledge Alert**
\`\`\`bash
POST /api/alerts/[id]/acknowledge
\`\`\`

## Data Model

### Client Health Score Components

1. **Overall Score (0-100)**: Composite health metric
2. **Engagement Score**: Activity frequency and recency
3. **Satisfaction Score**: Feedback and sentiment analysis
4. **Churn Probability (0-1)**: ML-predicted churn likelihood
5. **Risk Level**: low | medium | high | critical
6. **Trend**: improving | stable | declining

### Activity Types

- **Email**: Customer communications and support tickets
- **Payment**: Transaction history and payment behavior
- **Meeting**: Scheduled calls and attendance
- **Feedback**: Surveys and satisfaction ratings

### Alert Types

- `churn_risk`: High probability of customer churn
- `low_engagement`: Decreased activity levels
- `negative_sentiment`: Negative feedback patterns
- `payment_issue`: Late or failed payments

## Mock Data

The system includes realistic mock data for 5 clients:

1. **TechFlow Inc** (Sarah Chen) - Healthy, expanding
2. **DataSync Solutions** (Marcus Rodriguez) - Critical risk, payment issues
3. **CloudScale Systems** (Emily Watson) - Excellent health, champion account
4. **Innovate Labs** (James Park) - New customer, onboarding challenges
5. **Growth Metrics Co** (Lisa Thompson) - Declining, exploring alternatives

## AI Analysis Engine

The system uses the Vercel AI SDK with GPT-5 to:

- Analyze client activity patterns
- Detect sentiment and emotional tone
- Predict churn probability
- Generate actionable insights
- Recommend next steps for CSMs

## Usage Examples

### Monitoring At-Risk Clients

\`\`\`typescript
// Get all critical alerts
const response = await fetch('/api/alerts?severity=critical&acknowledged=false')
const { alerts } = await response.json()

// Send Slack notification
for (const alert of alerts) {
  await fetch('/api/integrations/slack', {
    method: 'POST',
    body: JSON.stringify({
      clientId: alert.clientId,
      alertType: alert.type
    })
  })
}
\`\`\`

### Analyzing Client Health

\`\`\`typescript
// Analyze a specific client
const response = await fetch('/api/analyze-client', {
  method: 'POST',
  body: JSON.stringify({ clientId: 'client-2' })
})

const { healthScore } = await response.json()

// Check if action needed
if (healthScore.riskLevel === 'critical') {
  // Trigger webhook
  await fetch('/api/webhooks/client-at-risk', {
    method: 'POST',
    body: JSON.stringify({ clientId: 'client-2' })
  })
}
\`\`\`

## Tech Stack

- **Framework**: Next.js 16 with App Router
- **AI**: Vercel AI SDK v5 with GPT-5
- **UI**: shadcn/ui components with Tailwind CSS v4
- **Charts**: Recharts for data visualization
- **TypeScript**: Full type safety

## Getting Started

1. Clone the repository
2. Install dependencies: `npm install`
3. Run development server: `npm run dev`
4. Open [http://localhost:3000](http://localhost:3000)

## Environment Variables

No environment variables required for mock mode. The system uses the Vercel AI Gateway by default.

For production:
- `SLACK_TOKEN`: Slack API token for notifications
- `SALESFORCE_TOKEN`: CRM integration token

## Future Enhancements

- Real database integration (Supabase/Neon)
- Live Slack/CRM webhooks
- Email automation
- Custom ML models for churn prediction
- Multi-tenant support
- Advanced reporting and exports
