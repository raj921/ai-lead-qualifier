# AI Lead Qualifier & Outreach Micro-App

A **full-stack application** that automatically captures, scores, and manages new business leads.  
It combines a modern **frontend**, **workflow automation backend**, **AI-powered lead analysis**, and a **robust database** to streamline lead qualification and outreach.

---

## 🚀 Features
- **Public Lead Capture Form** – Collect lead details from potential clients.  
- **AI Lead Scoring & Classification** – Uses **Google Gemini** to enrich and prioritize leads.  
- **Admin Dashboard** – Review, filter, and initiate outreach for qualified leads.  
- **Automated Outreach** – Drafts personalized emails.  
- **Database Integration** – Stores leads and events in **Supabase Postgres**.  

---

## 🛠️ Tech Stack
- **Frontend**: [Lovable](https://lovable.dev) (Public Website + Admin Dashboard)  
- **Automation Backend**: [n8n](https://n8n.io) (Workflow Automation)  
- **AI Model**: [Google Gemini](https://ai.google.dev/) (Scoring, Classification & Drafting)  
- **Database**: [Supabase](https://supabase.com) (Postgres Database)  

---

## 📺 Demo & Repositories
- **Live App**: [INSERT YOUR LIVE LOVABLE APP URL HERE]  
- **Demo Video (Loom)**: [INSERT YOUR LOOM VIDEO URL HERE]  
- **Frontend Repo (Lovable)**: [INSERT GITHUB REPO LINK FOR YOUR LOVABLE PROJECT]  
- **Automation & SQL Repo**: [INSERT GITHUB REPO LINK FOR YOUR PROJECT FILES]  

---

## 🏗️ Architecture

[Lovable Frontend] ---> [n8n Webhook] ---> [Google Gemini AI] ---> [Supabase DB]
| ^
| |
+-----> [Admin Dashboard] ----------------------------------------+

markdown
Copy code

- **Frontend (Lovable)** handles both public-facing form and private admin dashboard.  
- **n8n** orchestrates workflows and connects to AI + DB.  
- **Gemini AI** provides intelligent scoring, classification, and email drafting.  
- **Supabase** stores all leads, statuses, and events.  

---

## 🔄 Flows

### 1. Lead Capture
1. User submits the **lead form** on the website.  
2. Form data is sent to **Lead Capture Webhook** (n8n).  
3. n8n sends problem description → **Google Gemini API**.  
4. Enriched data (score, classification) → stored in **Supabase**.  

### 2. Outreach
1. Admin opens the **dashboard**, reviews lead, clicks **Send Outreach**.  
2. Dashboard sends `lead_id` → **Send Outreach Webhook**.  
3. n8n fetches lead from **Supabase**.  
4. **Gemini AI** drafts personalized email.  
5. Supabase updates lead status → `outreach_sent`.  

---

## ⚙️ Setup Instructions

### 1. Prerequisites
- [Supabase](https://supabase.com) account (Free Tier OK)  
- [n8n](https://n8n.io) account (Cloud or Self-hosted)  
- [Google AI Studio](https://ai.google.dev/) API Key (Gemini)  
- [Lovable Project](https://lovable.dev)  

---

### 2. Database Setup (Supabase)
1. Create a **new project** in Supabase.  
2. Go to **SQL Editor**.  
3. Copy & run contents of `schema.sql` from this repo.  
   - Creates tables: `leads`, `lead_events`, etc.  
   - Adds sample data.  

---

### 3. Automation Setup (n8n)
1. Login to n8n.  
2. Create **two workflows**:  
   - Lead Capture → Import `lead-capture-workflow.json`  
   - Send Outreach → Import `send-outreach-workflow.json`  
3. Reconnect credentials for **Supabase** and **Google Gemini** nodes.  

---

### 4. Environment Variables
Create `.env` file (copy `.env.example`) and set values:

```env
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key
GEMINI_API_KEY=your_gemini_api_key

N8N_LEAD_CAPTURE_URL=https://your-n8n-webhook-url/lead-capture
N8N_SEND_OUTREACH_URL=https://your-n8n-webhook-url/send-outreach
5. Frontend Setup (Lovable)
Open your Lovable project.

Connect it with Supabase via Lovable native integration.

Configure:

Public form → sends data → Lead Capture Webhook.

Admin “Send Outreach” button → POST request with lead_id → Send Outreach Webhook.

✅ Testing
Go to your live public form.

Enter a test lead. Example:

vbnet
Copy code
Our sales reps spend 10+ hours/week manually copying lead data into CRM. 
We want automation to capture & score leads instantly.
Open /admin dashboard → see new lead with Fit Score and Classification.

Click Send Outreach → Success notification.

Verify Supabase: lead status = outreach_sent.

⚠️ Known Limitations
Email sending is not fully integrated.

Currently, only drafts email + updates status.

Can add SMTP / SendGrid / SES node in n8n for real sending.

📌 Roadmap
 Add real email sending (SMTP or Email API).

 Build analytics dashboard (conversion, trends).

 Extend AI for "Next Best Action" recommendations.

👨‍💻 Author
Built with ❤️ using Lovable, n8n, Supabase, and Google Gemini.

yaml
Copy code

---

👉 Do you also want me to **generate and package the `schema.sql`, `lead-capture-workflow.json`, and `send-outreach-workflow.json`** so you’ll have a complete repo (README + DB + workflows) ready to upload to GitHub?







