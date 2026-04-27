# GHL Custom Fields Setup
# Build #1: 24/7 AI Voice Intake Agent

Create these custom fields in GoHighLevel under Settings > Custom Fields > Contacts.

## Required Custom Fields

| Field Name | API Key | Type |
|-----------|---------|------|
| Accident Type | accident_type | Dropdown |
| Injury Present | injury_present | Checkbox |
| Injury Severity | injury_severity | Dropdown |
| At Fault Party | at_fault_party | Text |
| Insurance Present | insurance_present | Checkbox |
| Insurance Type | insurance_type | Text |
| Incident Date | incident_date | Date |
| Days Since Incident | days_since_incident | Number |
| Has Existing Attorney | has_existing_attorney | Checkbox |
| Lead Score | lead_score | Number |
| Lead Status | lead_status | Dropdown |
| Call Recording URL | recording_url | URL |
| Call Transcript | call_transcript | Text Area |
| Retell Call ID | retell_call_id | Text |
| Intake Source | intake_source | Dropdown |

## How to Create Custom Fields in GHL

1. Go to Settings (gear icon)
2. Click Custom Fields in left sidebar
3. Click + Add Field
4. Select Contact as the object
5. Fill in Label, API Key, and Type
6. Click Save

## GHL Tags to Create

- voice-intake - All calls from Retell AI
- hot-lead - Lead score >= 60
- warm-lead - Lead score 35-59
- cold-lead - Lead score < 35
- auto-accident, slip-fall, workplace-injury, medical-malpractice
- needs-attorney-call - Hot leads awaiting attorney call
- in-nurture - Cold leads in nurture sequence

## Smart List Views to Create

### Hot Leads Today
- Filter: Lead Status = hot, Created Date = today
- Sort: Lead Score (highest first)

### Active Nurture
- Filter: Lead Status = cold OR warm, Tag contains in-nurture

### Awaiting Attorney Call
- Filter: Tag contains needs-attorney-call
- Sort: Created Date (oldest first)
