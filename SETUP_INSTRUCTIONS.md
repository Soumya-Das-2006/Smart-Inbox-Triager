# 🛠️ SETUP & TESTING INSTRUCTIONS
## Smart Inbox Triager - Complete Implementation Guide

**Project:** Smart Inbox Triager  
**Submitted By:** Soumya Das (soumyadastopper2006@gmail.com)  
**Document Version:** 1.0  
**Last Updated:** November 21, 2025

---

## 📋 TABLE OF CONTENTS

1. Prerequisites & Requirements
2. API Accounts Setup (Step-by-Step)
3. n8n Installation
4. Workflow Import Process
5. Credential Configuration
6. Environment Variables
7. Testing Procedures
8. Troubleshooting Guide
9. Production Deployment
10. Monitoring & Maintenance

---

## 1️⃣ PREREQUISITES & REQUIREMENTS

### System Requirements:
- **Operating System:** Windows 10/11, macOS 10.15+, or Linux
- **RAM:** Minimum 4GB (8GB recommended)
- **Storage:** 2GB free space
- **Internet:** Stable broadband connection
- **Browser:** Chrome, Firefox, or Edge (latest version)

### Required Accounts (All FREE tiers available):
1. ✅ Gmail account
2. ✅ OpenAI API account (₹400 free credit for new users)
3. ✅ Trello account
4. ✅ Slack workspace
5. ✅ Google Cloud account (for Sheets API)
6. ✅ n8n Cloud account OR local installation

### Estimated Setup Time:
- **First-time setup:** 45-60 minutes
- **If you have accounts:** 20-30 minutes
- **Testing:** 15 minutes

---

## 2️⃣ API ACCOUNTS SETUP (STEP-BY-STEP)

### A) Gmail Setup for IMAP & SMTP

**Step 1: Enable IMAP in Gmail**
```
1. Open Gmail (https://gmail.com)
2. Click Settings (gear icon) → See all settings
3. Go to "Forwarding and POP/IMAP" tab
4. Under "IMAP access", select "Enable IMAP"
5. Click "Save Changes" at bottom
```

**Step 2: Generate App Password**
```
1. Go to Google Account: https://myaccount.google.com
2. Navigate to Security section
3. Enable "2-Step Verification" (if not already enabled)
   - Click "2-Step Verification"
   - Follow setup wizard (requires phone number)
   - Verify your identity

4. Once 2-Step is enabled, go back to Security
5. Find "App passwords" (under "2-Step Verification")
6. Click "App passwords"
7. Select app: "Mail"
8. Select device: "Other (Custom name)"
9. Enter name: "n8n Smart Inbox Triager"
10. Click "Generate"
11. COPY the 16-character password (example: abcd efgh ijkl mnop)
12. SAVE THIS PASSWORD - you'll need it later!
```

**Important Notes:**
- Don't use your regular Gmail password in n8n
- App password format: 16 characters, no spaces when entering in n8n
- Keep this password secure and private

---

### B) OpenAI API Setup

**Step 1: Create OpenAI Account**
```
1. Visit: https://platform.openai.com/signup
2. Click "Sign up"
3. Enter email or use Google/Microsoft sign-in
4. Verify your email address
5. Complete profile setup (name, organization)
```

**Step 2: Add Payment Method**
```
1. Go to: https://platform.openai.com/account/billing
2. Click "Add payment method"
3. Enter credit/debit card details
4. Add ₹400 (minimum) for credits
   - This gives you ~200,000 API calls
   - Enough for 6+ months of testing
```

**Step 3: Generate API Key**
```
1. Go to: https://platform.openai.com/api-keys
2. Click "+ Create new secret key"
3. Name: "n8n Smart Inbox Triager"
4. Permissions: "All" (default)
5. Click "Create secret key"
6. COPY the key (starts with "sk-...")
   Example: sk-proj-abc123xyz789...
7. SAVE IMMEDIATELY - you can't view it again!
8. Store securely (use password manager)
```

**API Key Format:**
```
sk-proj-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
(Total length: ~51 characters)
```

**Cost Estimation:**
- GPT-4 Turbo: ~₹0.02 per email classification
- 100 emails/day = ₹2/day = ₹60/month
- 1000 emails/day = ₹20/day = ₹600/month

---

### C) Trello API Setup

