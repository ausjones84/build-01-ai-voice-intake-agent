# GHL SMS & Email Templates
# Build #1: 24/7 AI Voice Intake Agent

Create these templates in GHL under Marketing > Templates.

---

## SMS Templates

### 1. Hot Lead Attorney Alert (Sent via n8n webhook)
**Template Name:** hot-lead-attorney-alert
**Trigger:** n8n workflow (not GHL automation)

Message:
HOT LEAD ALERT
Name: {{contact.firstName}} {{contact.lastName}}
Phone: {{contact.phone}}
Accident: {{contact.accident_type}}
Injuries: {{contact.injury_severity}}
Score: {{contact.lead_score}}/100

Call them NOW. They just called our intake line.

---

### 2. Intake Confirmation SMS (Day 0 - Cold/Warm Leads)
**Template Name:** intake-confirmation-sms

Message:
Hi {{contact.firstName}}, this is [FIRM NAME]. Thank you for calling about your case. Our team is reviewing your information and will follow up within 1 business day. Questions? Call us at [FIRM PHONE].

---

### 3. Day 3 Check-In SMS
**Template Name:** day3-checkin-sms

Message:
Hi {{contact.firstName}}, this is [ATTORNEY NAME] from [FIRM NAME]. I personally reviewed your case details from your recent call. I'd love to connect with you. Reply YES to schedule a free 15-min call, or call us at [FIRM PHONE].

---

### 4. Day 7 Re-Engagement SMS
**Template Name:** day7-reengagement-sms

Message:
{{contact.firstName}}, we haven't forgotten about you. Accident cases have strict time limits. Our attorneys have recovered millions for clients in similar situations. Ready to talk? Call [FIRM PHONE] or reply CALL ME.

---

### 5. Day 14 Final Attempt SMS
**Template Name:** day14-final-sms

Message:
Hi {{contact.firstName}}, this is our final follow-up from [FIRM NAME]. If you're still dealing with your accident situation, we're here to help - at NO cost unless we win. Call [FIRM PHONE] anytime. We answer 24/7.

---

## Email Templates

### 1. Day 1 Case Evaluation Email
**Template Name:** day1-case-evaluation
**Subject:** Your Case Evaluation from [FIRM NAME]

Hi {{contact.firstName}},

Thank you for calling [FIRM NAME] about your recent incident. We take every case seriously and want to make sure you get the representation you deserve.

Based on your call, here's what you should know:

TIME IS CRITICAL - Most personal injury cases have a statute of limitations. The sooner you act, the stronger your case.

NO COST TO YOU - We work on contingency. You pay nothing unless we win your case.

EXPERIENCED TEAM - Our attorneys have recovered millions for clients just like you.

NEXT STEP: Click below to schedule your free consultation.

[SCHEDULE CONSULTATION BUTTON]

Or call us directly: [FIRM PHONE]

Best regards,
[ATTORNEY NAME]
[FIRM NAME]

---

### 2. Day 7 Social Proof Email
**Template Name:** day7-social-proof
**Subject:** See What Our Clients Are Saying, {{contact.firstName}}

Hi {{contact.firstName}},

We know you're going through a difficult time. Here's what clients in similar situations said about working with us:

[CLIENT TESTIMONIAL 1]
[CLIENT TESTIMONIAL 2]
[CLIENT TESTIMONIAL 3]

Ready to get started? Your consultation is FREE.

[SCHEDULE NOW BUTTON]

[FIRM NAME] | [FIRM PHONE]

---

## GHL Workflow Automation

### Cold Lead Nurture Sequence
Create this workflow in GHL Automations > Workflows:

Trigger: Tag Added > cold-lead OR warm-lead
Wait: Immediately
Action: Send SMS (intake-confirmation-sms)

Wait: 1 day
Action: Send Email (day1-case-evaluation)

Wait: 2 days
Action: Send SMS (day3-checkin-sms)

Wait: 4 days
Action: Send Email (day7-social-proof)

Wait: 7 days
Action: Send SMS (day7-reengagement-sms)

Wait: 7 days
Action: Send SMS (day14-final-sms)

End workflow.

### Hot Lead Pipeline Workflow
Trigger: Tag Added > hot-lead
Action: Move to Pipeline Stage "Hot Lead - Needs Call"
Action: Create Task "Call hot lead within 1 hour" (assigned to attorney)
Action: Add tag needs-attorney-call
End workflow.
