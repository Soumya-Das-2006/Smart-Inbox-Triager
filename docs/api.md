# 🔐 API CREDENTIALS CHECKLIST
## Smart Inbox Triager - All APIs & Setup Links

**Developer:** Soumya Das  
**Email:** soumyadastopper2006@gmail.com  
**Project:** Smart Inbox Triager

---

## 📋 QUICK REFERENCE TABLE

| API / Service | Purpose | Cost | Setup Time |
|---------------|---------|------|------------|
| Gmail API | Email monitoring & sending | FREE | 10 min |
| OpenAI API | AI classification | ₹60/month (100 emails/day) | 5 min |
| Trello API | Ticket management | FREE | 10 min |
| Slack API | Team notifications | FREE | 5 min |
| Google Sheets API | Analytics tracking | FREE | 5 min |
| n8n | Workflow automation | FREE (self-hosted) | 10 min |

**Total Monthly Cost:** ₹60-600 depending on email volume  
**Total Setup Time:** ~45 minutes

---

## 1️⃣ GMAIL API

### Purpose:
- Monitor inbox for new emails (IMAP)
- Send automated responses (SMTP)

### What You Need:
✅ Gmail account (any existing Gmail)  
✅ 2-Step Verification enabled  
✅ App Password generated

### Setup Links:
- **Gmail Settings:** https://mail.google.com/mail/u/0/#settings/fwdandpop
- **Google Account Security:** https://myaccount.google.com/security
- **App Passwords:** https://myaccount.google.com/apppasswords

### Step-by-Step:

**1. Enable IMAP:**
```
Settings → Forwarding and POP/IMAP → Enable IMAP → Save
```

**2. Enable 2-Step Verification:**
```
myaccount.google.com → Security → 2-Step Verification → Turn on
```

**3. Create App Password:**
```
Security → App passwords → Select app: Mail → Generate
Copy 16-digit password: xxxx xxxx xxxx xxxx
```

### Credentials to Save:
```
Gmail Email: ________________________@gmail.com
App Password: ____ ____ ____ ____ (16 digits)
IMAP Host: imap.gmail.com
IMAP Port: 993
SMTP Host: smtp.gmail.com
SMTP Port: 465 or 587
```

### Cost: 
**FREE** - No limits for personal use

### Documentation:
https://support.google.com/mail/answer/7126229

---

## 2️⃣ OPENAI API (GPT-4)

### Purpose:
- AI-powered email classification
- Sentiment analysis
- Urgency detection
- Summary generation

### What You Need:
✅ OpenAI account  
✅ Payment method added  
✅ ₹400+ credits loaded

### Setup Links:
- **Sign Up:** https://platform.openai.com/signup
- **API Keys:** https://platform.openai.com/api-keys
- **Billing:** https://platform.openai.com/account/billing
- **Usage:** https://platform.openai.com/account/usage

### Step-by-Step:

**1. Create Account:**
```
platform.openai.com/signup → Enter email → Verify
```

**2. Add Payment Method:**
```
Billing → Add payment method → Enter card → Load ₹400-500
```

**3. Generate API Key:**
```
API Keys → + Create new secret key → Name: "n8n Email Triager" → Copy key
```

### Credentials to Save:
```
API Key: sk-proj-________________________________________________
Organization ID (optional): org-________________________________
```

### Cost Estimate:
- **Model:** GPT-4 Turbo
- **Per Email:** ₹0.60 (500 tokens average)
- **100 emails/day:** ₹60/day = ₹1,800/month
- **Cheaper option:** GPT-3.5 Turbo = ₹0.06/email = ₹180/month

### Cost Optimization Tips:
```
- Use GPT-3.5-turbo for testing (10x cheaper)
- Set max_tokens to 300 instead of 500
- Add rate limiting for high volumes
- Monitor usage daily: platform.openai.com/account/usage
```

### Documentation:
https://platform.openai.com/docs/api-reference

---

## 3️⃣ TRELLO API

### Purpose:
- Create support tickets automatically
- Manage sales leads
- Organize workflow

