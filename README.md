AI Lead Qualifier & Outreach Micro-App
This project is a complete, full-stack application designed to automatically capture, score, and manage new business leads. It uses a modern stack including a web-based frontend, a powerful automation backend, AI for intelligent analysis, and a robust database.

The system features a public-facing lead capture form and a private admin dashboard to review, filter, and initiate outreach for the leads that have been scored by the AI.

Core Technologies
Frontend: Lovable (Public Website + Admin Dashboard)

Automation Backend: n8n (Workflow Automation)

AI Model: Google Gemini (Lead Scoring, Classification & Email Drafting)

Database: Supabase (Postgres Database)

Live Demo & Repositories
Live App URL: [INSERT YOUR LIVE LOVABLE APP URL HERE]

Demo Video (Loom): [INSERT YOUR LOOM VIDEO URL HERE]

Frontend Repo (Lovable): [INSERT GITHUB REPO LINK FOR YOUR LOVABLE PROJECT]

Project Files Repo (n8n, SQL): [INSERT GITHUB REPO LINK FOR YOUR PROJECT FILES]

Architecture Overview
The application follows a modern, decoupled architecture where the frontend, backend automation, and database operate as independent services.

[Lovable Frontend] ---> [n8n Webhook] ---> [Google Gemini AI] ---> [Supabase DB]
      |                                                                 ^
      |                                                                 |
      +-----> [Admin Dashboard] ----------------------------------------+

Flow 1: Lead Capture
A user submits the lead capture form on the public Lovable website.

The form data is sent to the "Lead Capture" n8n webhook.

The n8n workflow sends the lead's problem description to the Google Gemini API for scoring and classification.

The complete, enriched lead data is saved to the Supabase Postgres database.

Flow 2: Outreach
An admin reviews a lead in the Lovable admin dashboard and clicks "Send Outreach".

The dashboard sends the lead_id to the "Send Outreach" n8n webhook.

The n8n workflow fetches the lead's data from Supabase.

The Google Gemini API drafts a personalized email.

The lead's status is updated to outreach_sent in the Supabase database.

Setup Instructions
Follow these steps to set up and run the project locally or in a similar cloud environment.

1. Prerequisites
A Supabase account (free tier is sufficient).

An n8n account (cloud or self-hosted).

A Google AI Studio account to get a Gemini API key.

A Lovable project.

2. Set Up the Database (Supabase)
Create a new project in Supabase.

Navigate to the SQL Editor.

Open the schema.sql file from this repository, copy its contents, and run it in the Supabase SQL Editor. This will create all the necessary tables (leads, lead_events, etc.) and add some sample data.

3. Set Up the Automation (n8n)
Log in to your n8n instance.

Create two new blank workflows.

For the first workflow, go to File > Import > From File and import the lead-capture-workflow.json file from this repository.

For the second workflow, import the send-outreach-workflow.json file.

For both workflows, you will need to reconnect the credentials for the Supabase and Google Gemini nodes using your own API keys.

4. Configure Environment Variables
Create a .env file by copying the .env.example file.

Fill in the required values:

Your Supabase Database Connection URL.

Your Google Gemini API Key.

The Production URLs for both of your new n8n webhooks.

5. Connect the Frontend (Lovable)
Open your Lovable project.

Connect it to your Supabase project using Lovable's native integration.

Ensure the public form is configured to send its data to your "Lead Capture" webhook URL.

Ensure the "Send Outreach" button in your admin dashboard is configured to send a POST request with the lead_id to your "Send Outreach" webhook URL.

How to Test
To test the end-to-end flow of the application:

Navigate to your live Lovable website's public form.

Fill in the form fields. For the "Problem" description, use a realistic example to see the AI in action.

Sample Test Lead (High-Fit)
Our sales reps are spending over 10 hours a week manually copying and pasting lead data from our marketing forms into the company CRM. This is causing significant delays in follow-up and leads to frequent data errors. We are looking for an automated solution to instantly capture and score new leads to free up our sales team to focus on closing deals.

Submit the form.

Navigate to your /admin dashboard. You should see the new lead appear in the table with a high "Fit Score" and a "Sales ops" label.

Click on the lead to open the detail view.

Click the "Send Outreach" button. You should see a success notification.

Check your Supabase leads table. The status for that lead should now be updated to outreach_sent.

Known Limitations
Email Sending: The "Send Outreach" workflow currently only drafts the email and updates the lead's status. It does not connect to an SMTP service to actually send the email. This could be added as a future enhancement by adding a "Send Email" node in n8n.