**Step 1: Create Trello Account**
```
1. Visit: https://trello.com/signup
2. Sign up with email or Google
3. Verify email address
4. Skip team creation (click "Skip for now")
```

**Step 2: Create Board and Lists**
```
1. Click "+ Create new board"
2. Board name: "Email Triage System"
3. Workspace: "Personal" (or create new)
4. Background: Choose any
5. Click "Create"

6. Create lists (by default you have 3, rename them):
   - List 1: "Support Queue" (for support tickets)
   - List 2: "Sales Pipeline" (for sales leads)
   - List 3: "Completed" (for resolved items)
```

**Step 3: Get Trello API Key**
```
1. Visit: https://trello.com/power-ups/admin
2. Click "New" → "Create Power-Up"
3. Enter name: "n8n Integration"
4. Workspace: Select your workspace
5. Click "Create"
6. Copy your API Key (long string of letters/numbers)
   Example: a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6
7. SAVE THIS KEY
```

**Step 4: Generate Trello Token**
```
1. On same page, look for "Token" link
2. Click "generate a Token"
3. Click "Allow" to grant permissions
4. Copy the Token (another long string)
   Example: 1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef
5. SAVE THIS TOKEN
```

**Step 5: Get Board and List IDs**
```
1. Open your "Email Triage System" board
2. Add ".json" to the URL:
   From: https://trello.com/b/ABC123/email-triage-system
   To: https://trello.com/b/ABC123/email-triage-system.json
   
3. Press Enter - you'll see JSON data
4. Find: "id" near the top - this is your BOARD ID
   Example: "id": "5f9a8b7c6d5e4f3a2b1c0d9e"
   
5. Find "lists" section in JSON
6. Find your list names and copy their IDs:
   - "Support Queue" → id: "abc123..."
   - "Sales Pipeline" → id: "xyz789..."
   
7. SAVE THESE IDs
```

---

### D) Slack Webhook Setup

**Step 1: Create Slack Workspace (if needed)**
```
1. Visit: https://slack.com/get-started
2. Enter email → Click "Continue"
3. Check email for 6-digit code
4. Enter code
5. Create workspace name: "My Team" (or any name)
6. Add team members (skip for now)
```

**Step 2: Create Channels**
```
1. In Slack, click "+" next to "Channels"
2. Create channel: "#support"
   - Name: support
   - Make it public
   - Click "Create"
   
3. Create channel: "#sales"
   - Name: sales
   - Make it public
   - Click "Create"
```

**Step 3: Create Incoming Webhooks**
```
1. Visit: https://api.slack.com/apps
2. Click "Create New App"
3. Choose "From scratch"
4. App Name: "n8n Email Triager"
5. Workspace: Select your workspace
6. Click "Create App"

7. In left sidebar, click "Incoming Webhooks"
8. Toggle "Activate Incoming Webhooks" to ON

9. Click "Add New Webhook to Workspace"
10. Select channel: #support
11. Click "Allow"
12. COPY the Webhook URL (long URL starting with https://hooks.slack.com/...)
    Example: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXX
13. SAVE THIS URL (this is for Support)

14. Repeat steps 9-13 for #sales channel:
    - Click "Add New Webhook to Workspace" again
    - Select channel: #sales
    - Copy and SAVE the second webhook URL
```

**You should now have:**
- ✅ Support Webhook URL
- ✅ Sales Webhook URL

---

### E) Google Sheets API Setup

**Step 1: Create Google Sheet**
```
1. Visit: https://sheets.google.com
2. Click "+ Blank" to create new sheet
3. Name it: "Email Metrics Dashboard"
4. Create headers in first row:
   A1: Timestamp
   B1: Category
   C1: Urgency
   D1: Sentiment
   E1: Priority_Score
   F1: Sender_Email
   G1: Subject
   H1: Response_Time_Seconds
```

**Step 2: Get Sheet ID**
```
1. Look at the URL of your sheet:
   https://docs.google.com/spreadsheets/d/SHEET_ID_HERE/edit
   
2. Copy the SHEET_ID part (between /d/ and /edit)
   Example: 1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms
   
3. SAVE THIS ID
```

