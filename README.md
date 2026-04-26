# Build #1: 24/7 AI Voice Intake Agent 🎙️

> **Stack:** Retell AI + GoHighLevel (GHL) + n8n + AnythingLLM + Mem0
> > **Problem Solved:** Law firms miss calls after hours — leads go cold
> > > **Pricing:** $3,500 Setup + $1,200/month
> > >
> > > ---
> > >
> > > ## Overview
> > >
> > > This build deploys a fully autonomous 24/7 AI voice intake agent for personal injury and general law firms. Every inbound call is answered by a trained AI agent that qualifies the lead, scores it, routes hot leads to attorneys via SMS, logs all data to GHL, and triggers automated nurture sequences for cold leads.
> > >
> > > ---
> > >
> > > ## Architecture
> > >
> > > ```
> > > Caller → Retell AI Voice Agent
> > >            ↓
> > >     Qualification Questions
> > >     (accident type, injuries, at-fault, insurance)
> > >            ↓
> > >     Lead Scoring Engine (n8n)
> > >            ↙          ↘
> > >   HOT LEAD           COLD LEAD
> > >   → SMS Alert        → GHL Nurture
> > >     to Attorney        Sequence
> > >   → GHL Contact      → Follow-up
> > >     Record Created     Emails/SMS
> > > ```
> > >
> > > ---
> > >
> > > ## Tech Stack
> > >
> > > | Component | Tool | Purpose |
> > > |-----------|------|---------|
> > > | Voice AI | Retell AI | Answers calls, conducts intake interview |
> > > | CRM | GoHighLevel (GHL) | Contact records, pipelines, automations |
> > > | Workflow | n8n | Webhook processing, routing logic |
> > > | Context | AnythingLLM | Firm-specific knowledge base for agent |
> > > | Memory | Mem0 | Caller memory — returning callers recognized |
> > >
> > > ---
> > >
> > > ## File Structure
> > >
> > > ```
> > > build-01-ai-voice-intake-agent/
> > > ├── README.md
> > > ├── retell/
> > > │   ├── agent-prompt.md          # Full system prompt for Retell AI agent
> > > │   └── agent-config.json        # Retell agent configuration
> > > ├── n8n/
> > > │   ├── workflow-intake.json     # Main n8n workflow (import directly)
> > > │   └── workflow-nurture.json    # Cold lead nurture workflow
> > > ├── ghl/
> > > │   ├── custom-fields.md         # GHL custom fields to create
> > > │   ├── pipeline-setup.md        # Pipeline stages configuration
> > > │   └── sms-templates.md         # SMS templates for hot lead alerts + nurture
> > > ├── anythingllm/
> > > │   └── knowledge-base-setup.md  # How to configure AnythingLLM context
> > > └── docs/
> > >     ├── setup-guide.md           # Full step-by-step setup instructions
> > >     └── pricing.md               # Pricing breakdown and deliverables
> > > ```
> > >
> > > ---
> > >
> > > ## How It Works — Step by Step
> > >
> > > ### 1. Call Received
> > > - Client's phone number forwards to Retell AI phone number
> > > - - Retell AI answers with custom voice agent (firm name, tone configured)
> > >  
> > >   - ### 2. Intake Interview (Retell AI)
> > >   - The agent asks qualification questions:
> > >   - - What type of accident or incident? (auto, slip/fall, medical, etc.)
> > >     - - Were there any injuries? (severity scale)
> > >       - - Who was at fault?
> > >         - - Is there active insurance coverage?
> > >           - - Has caller spoken with another attorney?
> > >             - - Contact info collection (name, phone, email)
> > >              
> > >               - ### 3. Lead Scoring (n8n)
> > >               - After call ends, Retell AI sends webhook to n8n with transcript + call data.
> > >              
> > >               - **Scoring Logic:**
> > >               - - +40 pts: Injury present
> > >                 - - +25 pts: Clear at-fault party identified
> > > - +20 pts: Active insurance coverage
> > > - - +15 pts: Recent incident (< 30 days)
> > >   - - -20 pts: Already has attorney
> > >     - - Score ≥ 60 = HOT LEAD → immediate attorney SMS
> > >       - - Score < 60 = COLD LEAD → nurture sequence
> > >        
> > >         - ### 4. GHL Contact Record (n8n → GHL API)
> > >         - n8n automatically creates/updates GHL contact with:
> > >         - - Full name, phone, email
> > >           - - Accident type (custom field)
> > >             - - Injury severity (custom field)
> > >               - - Lead score (custom field)
> > >                 - - Lead status: Hot / Warm / Cold (custom field)
> > >                   - - Call transcript (notes)
> > >                     - - Recording URL (custom field)
> > >                      
> > >                       - ### 5. Hot Lead Routing
> > >                       - - Attorney receives SMS: "🔥 HOT LEAD: [Name] — [Accident Type] — Score: [X]/100. Call now: [Phone]"
> > >                         - - GHL contact moved to "Hot Lead - Needs Call" pipeline stage
> > >                           - - 15-minute follow-up task created for attorney
> > >                            
> > >                             - ### 6. Cold Lead Nurture (GHL Automation)
> > >                             - - Day 0: SMS — "Thanks for calling [Firm]. We'll review your case and follow up soon."
> > >                               - - Day 1: Email — Case evaluation overview
> > >                                 - - Day 3: SMS — Check-in with attorney intro
> > >                                   - - Day 7: Email — Social proof + testimonials
> > >                                     - - Day 14: Final follow-up call attempt via GHL
> > >                                      
> > >                                       - ---
> > >
> > > ## Setup Instructions
> > >
> > > See [docs/setup-guide.md](docs/setup-guide.md) for full walkthrough.
> > >
> > > ### Quick Start
> > >
> > > 1. **Retell AI** — Create agent, import prompt from `retell/agent-prompt.md`, assign phone number
> > > 2. 2. **AnythingLLM** — Upload firm documents, configure API, add endpoint to Retell agent
> > >    3. 3. **n8n** — Import `n8n/workflow-intake.json`, set credentials (GHL API key, Retell webhook secret)
> > >       4. 4. **GHL** — Create custom fields, pipeline stages, SMS/email templates per `ghl/` docs
> > >          5. 5. **Mem0** — Configure API key in n8n workflow for caller memory lookups
> > >            
> > >             6. ---
> > >            
> > >             7. ## Environment Variables
> > >            
> > >             8. ```env
> > > # Retell AI
> > > RETELL_API_KEY=your_retell_api_key
> > > RETELL_WEBHOOK_SECRET=your_webhook_secret
> > >
> > > # GoHighLevel
> > > GHL_API_KEY=your_ghl_api_key
> > > GHL_LOCATION_ID=your_location_id
> > > GHL_PIPELINE_ID=your_pipeline_id
> > > GHL_HOT_LEAD_STAGE_ID=stage_id
> > > GHL_COLD_LEAD_STAGE_ID=stage_id
> > >
> > > # AnythingLLM
> > > ANYTHINGLLM_API_URL=http://your-anythingllm-instance/api
> > > ANYTHINGLLM_API_KEY=your_key
> > > ANYTHINGLLM_WORKSPACE=law-firm-intake
> > >
> > > # Mem0
> > > MEM0_API_KEY=your_mem0_api_key
> > >
> > > # n8n
> > > N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook/retell-intake
> > > ```
> > >
> > > ---
> > >
> > > ## Pricing
> > >
> > > | Item | Cost |
> > > |------|------|
> > > | **Setup Fee** | $3,500 (one-time) |
> > > | **Monthly Retainer** | $1,200/month |
> > >
> > > ### Setup Includes
> > > - Retell AI agent configuration + voice training
> > > - n8n workflow build + deployment
> > > - GHL pipeline + custom fields + automations
> > > - AnythingLLM knowledge base setup
> > > - Mem0 caller memory integration
> > > - 30-day post-launch support
> > >
> > > ### Monthly Retainer Includes
> > > - Workflow monitoring + maintenance
> > > - Agent prompt optimization
> > > - GHL automation updates
> > > - Monthly performance report
> > > - Up to 5 hours of changes/month
> > >
> > > ---
> > >
> > > ## Repos Referenced
> > >
> > > - [n8n](https://github.com/n8n-io/n8n) — Workflow automation
> > > - [AnythingLLM](https://github.com/Mintplex-Labs/anything-llm) — Local LLM context
> > > - [Mem0](https://github.com/mem0ai/mem0) — Persistent AI memory
> > >
> > > ---
> > >
> > > ## License
> > >
> > > MIT — Built by ausjones84
