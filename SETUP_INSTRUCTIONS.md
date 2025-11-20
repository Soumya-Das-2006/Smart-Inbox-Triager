# 🛠️ SMART INBOX TRIAGER — SETUP GUIDE

### Production-Ready Installation Manual (v1.1)

**Last Updated:** November 21, 2025

---

# ⚡ QUICK START (Setup Time: ~15 Minutes)

### ✅ Prerequisites

- n8n instance (Cloud or Self-Hosted)
- Gmail account with IMAP enabled (requires App Password)
- OpenAI or Claude API Key
- Trello account (free tier)
- Slack workspace (free tier)
- Google Sheets (for analytics logs)

---

# 📋 STEP-BY-STEP INSTALLATION

---

## 1️⃣ Install n8n

### **Option A: n8n Cloud (Recommended)**

1. Visit: **https://n8n.cloud**
2. Sign up for a free trial
3. Click **Create Workflow**

### **Option B: Self-Hosted via Docker**

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

### **Option C: Self-Hosted via NPM**

```bash
npm install -g n8n
n8n
```

➡️ Access the UI at: **http://localhost:5678**

---

## 2️⃣ Import the Workflow

1. Download: **Smart_Inbox_Triager_Workflow.json**
2. Open n8n → **Import from File**
3. The full workflow will appear in the editor

---

## 3️⃣ Configure Credentials

---

### **A) Email IMAP Node (Gmail)**

> Note: Gmail IMAP requires 2FA + App Password.

#### Steps:

1. Go to **Google Account → Security**
2. Enable **2-Step Verification**
3. Open **App Passwords**
4. Generate App Password for **Mail**
5. Configure n8n IMAP node:

```
Host: imap.gmail.com
Port: 993
User: your-email@gmail.com
Password: 16-digit App Password
SSL/TLS: true
```

---

### **B) OpenAI (Recommended)**

Use the native **Chat Model** node (NOT HTTP Request).

Steps:

1. Visit: https://platform.openai.com/api-keys
2. Create a new API key
3. In n8n:
   - Credentials → **OpenAI**
   - Paste API Key
4. Set model: **gpt-4.1**, **gpt-4o-mini**, or **gpt-4o**

---

### **C) Claude (Alternative)**

1. Visit: https://console.anthropic.com
2. Create API Key
3. In n8n:
   - Use **AI Model** node → Anthropic
   - Paste the API key

---

### **D) Trello API**

> Correct & Updated Method (Power-Up method deprecated)

1. Open: https://trello.com/app-key
2. Copy **API Key**
3. Click **Generate Token**
4. In n8n:
   - Credentials → Trello
   - Add Key + Token

---

### **E) Slack Webhook**

1. Visit: https://api.slack.com/apps
2. Create **New App → From Scratch**
3. Enable **Incoming Webhooks**
4. Add Webhook → Select Channel
5. Copy Webhook URL
6. Add to n8n Slack node

Scopes required:

```
incoming-webhook
```

---

### **F) Google Sheets**

1. In n8n → **Google Sheets** credential
2. Authenticate via OAuth
3. Create new Sheet: **Email_Metrics**
4. Add headers:

```
Timestamp | Category | Urgency | Sentiment | Response_Time
```

5. Get Sheet ID:

```
https://docs.google.com/spreadsheets/d/<SHEET_ID>/edit
```

---

# 4️⃣ Optional: Environment Variables (.env)

If running self-hosted:

```bash
# AI
OPENAI_API_KEY=sk-xxxxxxxx
CLAUDE_API_KEY=sk-ant-xxxxxx

# Gmail IMAP
GMAIL_USER=your-email@gmail.com
GMAIL_APP_PASSWORD=xxxxxxxxxxxx

# Trello
TRELLO_API_KEY=xxxxxxxx
TRELLO_TOKEN=xxxxxxxx
TRELLO_BOARD_ID=xxxxxxxx

# Slack
SLACK_WEBHOOK_SUPPORT=https://hooks.slack.com/services/xxx
SLACK_WEBHOOK_SALES=https://hooks.slack.com/services/yyy

# Google Sheets
SHEET_ID=xxxxxxxx
```

