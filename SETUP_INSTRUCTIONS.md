# 🛠️ SMART INBOX TRIAGER - SETUP GUIDE

## ⚡ QUICK START (15 Minutes)

### Prerequisites:
- n8n instance (cloud or self-hosted)
- Gmail account with IMAP enabled
- OpenAI API key ($5 credit needed) OR Claude API key
- Trello account (free tier)
- Slack workspace (free tier)
- Google account for Sheets

---

## 📋 STEP-BY-STEP SETUP

### 1️⃣ n8n Installation

#### Option A: Cloud (Recommended)
```bash
1. Visit https://n8n.cloud
2. Sign up for free trial
3. Create new workflow
```

#### Option B: Self-Hosted
```bash
# Using Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n

# Using NPM
npm install -g n8n
n8n
```

Access at: `http://localhost:5678`

---

### 2️⃣ Import Workflow
```bash
1. Download: Smart_Inbox_Triager_Workflow.json
2. In n8n, click "Import from File"
3. Select the JSON file
4. Workflow will appear in editor
```

---

### 3️⃣ Configure Credentials

#### A) Gmail IMAP (Email Trigger)
```
1. Go to Google Account Settings
2. Security → 2-Step Verification → App Passwords
3. Generate app password for "Mail"
4. In n8n Gmail Trigger node:
   - Email: your-email@gmail.com
   - Password: [16-digit app password]
   - IMAP Host: imap.gmail.com
   - IMAP Port: 993
   - TLS: Enabled
```

#### B) OpenAI API
```
1. Visit https://platform.openai.com/api-keys
2. Create new secret key
3. In n8n HTTP Request node:
   - Header: Authorization: Bearer sk-xxxxx
   - OR use built-in OpenAI credential
```

**Alternative: Claude API**
```
1. Visit https://console.anthropic.com
2. Get API key
3. Configure in HTTP Request node
```

#### C) Trello API
```
1. Visit https://trello.com/power-ups/admin
2. Create new Power-Up
3. Generate API Key and Token
4. In n8n Trello nodes:
   - API Key: [your-key]
   - API Token: [your-token]
   - Board ID: [from Trello board URL]
```

#### D) Slack Webhook
```
1. Visit https://api.slack.com/apps
2. Create New App → From Scratch
3. Incoming Webhooks → Activate
4. Add New Webhook → Select channel
5. Copy Webhook URL
6. Paste in n8n Slack nodes
```

#### E) Google Sheets
```
1. In n8n, add Google Sheets credential
2. Authenticate with OAuth
3. Create new sheet: "Email_Metrics"
4. Headers: Timestamp | Category | Urgency | Sentiment | Response_Time
```

---

### 4️⃣ Environment Variables

Create `.env` file (if self-hosted):
```bash
# AI API
OPENAI_API_KEY=sk-xxxxxxxxxxxxx
# OR
CLAUDE_API_KEY=sk-ant-xxxxxxxxxxxxx

# Email
GMAIL_USER=your-email@gmail.com
GMAIL_APP_PASSWORD=xxxxxxxxxxxxxxxx

# Trello
TRELLO_API_KEY=xxxxxxxxxxxxx
TRELLO_TOKEN=xxxxxxxxxxxxx
TRELLO_BOARD_ID=xxxxxxxxxxxxx

# Slack
SLACK_WEBHOOK_SUPPORT=https://hooks.slack.com/services/xxx
SLACK_WEBHOOK_SALES=https://hooks.slack.com/services/yyy

# Google Sheets
SHEET_ID=xxxxxxxxxxxxx
```

---

## 🧪 TESTING

### Test Email Templates:

#### 1. High-Urgency Support Email
```
To: your-test-inbox@gmail.com
Subject: URGENT: Cannot access my account!!!
Body:
I've been locked out of my account for 3 hours now. 
This is completely unacceptable! I need immediate help.
My user ID is: user12345
This is blocking critical work.
```

**Expected Result:**
- ✅ Classified as: support, high urgency, angry sentiment
- ✅ Trello ticket created with CRITICAL label
- ✅ Auto-reply sent within 10 seconds
- ✅ Slack alert to #support channel
- ✅ Priority score: 9-10