**Step 3: Enable Google Sheets API**
```
For n8n Cloud: No additional setup needed, OAuth will handle it

For Self-Hosted n8n:
1. Visit: https://console.cloud.google.com
2. Create new project: "n8n Integration"
3. Enable Google Sheets API:
   - Search "Google Sheets API"
   - Click "Enable"
4. Create OAuth credentials:
   - Go to "Credentials"
   - Create OAuth 2.0 Client ID
   - Application type: Web application
   - Name: "n8n"
   - Authorized redirect URIs: http://localhost:5678/rest/oauth2-credential/callback
   - Copy Client ID and Client Secret
```

---

## 3️⃣ N8N INSTALLATION

### Option A: n8n Cloud (Recommended for Beginners)

**Pros:** Easy setup, no maintenance, automatic updates  
**Cons:** Paid after trial (₹1,600/month)

```
1. Visit: https://n8n.cloud
2. Click "Start for free"
3. Sign up with email or Google
4. Verify email
5. Choose plan: Start with "Free Trial" (14 days)
6. You'll be taken to n8n dashboard
7. Ready to import workflow!
```

---

### Option B: Self-Hosted n8n (FREE Forever)

**Pros:** Free, full control, privacy  
**Cons:** Requires technical setup

#### Method 1: Using npx (Easiest for testing)

```bash
# Open Terminal (Mac/Linux) or Command Prompt (Windows)

# Run n8n with npx (no installation needed)
npx n8n

# Output will show:
# n8n ready on http://localhost:5678
```

**Access:** Open browser → http://localhost:5678

---

#### Method 2: Using Docker (Best for production)

**Prerequisites:** Install Docker Desktop first

**Windows:**
```
1. Download Docker Desktop: https://www.docker.com/products/docker-desktop
2. Install and restart computer
3. Open Docker Desktop
```

**Mac:**
```
1. Download Docker Desktop for Mac
2. Install .dmg file
3. Open Docker from Applications
```

**Run n8n:**
```bash
# Create folder for n8n data
mkdir ~/.n8n

# Run n8n container
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

**Access:** Open browser → http://localhost:5678

---

#### Method 3: Using npm (For developers)

```bash
# Install Node.js first: https://nodejs.org (v18 or higher)

# Install n8n globally
npm install -g n8n

# Run n8n
n8n

# Access: http://localhost:5678
```

---

## 4️⃣ WORKFLOW IMPORT PROCESS

### Step 1: Download Workflow File

```
1. Locate the file: "Smart_Inbox_Triager_Workflow.json"
2. Save it to your Downloads folder
3. Do NOT open or edit the file
```

### Step 2: Import into n8n

```
1. Open n8n (cloud or local)
2. Look for "Workflows" in left sidebar
3. Click the "+" button or "Import from File"
4. Click "Import from File" button
5. Select "Smart_Inbox_Triager_Workflow.json"
6. Wait for upload (should be instant)
7. Workflow will open in editor
```

### Step 3: Verify Import

```
✅ Check you see 14 nodes in the canvas
✅ Nodes should be connected with lines
✅ No error icons on nodes yet (credentials not added)
```

---

## 5️⃣ CREDENTIAL CONFIGURATION

### A) Gmail Credentials

**Step 1: Add Gmail IMAP Credential**
```
1. Click on "Gmail Trigger" node (first node)
2. In right panel, find "Credential to connect with"
3. Click dropdown → "+ Create New Credential"
4. Choose "IMAP"
5. Fill in:
   - Host: imap.gmail.com
   - Port: 993
   - User: your-email@gmail.com
   - Password: [Your 16-digit App Password]
   - SSL/TLS: Enable (checked)
6. Click "Create"
7. Click "Test" to verify connection
8. Should show green "Success" message
```

**Step 2: Add Gmail OAuth2 for Sending**
```
1. Click on "Send Support Auto-Reply" node
2. Credential type: "Gmail OAuth2"
3. Click "+ Create New Credential"
4. Click "Connect my account"
5. Sign in with Google
6. Allow n8n permissions
7. Should redirect back to n8n
8. Click "Save"
```

---

### B) OpenAI Credentials

```
1. Click "AI Classification (OpenAI)" node
2. Find "Authentication" section
3. Choose "Header Auth"
4. OR use built-in "OpenAI" credential type
5. Click "+ Create New Credential"
6. API Key: [Paste your sk-proj-... key]
7. Click "Create"
8. Node should turn green (no error)
```

---

### C) Trello Credentials

```
1. Click "Create Support Ticket" node
2. Click "+ Create New Credential" for Trello
3. Fill in:
   - API Key: [Your Trello API key]
   - API Token: [Your Trello token]