Reference inside nodes:

```
{{$env.OPENAI_API_KEY}}
```

⚠  Never upload `.env` to GitHub.

---

# 🧪 TESTING THE SYSTEM

---

## **Test Email 1 — Critical Support**

```
Subject: URGENT: Cannot access my account!!!
Body:
I've been locked out of my account for hours. 
This is blocking important work. Please assist immediately.
```

Expected:

- Classified: support / high urgency / angry
- Trello card → CRITICAL
- Auto-reply sent
- Slack alert → #support
- Priority score: 9–10

---

## **Test Email 2 — Sales Inquiry**

```
Subject: Enterprise plan quote for 50 users
Body:
Please share pricing, integrations, and demo availability.
– John Smith
```

Expected:

- Classified: sales / medium urgency / positive
- Trello lead card
- Auto response w/ pricing link + Calendly
- Slack → #sales

---

## **Test Email 3 — Spam**

```
Subject: 🎉 YOU WON $1,000,000! ACT NOW!!!
Body:
Click this link to claim your BIG reward!
```

Expected:

- Classified as spam
- No auto-reply
- Logged in Google Sheets
- Email archived

---

# ✓ Verification Checklist

```
□ IMAP trigger activates within 30s  
□ AI classification < 5s  
□ Trello card created  
□ Auto reply sent  
□ Slack notification works  
□ Metrics row added in Sheets  
□ Workflow finishes < 15s  
□ No JSON parse errors
```

---

# 🐛 TROUBLESHOOTING

### ❗ IMAP Not Triggering

```
1. Ensure IMAP is enabled in Gmail:
   Settings → Forwarding & POP/IMAP → Enable IMAP
2. Use 16-digit App Password
3. Check Gmail security alerts and mark as "Yes, it was me"
4. Confirm port 993 is not blocked
```

---

### ❗ AI Returns Invalid JSON

```
1. Ensure your API key has enough credit
2. Validate your prompt template
3. Add safe fallback:

try {
  return JSON.parse(response);
} catch (e) {
  return { category: "support", urgency: "medium" };
}
```

---

### ❗ Trello Rate Limits

```
Free tier: 300 requests / 10 seconds  
Solution:
- Add Delay Node (2 seconds)
- Reduce excessive card updates
```

---

### ❗ Slack Webhook Fails

```
1. Regenerate Webhook URL  
2. Check app permissions  
3. Test manually:
   curl -X POST -H 'Content-type: application/json' \
   --data '{"text":"Test"}' <WEBHOOK_URL>
```

---

# 📊 Monitoring & Logs

### n8n Execution Logs:

```
Executions → Select Run → View Input/Output → Check Duration
```

### Google Sheets Dashboard:

1. Open **Email_Metrics**
2. Create pivot table:
   - Rows: Category
   - Values: Count, Avg Response Time
3. Add pie chart + trend charts

---

# 🚀 PRODUCTION RECOMMENDATIONS

### n8n Configuration:

```yaml
Execution Mode: queue
Max Parallel Executions: 10
Timeout: 60 seconds
Error Workflow: Enabled
```

### Scaling:

```
- Use n8n Cloud Pro for >1000 emails/day
- Use Redis for queuing and caching
- Add load-balanced n8n workers
- Enable webhook retries & error alerts
```

---

# 📞 SUPPORT & RESOURCES

- **Issues?**
  Contact: soumyadastopper2006@gmail.com
  Phone: 8159824282

# 📑 Documentation

- **n8n Docs:** https://docs.n8n.io
- **OpenAI Docs:** https://platform.openai.com/docs
- **Trello API:** https://developer.atlassian.com/cloud/trello
- **Slack API:** https://api.slack.com

---

# 🎉 Congratulations!

Your **Smart Inbox Triager** is now fully installed, configured, and ready to automate your entire email inbox using AI + n8n.
