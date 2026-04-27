# Full Setup Guide
# Build #1: 24/7 AI Voice Intake Agent

---

## Prerequisites

Before starting, ensure you have accounts on:
- Retell AI (retellai.com)
- GoHighLevel (gohighlevel.com) - Agency or Pro plan
- n8n (n8n.io cloud or self-hosted)
- AnythingLLM (self-hosted or mintplexlabs.com)
- Mem0 (mem0.ai)

---

## Step 1: GoHighLevel Setup

### 1a. Create Custom Fields
Follow instructions in ghl/custom-fields.md

### 1b. Create Pipeline
1. Go to CRM > Pipelines
2. Click + New Pipeline
3. Name it: Voice Intake Pipeline
4. Create stages:
   - New Voice Lead
   - Hot Lead - Needs Call
   - In Consultation
   - Client Signed
   - Not Qualified
5. Save and note the Pipeline ID from the URL

### 1c. Get API Credentials
1. Go to Settings > Integrations > API Keys
2. Create new API key with full access
3. Copy the API key and Location ID
4. Store in your .env file as GHL_API_KEY and GHL_LOCATION_ID

### 1d. Create SMS/Email Templates
Follow instructions in ghl/sms-templates.md

---

## Step 2: AnythingLLM Setup

### 2a. Install AnythingLLM
Option A (Docker):
docker pull mintplexlabs/anythingllm
docker run -d -p 3001:3001 mintplexlabs/anythingllm

Option B: Use cloud version at useanything.com

### 2b. Create Workspace
1. Open AnythingLLM at http://localhost:3001
2. Create workspace named: law-firm-intake
3. Upload firm documents:
   - Practice areas PDF
   - Attorney bios
   - FAQ document
   - Geographic service areas

### 2c. Get API Key
1. Go to Settings > API Keys
2. Create new API key
3. Copy workspace slug and API key
4. Store in .env as ANYTHINGLLM_API_KEY and ANYTHINGLLM_WORKSPACE

---

## Step 3: Mem0 Setup

### 3a. Get API Key
1. Go to app.mem0.ai
2. Create account and go to API Keys
3. Copy your API key
4. Store in .env as MEM0_API_KEY

---

## Step 4: n8n Setup

### 4a. Import Workflow
1. Open your n8n instance
2. Go to Workflows > Import
3. Upload n8n/workflow-intake.json
4. The workflow will appear with all nodes

### 4b. Configure Credentials
1. In n8n, go to Settings > Credentials
2. Create HTTP Header Auth credential named GHL-API
   - Header: Authorization
   - Value: Bearer YOUR_GHL_API_KEY
3. Update environment variables in Settings > Environment Variables

### 4c. Set Environment Variables in n8n
GHL_API_KEY=your_ghl_api_key
GHL_LOCATION_ID=your_ghl_location_id
GHL_PIPELINE_ID=your_pipeline_id
GHL_HOT_LEAD_STAGE_ID=hot_lead_stage_id
GHL_COLD_LEAD_STAGE_ID=cold_lead_stage_id
GHL_ATTORNEY_CONTACT_ID=attorney_ghl_contact_id
GHL_PORTAL_URL=https://app.gohighlevel.com

### 4d. Activate Workflow
1. Click the toggle to activate the workflow
2. Note the webhook URL (displayed when webhook node is active)
3. Should look like: https://your-n8n.com/webhook/retell-intake

---

## Step 5: Retell AI Setup

### 5a. Create Agent
1. Go to app.retellai.com
2. Click + Create Agent
3. Select LLM type: Custom LLM (for AnythingLLM) or OpenAI

### 5b. Configure System Prompt
1. Open retell/agent-prompt.md from this repo
2. Replace [FIRM NAME] with your firm name
3. Paste full prompt into Retell agent system prompt field

### 5c. Configure Post-Call Webhook
1. In Retell agent settings, go to Post-Call Webhook
2. Enter your n8n webhook URL: https://your-n8n.com/webhook/retell-intake
3. Set webhook secret (store as RETELL_WEBHOOK_SECRET in n8n)

### 5d. Configure Custom Data Extraction
In Retell agent settings, add these extraction fields:
- caller_name (string)
- caller_email (string)
- accident_type (string)
- injuries_present (boolean)
- injury_severity (string)
- at_fault_party_identified (boolean)
- at_fault_description (string)
- insurance_present (boolean)
- insurance_type (string)
- incident_date_approx (string)
- days_since_incident (number)
- has_existing_attorney (boolean)

### 5e. Assign Phone Number
1. In Retell dashboard, go to Phone Numbers
2. Purchase a number or connect Twilio
3. Assign to your intake agent

### 5f. Test the Agent
1. Call your Retell number
2. Complete a full intake interview
3. Check n8n execution log
4. Verify GHL contact was created
5. Verify SMS was sent (if hot lead)

---

## Step 6: Call Forwarding Setup

### Option A: Simple Forwarding
Have the law firm forward their after-hours calls to the Retell number.

### Option B: Time-Based Routing (GHL)
1. In GHL, go to Phone Numbers
2. Set business hours
3. After hours: forward to Retell number
4. During hours: ring to receptionist first, then Retell

---

## Step 7: Testing Checklist

Run these test scenarios:

Hot Lead Test:
- Say you were in a car accident
- Report moderate injuries
- Identify an at-fault driver
- Confirm you have insurance
- Incident was 2 weeks ago
Expected: Score >= 60, attorney SMS sent, Hot Lead pipeline stage

Cold Lead Test:
- Say you had a slip and fall
- No significant injuries
- Unsure who is at fault
- No insurance info
- Incident was 6 months ago
Expected: Score < 35, cold lead nurture sequence started

Returning Caller Test:
- Call twice with same number
- Second call should recognize you via Mem0
Expected: Agent references previous call

---

## Troubleshooting

### n8n webhook not receiving data
- Verify Retell webhook URL is correct
- Check n8n workflow is activated (not just saved)
- Check n8n execution log for errors

### GHL contact not created
- Verify GHL_API_KEY is valid
- Check GHL_LOCATION_ID is correct
- Look at n8n execution log for API response

### SMS not sending to attorney
- Verify GHL_ATTORNEY_CONTACT_ID is the attorney's GHL contact ID
- Check attorney phone number is valid in GHL contact
- Verify GHL SMS settings are configured

### Lead score always 0
- Check Retell custom data extraction is configured
- Verify field names match exactly
- Review n8n code node for parsing errors