4. Click "Create"
5. Test connection by clicking "Test"

6. Configure Board and List:
   - Board ID: [Your board ID from earlier]
   - List ID: [Your "Support Queue" list ID]
   
7. Repeat for "Create Sales Lead" node:
   - Use same Trello credential
   - Board ID: Same as above
   - List ID: [Your "Sales Pipeline" list ID]
```

---

### D) Slack Webhooks

```
1. Click "Slack Alert - Support" node
2. In node parameters:
   - Method: POST
   - URL: [Paste your Support webhook URL]
3. No credential needed (webhook is self-authenticated)

4. Click "Slack Alert - Sales" node
5. URL: [Paste your Sales webhook URL]
```

---

### E) Google Sheets

```
1. Click "Log to Google Sheets" node
2. Click "+ Create New Credential"
3. Choose "Google Sheets OAuth2"
4. Click "Connect my account"
5. Sign in with Google
6. Allow permissions
7. Should redirect back

8. Configure node:
   - Document ID: [Your Sheet ID]
   - Sheet Name: "Sheet1" (or your sheet name)
   - Operation: Append
```

---

## 6️⃣ ENVIRONMENT VARIABLES

### Create .env File (For Self-Hosted Only)

```bash
# Create file: .env in n8n directory

# Gmail
GMAIL_USER=your-email@gmail.com
GMAIL_APP_PASSWORD=your16digitpassword

# OpenAI
OPENAI_API_KEY=sk-proj-your-api-key-here

# Trello
TRELLO_API_KEY=your-trello-api-key
TRELLO_TOKEN=your-trello-token
TRELLO_BOARD_ID=your-board-id
TRELLO_SUPPORT_LIST_ID=your-support-list-id
TRELLO_SALES_LIST_ID=your-sales-list-id

# Slack
SLACK_WEBHOOK_SUPPORT=https://hooks.slack.com/services/YOUR/SUPPORT/WEBHOOK
SLACK_WEBHOOK_SALES=https://hooks.slack.com/services/YOUR/SALES/WEBHOOK

# Google Sheets
GOOGLE_SHEET_ID=your-sheet-id
```

**Load Environment Variables:**
```bash
# For npx/npm:
export $(cat .env | xargs)
n8n

# For Docker:
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  --env-file .env \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

---

## 7️⃣ TESTING PROCEDURES

### Pre-Flight Checklist

```
□ All 14 nodes show green (no red errors)
□ All credentials configured
□ Trello board created with lists
□ Slack channels created
□ Google Sheet created with headers
```

### Test 1: High-Priority Support Email

**Step 1: Prepare Test Email**
```
1. From a different email account (not the monitored one)
2. Send email to: [your monitored Gmail address]

Subject: URGENT: Cannot access my account!!!

Body:
I've been locked out of my account for 3 hours now. 
This is completely unacceptable! I need immediate help.
My user ID is: testuser12345
This is blocking critical work.
```

**Step 2: Trigger Workflow**
```
1. In n8n, click "Execute Workflow" button (top right)
2. OR wait 30 seconds for automatic trigger
3. Watch nodes light up as they execute
```

**Step 3: Verify Results**
```
✅ Check Trello: 
   - New card in "Support Queue"
   - Title: 🚨 URGENT: Cannot access my account!!!
   - Description has AI summary
   - Labels show HIGH priority

✅ Check Gmail:
   - Reply email sent to test sender
   - Professional HTML format
   - Includes ticket details

✅ Check Slack:
   - Message in #support channel
   - Shows urgency and sentiment
   - Has "View Ticket" button

✅ Check Google Sheets:
   - New row with all data
   - Timestamp, category, urgency, etc.
```

**Expected Execution Time:** 8-15 seconds

---

### Test 2: Sales Inquiry Email

**Send Email:**
```
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

**Verify:**
```
✅ Trello card in "Sales Pipeline"
✅ Auto-reply with pricing info
✅ Slack notification in #sales
✅ Google Sheets logged
```

---

### Test 3: Spam Email

**Send Email:**
```
Subject: 🎉 YOU WON $1,000,000! Click Now!!!