---

#### 2. Sales Inquiry Email
```
To: your-test-inbox@gmail.com
Subject: Interested in Enterprise plan for 50 users
Body:
Hi there,

We're evaluating project management tools for our company.
Could you share:
- Enterprise pricing for 50 users
- Available integrations
- Demo availability this week

Thanks!
John Smith
VP of Operations, TechCorp Inc.
```

**Expected Result:**
- ✅ Classified as: sales, medium urgency, positive sentiment
- ✅ Lead card in Trello sales pipeline
- ✅ Auto-response with pricing link & Calendly
- ✅ Slack notification to #sales
- ✅ Priority score: 6-7

---

#### 3. Spam Email
```
To: your-test-inbox@gmail.com
Subject: 🎉 YOU WON $1,000,000! Click Now!!!
Body:
Congratulations! You've been selected as our lucky winner!
Click here immediately to claim your prize: [suspicious-link]
Offer expires in 24 hours!!! Act now!!!
```

**Expected Result:**
- ✅ Classified as: spam
- ✅ No ticket created
- ✅ No auto-reply sent
- ✅ Logged to Google Sheets
- ✅ Email marked as read/archived

---

### Verification Checklist:
```bash
□ Email trigger activates within 30 seconds
□ AI classification completes in < 5 seconds
□ Trello card created with all details
□ Auto-reply sent from Gmail
□ Slack notification appears
□ Google Sheets row added
□ No errors in execution log
□ Workflow completes end-to-end in < 15 seconds
```

---

## 🐛 TROUBLESHOOTING

### Issue: Email Trigger Not Working
```
Solution:
1. Check Gmail IMAP is enabled:
   Settings → Forwarding and POP/IMAP → Enable IMAP
2. Verify app password (not regular password)
3. Test connection in n8n credentials
4. Check firewall isn't blocking port 993
```

### Issue: AI Returns Invalid JSON
```
Solution:
1. Check API key is valid and has credits
2. Verify prompt template has no syntax errors
3. Add error handling in Code node:
   try {
     return JSON.parse(response);
   } catch(e) {
     return { category: "support", urgency: "medium" };
   }
```

### Issue: Trello API Rate Limit
```
Solution:
1. Free tier: 300 requests/10 seconds
2. Add delay node (2 seconds) before Trello calls
3. Or upgrade to Trello paid plan
```

### Issue: Slack Webhook Fails
```
Solution:
1. Regenerate webhook URL
2. Check channel permissions
3. Test with curl:
   curl -X POST -H 'Content-type: application/json' \
   --data '{"text":"Test"}' YOUR_WEBHOOK_URL
```

---

## 📊 MONITORING

### n8n Execution Log:
```
1. Click "Executions" tab
2. View successful/failed runs
3. Inspect input/output data
4. Check execution time
```

### Metrics Dashboard:
```
1. Open Google Sheet: "Email_Metrics"
2. Create pivot table:
   - Rows: Category
   - Values: Count, Avg Response Time
3. Insert charts for visualization
```

---

## 🚀 PRODUCTION DEPLOYMENT

### Recommended Settings:
```yaml
# n8n Settings
Execution Mode: Queue
Max Concurrent Executions: 10
Timeout: 60 seconds
Error Workflow: [Create separate error handling workflow]

# Monitoring
Enable: Execution retention (30 days)
Alerts: Slack webhook for failures
Health Check: /healthz endpoint
```

### Scaling Considerations:
```
- Use n8n Cloud Pro for high volume (>1000 emails/day)
- Implement queue-based processing
- Add Redis cache for duplicate detection
- Load balance across multiple n8n instances
```

---

## 📞 SUPPORT

**Issues?** Contact: [your-email]@sap.com

**Documentation:**
- n8n Docs: https://docs.n8n.io
- OpenAI API: https://platform.openai.com/docs
- Trello API: https://developer.atlassian.com/cloud/trello

---

**Last Updated:** November 21, 2025  
**Version:** 1.0.0  
**License:** MIT