### What You Need:
✅ Trello account (free)  
✅ Board with lists created  
✅ API Key & Token

### Setup Links:
- **Sign Up:** https://trello.com/signup
- **Power-Ups Admin:** https://trello.com/power-ups/admin
- **API Documentation:** https://developer.atlassian.com/cloud/trello/

### Step-by-Step:

**1. Create Account & Board:**
```
trello.com/signup → Create board: "Email Triage System"
Create lists: "Support Queue", "Sales Pipeline", "Completed"
```

**2. Get API Key:**
```
trello.com/power-ups/admin → New → Create Power-Up
Name: "n8n Integration" → Copy API Key
```

**3. Generate Token:**
```
Same page → Click "generate a Token" → Allow → Copy Token
```

**4. Get Board ID:**
```
Open board → Add ".json" to URL → Find "id" field near top
```

**5. Get List IDs:**
```
Same JSON → Find "lists" array → Match list names to IDs
```

### Credentials to Save:
```
API Key: ________________________________ (32 chars)
Token: ________________________________________________________________ (64 chars)
Board ID: ________________________ (24 chars)
Support List ID: ________________________ (24 chars)
Sales List ID: ________________________ (24 chars)
```

### Cost:
**FREE** - Up to 10 boards, unlimited cards

### Rate Limits:
- 300 requests per 10 seconds
- 100 requests per 10 seconds per token
- More than enough for email automation

### Documentation:
https://developer.atlassian.com/cloud/trello/guides/rest-api/api-introduction/

---

## 4️⃣ SLACK API (Webhooks)

### Purpose:
- Send real-time notifications to team
- Alert on high-priority emails
- Share ticket links