Body:
Congratulations! You've been selected as our lucky winner!
Click here immediately to claim your prize!!!
```

**Verify:**
```
✅ No Trello card created
✅ No auto-reply sent
✅ No Slack notification
✅ Logged in Google Sheets as "spam"
```

---

### Test 4: Edge Case - Ambiguous Email

**Send Email:**
```
Subject: Question

Body:
Hi, can you help?
```

**Expected:**
```
✅ Should classify as "support" (default fallback)
✅ AI summary: "Vague request needs clarification"
✅ Medium priority
✅ All actions execute normally
```

---

## 8️⃣ TROUBLESHOOTING GUIDE

### Issue 1: Gmail Trigger Not Working

**Symptoms:** No emails being detected

**Solutions:**
```
1. Check IMAP is enabled in Gmail settings
2. Verify App Password (not regular password)
3. Check n8n can reach imap.gmail.com:993
4. Test credential connection
5. Check spam/promotions folders aren't being checked
6. Manually trigger workflow: Click "Execute Workflow"
```

**Test Command:**
```bash
# Test IMAP connection
telnet imap.gmail.com 993
# Should connect, press Ctrl+C to exit
```

---

### Issue 2: OpenAI API Errors

**Error:** "Invalid API key" or "Insufficient quota"

**Solutions:**
```
1. Verify API key starts with "sk-proj-"
2. Check you have credits: https://platform.openai.com/account/billing
3. Add payment method if needed
4. Regenerate API key if compromised
5. Check API key permissions
```

**Check Balance:**
```
Visit: https://platform.openai.com/account/usage
Look for: Credits remaining
```

---

### Issue 3: Trello Card Not Created

**Error:** "Board or list not found"

**Solutions:**
```
1. Verify Board ID is correct:
   - Go to board URL
   - Add .json to URL
   - Copy "id" field

2. Verify List ID:
   - Same JSON, find "lists" array
   - Match list name to ID

3. Check Trello API token hasn't expired:
   - Regenerate if needed
   
4. Verify board permissions:
   - Make sure board is not private
   - Or token has board access
```

---

### Issue 4: Slack Webhook Failed

**Error:** "Invalid webhook URL" or "channel_not_found"

**Solutions:**
```
1. Regenerate webhook:
   - https://api.slack.com/apps
   - Select your app
   - Incoming Webhooks
   - Generate new webhook

2. Test webhook with curl:
curl -X POST \
  -H 'Content-Type: application/json' \
  -d '{"text":"Test from terminal"}' \
  YOUR_WEBHOOK_URL

3. Check channel still exists
4. Verify webhook is for correct workspace
```

---

### Issue 5: AI Returns Invalid JSON

**Error:** "Unexpected token in JSON"

**Solution in Parse Node:**
```javascript
// Already included in workflow:
try {
  const clean = content.replace(/```json|```/g, '').trim();
  const result = JSON.parse(clean);
  return result;
} catch (error) {
  // Fallback classification
  return {
    category: "support",
    summary: "AI parsing failed - manual review needed",
    urgency: "medium",
    sentiment: "neutral",
    priority_score: 5
  };
}
```

---

### Issue 6: Google Sheets Permission Error

**Error:** "Insufficient permissions"

**Solutions:**
```
1. Re-authenticate OAuth:
   - Delete credential
   - Create new
   - Sign in again
   - Allow all permissions

2. Check sheet isn't deleted
3. Verify Sheet ID is correct
4. Make sure you own the sheet
```

---

### Issue 7: Workflow Times Out

**Error:** "Workflow execution timed out"

**Solutions:**
```
1. Increase timeout in n8n settings:
   Settings → Executions → Timeout: 60 seconds

2. Check internet connection
3. Verify all APIs are responding:
   - OpenAI status: status.openai.com
   - Trello status: trello.status.atlassian.com
   - Slack status: status.slack.com

4. Reduce max tokens in OpenAI node (500 → 300)
```

---

## 9️⃣ PRODUCTION DEPLOYMENT

### For n8n Cloud:

```
1. Activate workflow:
   - Toggle switch at top: OFF → ON
   - Workflow will now run automatically

2. Monitor executions:
   - Click "Executions" tab
   - View success/failure history
   
3. Set up error notifications:
   - Add error workflow
   - Configure alerts to Slack/email
