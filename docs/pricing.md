# Pricing & Deliverables
# Build #1: 24/7 AI Voice Intake Agent

---

## Pricing Summary

| Item | Cost |
|------|------|
| Setup Fee (one-time) | $3,500 |
| Monthly Retainer | $1,200/month |

---

## Setup Fee - $3,500 (One-Time)

### What Is Delivered

**1. Retell AI Agent Configuration**
- Custom AI voice agent built with your firm name and branding
- Full intake script programmed and tested (accident type, injuries, fault, insurance, contact info)
- Voice and tone calibrated for legal intake (professional, empathetic)
- AnythingLLM knowledge base loaded with firm-specific context (FAQs, practice areas, jurisdiction)
- Mem0 integration for returning caller recognition

**2. n8n Workflow Build & Deployment**
- Webhook endpoint configured to receive Retell AI call-end events
- Lead scoring algorithm (40 variables, 0-100 scale)
- Hot/warm/cold routing logic
- GHL contact creation/update via API
- Attorney SMS alert for hot leads
- Pipeline opportunity creation
- Error handling and logging

**3. GoHighLevel Configuration**
- 15 custom fields created and mapped
- Intake pipeline created with 5 stages:
  - New Voice Lead
  - Hot Lead - Needs Call
  - In Consultation
  - Client Signed
  - Not Qualified
- 5 SMS templates created and tested
- 2 email templates created and tested
- Cold lead nurture sequence automated (14-day, 7 touchpoints)
- Hot lead workflow automated
- Smart list views configured

**4. Testing & QA**
- 10 test calls across different lead scenarios
- Scoring validation for all lead types
- GHL data population verification
- SMS/email delivery confirmation

**5. Documentation**
- Full setup guide (this repo)
- Agent prompt documentation
- Environment variable reference
- Handoff call (1 hour) with your team

**6. 30-Day Post-Launch Support**
- Bug fixes at no additional charge
- Up to 3 hours of minor adjustments
- Weekly check-in for first 30 days

---

## Monthly Retainer - $1,200/month

### What Is Included

**Monitoring & Maintenance**
- Weekly workflow health checks
- Alert if webhook failures occur
- GHL automation verification
- Retell AI uptime monitoring

**Optimization**
- Monthly review of lead scoring accuracy
- Agent prompt refinements based on call quality
- A/B testing of SMS/email templates
- Conversion rate analysis

**Reporting**
- Monthly performance dashboard (PDF)
  - Total calls answered
  - Lead breakdown (hot/warm/cold %)
  - Attorney response times
  - Conversion rates by lead source
  - Estimated ROI

**Change Requests**
- Up to 5 hours/month of changes included:
  - Workflow modifications
  - New SMS/email templates
  - Pipeline stage adjustments
  - New qualification questions
  - Additional attorney routing rules

**Priority Support**
- Response within 4 business hours
- Emergency support for workflow failures
- Direct Slack channel access

---

## Third-Party Costs (Client Responsibility)

These costs are separate and billed directly to the client by each platform:

| Service | Estimated Cost | Notes |
|---------|----------------|-------|
| Retell AI | $0.07-0.11/min | ~300-500 calls/mo = $150-250/mo |
| GoHighLevel | $97-$297/mo | Agency or Pro plan |
| n8n Cloud | $20-50/mo | Or self-hosted at ~$5-10/mo VPS |
| AnythingLLM | Free self-hosted | Or $0/mo cloud with own LLM keys |
| Mem0 | Free tier or $25/mo | Caller memory |
| Phone Number | ~$2-5/mo | Via Retell or Twilio |

**Estimated Total Platform Cost: ~$300-600/month**

---

## ROI Calculator

Based on average PI firm metrics:

- Average case value: $15,000-50,000 (attorney fee ~33%)
- Attorney fee per won case: $5,000-16,500
- If system captures just 1 additional case per month that would have been missed:
  - **Monthly ROI: $5,000-16,500**
  - **Against total cost of ~$1,800-1,900/mo: 3x-9x ROI**

---

## Contract Terms

- Setup fee due 50% upfront, 50% at launch
- Monthly retainer billed on the 1st of each month
- 3-month minimum commitment on retainer
- 30-day notice required to cancel after initial term
- All work product remains property of client upon full payment

---

## Upgrade Options

| Add-On | Cost |
|--------|------|
| Second attorney routing (multi-location) | +$500 setup, +$300/mo |
| Spanish-language agent | +$1,500 setup, +$200/mo |
| Custom lead scoring rules | +$500 one-time |
| Weekly reporting (enhanced) | +$200/mo |
| Additional practice area intake | +$800 setup |