### What You Need:
✅ Slack workspace (free)  
✅ Channels created (#support, #sales)  
✅ Incoming Webhooks configured

### Setup Links:
- **Create Workspace:** https://slack.com/get-started
- **Create App:** https://api.slack.com/apps
- **Webhook Guide:** https://api.slack.com/messaging/webhooks

### Step-by-Step:

**1. Create Workspace (if needed):**
```
slack.com/get-started → Create workspace: "My Team"
```

**2. Create Channels:**
```
+ next to Channels → Create #support (public)
Repeat for #sales
```

**3. Create App:**
```
api.slack.com/apps → Create New App → From scratch
Name: "n8n Email Triager" → Select workspace
```

**4. Enable Webhooks:**
```
Incoming Webhooks → Toggle ON
Add New Webhook to Workspace → Select #support → Allow
Copy webhook URL
Repeat for #sales channel
```

### Credentials to Save:
```
Support Webhook: https://hooks.slack.com/services/T____________/B____________/________________________
Sales Webhook: https://hooks.slack.com/services/T____________/B____________/________________________
```

### Test Webhook:
```bash
curl -X POST -H 'Content-type: application/json' \
--data '{"text":"Test from command line"}' \
https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Cost:
**FREE** - Unlimited messages

### Rate Limits:
- 1 message per second per webhook
- More than enough for email notifications

### Documentation:
https://api.slack.com/messaging/webhooks

---

## 5️⃣ GOOGLE SHEETS API

### Purpose:
- Log all email classifications
- Track metrics and analytics
- Create dashboards

### What You Need:
✅ Google account  
✅ New Google Sheet created  
✅ OAuth2 authentication (done in n8n)

### Setup Links:
- **Google Sheets:** https://sheets.google.com
- **API Console:** https://console.cloud.google.com
- **n8n Google Sheets Docs:** https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlesheets/

### Step-by-Step:

**1. Create Sheet:**
```
sheets.google.com → + Blank → Name: "Email Metrics Dashboard"
Add headers in row 1:
A1: Timestamp
B1: Category  
C1: Urgency
D1: Sentiment
E1: Priority_Score
F1: Sender_Email
G1: Subject
H1: Response_Time_Seconds
```

**2. Get Sheet ID:**
```
Copy from URL: https://docs.google.com/spreadsheets/d/SHEET_ID/edit
```

**3. Configure in n8n:**
```
n8n will handle OAuth2 authentication automatically
Just connect your Google account when prompted
```

### Credentials to Save:
```
Sheet ID: __________________________________________
Sheet Name: Email Metrics Dashboard
Tab Name: Sheet1 (or your tab name)
```

### Cost:
**FREE** - 15 GB storage included with Google account

### Limits:
- 10 million cells per sheet
- 50,000 rows more than enough for years of data

### Documentation:
https://developers.google.com/sheets/api

---

## 6️⃣ N8N (Workflow Platform)

### Purpose:
- Orchestrate all integrations
- Execute automation workflow
- Handle logic and routing

### What You Need:
Choose ONE option:

**Option A: n8n Cloud** (Easiest)
- ✅ No installation needed
- ✅ Automatic updates
- ✅ Hosted infrastructure
- ❌ Costs ₹1,600/month after trial

**Option B: Self-Hosted** (Free)
- ✅ Completely free forever
- ✅ Full control and privacy
- ❌ Requires setup and maintenance

### Setup Links:
- **n8n Cloud:** https://n8n.cloud
- **Self-Hosted Docs:** https://docs.n8n.io/hosting/
- **GitHub:** https://github.com/n8n-io/n8n
- **Docker Hub:** https://hub.docker.com/r/n8nio/n8n

### Installation Methods:

**Method 1: npx (Quick Test)**
```bash
npx n8n
# Access: http://localhost:5678
# Good for: Testing, learning
# Keep terminal open
```

**Method 2: Docker (Recommended)**
```bash
docker run -it --rm --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n

# Access: http://localhost:5678
# Good for: Production, easy management
```

**Method 3: npm Global**
```bash
npm install -g n8n
n8n
# Access: http://localhost:5678
# Good for: Development
```

**Method 4: PM2 (Production)**
```bash
npm install -g pm2
pm2 start n8n
pm2 save
pm2 startup
# Runs in background, auto-starts on boot
```

### Credentials to Save:
```
n8n URL: http://localhost:5678 (self-hosted) OR https://yourname.app.n8n.cloud
n8n Login: ________________________
n8n Password: ________________________
```

### Cost:
- **Cloud:** ₹1,600/month (14-day free trial)
- **Self-Hosted:** ₹0 forever

### System Requirements:
- RAM: 4GB minimum (8GB recommended)
- Storage: 2GB free space
- Node.js: v18 or higher (for npm method)
- Docker: Latest version (for Docker method)

### Documentation:
https://docs.n8n.io

---

## 📊 CREDENTIALS SECURITY CHECKLIST

### ✅ DO:
- [ ] Store all credentials in password manager (1Password, Bitwarden)
- [ ] Use .env file for self-hosted n8n
- [ ] Never commit credentials to GitHub
- [ ] Rotate API keys every 90 days
- [ ] Use separate API keys for dev and production
- [ ] Enable 2FA on all accounts
- [ ] Backup credentials in secure location

### ❌ DON'T:
- [ ] Share credentials in Slack/email
- [ ] Hardcode credentials in workflows
- [ ] Upload workflows with credentials to public repos
- [ ] Use same password across services
- [ ] Take screenshots of credentials
- [ ] Store in plain text files

---

## 🔄 CREDENTIAL ROTATION SCHEDULE

**Every 30 Days:**
- [ ] Check OpenAI API usage and costs
- [ ] Review Google Sheets for anomalies
- [ ] Verify all integrations still working

**Every 90 Days:**
- [ ] Rotate OpenAI API key
- [ ] Regenerate Trello token
- [ ] Update Gmail App Password
- [ ] Regenerate Slack webhooks
- [ ] Update all credentials in n8n

**Annually:**
- [ ] Review all API pricing (may have changed)
- [ ] Upgrade n8n if self-hosted
- [ ] Audit access logs
- [ ] Update documentation

---

## 💾 CREDENTIALS BACKUP TEMPLATE

Create file: `credentials_backup.txt` (encrypt this file!)

```
# SMART INBOX TRIAGER - CREDENTIALS BACKUP
# Created: [DATE]
# Last Updated: [DATE]

## GMAIL
Email: ________________________@gmail.com
App Password: ____ ____ ____ ____
IMAP: imap.gmail.com:993
SMTP: smtp.gmail.com:465

## OPENAI
API Key: sk-proj-________________________________________________
Organization: org-________________________________
Billing: https://platform.openai.com/account/billing
Usage: https://platform.openai.com/account/usage

## TRELLO
API Key: ________________________________
Token: ________________________________________________________________
Board ID: ________________________
Support List ID: ________________________
Sales List ID: ________________________
Board URL: https://trello.com/b/____________/email-triage-system

## SLACK
Support Webhook: https://hooks.slack.com/services/T____________/B____________/________________________
Sales Webhook: https://hooks.slack.com/services/T____________/B____________/________________________
Workspace: ________________________.slack.com

## GOOGLE SHEETS
Sheet ID: __________________________________________
Sheet URL: https://docs.google.com/spreadsheets/d/____________/edit
Sheet Name: Email Metrics Dashboard

## N8N
URL: ________________________
Login: ________________________
Password: ________________________
Version: ________________________

## NOTES
- Created for: n8n Hackathon 2025
- Developer: Soumya Das
- Email: soumyadastopper2006@gmail.com
- Phone: +91 8159824282

## BACKUP LOCATIONS
- Password Manager: ✅ / ❌
- Encrypted USB: ✅ / ❌
- Secure Cloud: ✅ / ❌
- Physical Safe: ✅ / ❌
```

**IMPORTANT:** Encrypt this file with:
- GPG: `gpg -c credentials_backup.txt`
- 7-Zip: With AES-256 encryption
- VeraCrypt: In encrypted container

---

## 🚨 EMERGENCY CONTACT INFO

### If Credentials Compromised:

**Immediate Actions:**
1. Revoke compromised credentials IMMEDIATELY
2. Generate new credentials
3. Update in n8n workflow
4. Review recent activity logs
5. Check for unauthorized usage
6. Report to service provider if needed

**Gmail Compromised:**
```
1. Change Google Account password
2. Revoke App Passwords: myaccount.google.com/apppasswords
3. Generate new App Password
4. Review account activity: myaccount.google.com/security
```

**OpenAI Compromised:**
```
1. Delete API key: platform.openai.com/api-keys
2. Create new API key
3. Check usage for unauthorized calls
4. Contact support if needed
```

**Trello Compromised:**
```
1. Revoke token: trello.com/power-ups/admin
2. Generate new token
3. Check board activity
```

**Slack Compromised:**
```
1. Regenerate webhooks: api.slack.com/apps
2. Check recent messages
3. Rotate workspace credentials
```

### Support Contacts:

**Developer:**
- Name: Soumya Das
- Email: soumyadastopper2006@gmail.com
- Phone: +91 8159824282

**Service Support:**
- Gmail: https://support.google.com/mail
- OpenAI: https://help.openai.com
- Trello: https://trello.com/contact
- Slack: https://slack.com/help
- n8n: https://community.n8n.io

---

## ✅ FINAL SETUP VERIFICATION

Before starting workflow, verify ALL credentials:

```
□ Gmail IMAP connection tested ✅
□ Gmail OAuth2 authenticated ✅
□ OpenAI API key valid and has credits ✅
□ Trello API key and token working ✅
□ Trello board and list IDs correct ✅
□ Slack webhooks tested (send test message) ✅
□ Google Sheets OAuth authenticated ✅
□ Google Sheet ID correct ✅
□ All credentials backed up securely ✅
□ n8n workflow imported successfully ✅
□ All node credentials configured ✅
```

**If all checked:** You're ready to test! 🎉

**If any unchecked:** Refer to setup sections above

---

**Document Version:** 1.0  
**Last Updated:** November 21, 2025  
**Status:** Ready for Production  

**🔐 Keep This Document Secure! 🔐**