```

### For Self-Hosted:

**Option 1: Keep Terminal Open**
```bash
# Simple but not ideal
npx n8n
# Keep this terminal window open
```

**Option 2: Use PM2 (Recommended)**
```bash
# Install PM2
npm install -g pm2

# Start n8n with PM2
pm2 start n8n

# Set to start on boot
pm2 startup
pm2 save

# Manage:
pm2 status        # Check status
pm2 logs n8n      # View logs
pm2 restart n8n   # Restart
pm2 stop n8n      # Stop
```

**Option 3: Docker Compose (Best)**

Create `docker-compose.yml`:
```yaml
version: '3.7'

services:
  n8n:
    image: n8nio/n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=your-password
      - N8N_HOST=localhost
      - N8N_PORT=5678
      - N8N_PROTOCOL=http
      - NODE_ENV=production
      - WEBHOOK_URL=http://localhost:5678/
    volumes:
      - ~/.n8n:/home/node/.n8n
```

Run:
```bash
docker-compose up -d
```

---

### Securing Your Installation:

**1. Add Basic Authentication:**
```bash
# Set environment variables
export N8N_BASIC_AUTH_ACTIVE=true
export N8N_BASIC_AUTH_USER=admin
export N8N_BASIC_AUTH_PASSWORD=StrongPassword123!

n8n
```

**2. Use HTTPS (with reverse proxy):**
```
Install nginx or Caddy
Configure SSL certificate
Point to n8n port 5678
```

**3. Firewall Rules:**
```bash
# Only allow connections from your IP
ufw allow from YOUR_IP to any port 5678
ufw enable
```

---

## 🔟 MONITORING & MAINTENANCE

### Daily Checks:

```
□ Check execution logs for failures
□ Monitor API usage/costs
□ Review classification accuracy
□ Check Google Sheets for anomalies
```

### Weekly Tasks:

```
□ Review error rate in n8n
□ Analyze sentiment trends
□ Update AI prompt if needed
□ Check API credit balance
□ Backup workflow JSON
```

### Monthly Review:

```
□ Calculate ROI and time saved
□ Review team feedback
□ Optimize prompt for better accuracy
□ Plan new features/integrations
□ Update documentation
```

---

### Metrics Dashboard:

**Create in Google Sheets:**
```
1. Open your Email Metrics sheet
2. Create pivot table:
   - Rows: Category
   - Values: COUNTA (count)
   - Create pie chart

3. Average response time:
   =AVERAGE(H:H)

4. Sentiment breakdown:
   - Positive count: =COUNTIF(D:D,"positive")
   - Negative count: =COUNTIF(D:D,"negative")
   - Angry count: =COUNTIF(D:D,"angry")

5. Urgency distribution:
   - High: =COUNTIF(C:C,"high")
   - Medium: =COUNTIF(C:C,"medium")
   - Low: =COUNTIF(C:C,"low")
```

---

### Backup Procedures:

**Export Workflow:**
```
1. In n8n, open workflow
2. Click ⋮ (three dots) → Download
3. Save: Smart_Inbox_Triager_Backup_YYYY-MM-DD.json
4. Store in cloud (Google Drive, Dropbox)
```

**Backup Credentials (Securely):**
```
1. Use password manager (1Password, Bitwarden)
2. Store all API keys
3. Document which key is for what
4. Include creation date
5. Set reminder to rotate keys every 90 days
```

---

## ✅ FINAL CHECKLIST

### Before Going Live:

```
□ All tests passed (Support, Sales, Spam)
□ Credentials secured (not in workflow JSON)
□ Error handling verified
□ Team trained on Trello/Slack
□ Backup workflow saved
□ Monitoring dashboard created
□ Documentation reviewed
□ Contact info updated
□ Emergency rollback plan ready
```

---

## 📞 SUPPORT & RESOURCES

**Developer Contact:**
- Name: Soumya Das
- Email: soumyadastopper2006@gmail.com
- Phone: +91 8159824282

**Official Documentation:**
- n8n Docs: https://docs.n8n.io
- OpenAI API: https://platform.openai.com/docs
- Trello API: https://developer.atlassian.com/cloud/trello
- Slack API: https://api.slack.com

**Community Support:**
- n8n Community: https://community.n8n.io
- n8n Discord: https://discord.gg/n8n

---

**Document Version:** 1.0  
**Last Updated:** November 21, 2025  
**Status:** Production Ready  
**License:** MIT
