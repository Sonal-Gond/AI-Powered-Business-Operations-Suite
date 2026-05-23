# AI-Powered-Business-Operations-Suite


# Features of AI-Powered-Business-Operations-Suite
**Omnichannel Lead Capture & Qualification** 
- Captures and qualifies leads across Website Widget, WhatsApp, Telegram, and Phone using a unified Voiceflow AI chatbot and Vapi IVR, with BANT qualification and cross-channel context stored in a single Google Sheet.
  
**Multilingual AI Chatbot with Smart Routing**
- Voiceflow-powered chatbot supports English and Hindi, identifies returning users by email, answers queries from a knowledge base, and routes interested leads through a structured BANT flow with automatic webhook submission.

**Voice AI Operations Suite**
- Vapi-powered voice assistants handle inbound customer support (IVR with 5 departments), outbound appointment reminders, payment collection calls, post-sale satisfaction surveys, and re-engagement campaigns for inactive customers — all with structured post-call reporting.

**Automated Lead Nurturing & Pipeline Management**
- Automatically scores leads as Hot/Warm/Cold, sends personalized email and WhatsApp follow-ups with Calendly booking links, runs outbound call campaigns for hot leads, and tracks every lead through a full pipeline (Qualified → Contacted → Meeting Scheduled → Won/Lost).

**AI Content Generation & Multi-Platform Publishing**
- Generates daily SEO-optimized blog posts via GPT-4o and publishes them to WordPress, while simultaneously creating AI-generated images and platform-specific captions for automated posting to LinkedIn and Facebook — all with CTA links for lead source tracking.

**Post-Meeting Human Review Workflow**
- After every meeting, automatically emails the host a formatted review request with one-click outcome buttons (Won / Lost / Opportunity). Host's response instantly updates the lead's pipeline stage in the master CRM sheet.

**Real-Time Dashboards & Automated Reporting**
- Provides live dashboards for Chatbot Performance, Voice AI Metrics, Lead Pipeline Stage, Content Attribution, and System Health & Uptime. Delivers automated Daily Digest, Weekly, Monthly, Cost Analysis, and ROI reports via Slack and Gmail.

**Proactive Alerting & System Monitoring**
- Monitors workflow health every minute for SLA violations, detects lead volume drops using 7-day rolling averages, tracks budget thresholds across Make.com, Voiceflow, and Vapi, and fires instant Slack alerts for any automation failures — maintaining 99.99% uptime targets.


# Requiremnets
- n8n self hosted or cloud based account
- make.com account
- OpenAI API key 
- Voiceflow account (for chatbot assistant)
- Vapi account (for voice calls)
- Twilio account (for whatsapp chatting)
- Telegram account 
- Google Cloud account (for credentials of google sheet, google calendar, gmail etc.)
- WordPress account with free domain website
- Slack account (for sending Alert and report) 
- Calendly account (For Appoinment link)  


# Setup steps
**n8n workflows setup steps**
- Download n8n workflow from these repository
- Goto n8n dashboard
- Create workflow -> click on three dots (top right corner) -> select import from file -> select   json file (downloaded workflow) 
 
**make.com scenario setup steps**
- Download make.com workflow 
- Goto Make.com dashboard -> create scenario 
- Click on three dots (top right corner) -> Import blueprint -> choose make.com json file -> Import blueprint

**Voiceflow agent**
- Craete account on voiceflow and Download .vf file from these repository
- Click on Project (left sidebar)
- Click import (top right corner) -> Selct downloaded .vf file
- Replace url of API tools with your urls


**VAPI Assistant Setup Steps**
- Download the VAPI tool and assistant JSON files from this repository
- Get your API Key from VAPI Dashboard → API Keys
- Create tool 
  Download all tool JSON files from this repository  
  For each tool JSON file send a POST request:  
  URL → https://api.vapi.ai/tool  
  Header → Authorization: Bearer YOUR_API_KEY  
  Header → Content-Type: application/json  
  Body → contents of the tool JSON file  
  Save the id from each tool response  

- Create Assistant
  Download assistant configurations from this repository    
  Replace YOUR_WEBHOOK_URL in assistant.json with your server URL    
  Replace the toolIds array values with the IDs saved from tool creation    
  Send a POST request:    
  URL → https://api.vapi.ai/assistant    
  Header → Authorization: Bearer YOUR_API_KEY    
  Header → Content-Type: application/json    
  Body → contents of assistant configurations  

 - Now see in vapi dashboard you will see the assistant

# API Keys & Access Token Guide

**Voiceflow API Key**
- Go to your Voiceflow Project → Select your project
- Click Settings from the left sidebar
- Navigate to API Keys → Copy your API key


**VAPI API Key**
- Go to VAPI Dashboard
- Click API Keys from the left sidebar
- Copy your Private Key


**Twilio Account SID & Auth Token**
- Create an account on Twilio
- Go to your Account Dashboard
- Copy your Account SID and Auth Token


**Facebook Never-Expiring Access Token**

- Create a Facebook account → Create a Company Page
- Go to Meta for Developers → Create an App → Open your App
- Navigate to Tools → Graph API Explorer
- Select your app under Meta App → Click Get User Access Token
- Grant the following permissions:
read_insights, pages_show_list, ads_management, ads_read, page_events, pages_read_engagement, pages_manage_metadata, pages_read_user_content, pages_manage_ads, pages_manage_posts, pages_manage_engagement, public_profile
- Copy the generated token → Go to Tools → Access Token Debugger → Paste token → Click Debug
- Scroll down and copy the 3-month access token
- Make a GET request to exchange it for a never-expiring token:  
    GET https://graph.facebook.com/v19.0/me/accounts?access_token=YOUR_3_MONTH_TOKEN

- Copy the token from the response — this is your permanent access token
- Verify by pasting it in Access Token Debugger → The Expires row should show Never


**WordPress Access Token**
- Create a WordPress.com account and get a free domain
- Go to https://developer.wordpress.com/apps/ → Create an app with:

    1. Name → anything (e.g. n8n blog automation)
    2. Website URL → http://localhost
    3. Redirect URL → http://localhost


- Copy your Client ID and Client Secret
- Open this URL in your browser to generate an access token (replace YOUR_CLIENT_ID):

  1. https://public-api.wordpress.com/oauth2/authorize?client_id=YOUR_CLIENT_ID&redirect_uri=http://localhost&response_type=token&scope=global
  2. Log in → Click Authorize → You will be redirected to a URL like:

  3. https://example.com/#access_token=XXXX&expires_in=...&scope=global

  4. Copy only the XXXX part — that is your access token

- Test the token with:

  1. GET https://public-api.wordpress.com/rest/v1.1/me  
  Header: Authorization: Bearer YOUR_TOKEN

- Get your Site ID with:
  1. GET https://public-api.wordpress.com/rest/v1.1/me/sites
  2. Copy the id value from the response — this is your site_id used for blog post generation


**LinkedIn Credentials**
- Create a LinkedIn account → Create a Company Page → Copy the company page URL
- Go to https://developer.linkedin.com/ → Create an app:
- Fill in App Name, LinkedIn Page URL, upload a logo, accept the Legal Agreement → Click Create App
- On the Products tab → Request access for Share on LinkedIn and Sign In with LinkedIn using OpenID Connect
- Go to Auth tab → OAuth 2.0 Settings → Add the redirect URL (obtained from n8n — see below)
- Copy your Client ID and Client Secret
- Get redirect URL from n8n: Go to n8n → Credentials → Search LinkedIn OAuth2 API → Copy the redirect URL → Paste it into the LinkedIn Developer OAuth settings
- Paste the Client ID and Client Secret into the LinkedIn OAuth2 API credential in n8n


**Google Client ID & Client Secret**
(Used for Google Sheets, Google Calendar, and Gmail in workflows)

- Go to Google Cloud Console → Create a new project or select an existing one
- Go to APIs & Services → Library → Search and Enable the following APIs:

   1. Google Sheets API
   2. Google Calendar API
   3. Gmail API


- Go to APIs & Services → OAuth Consent Screen → Select External → Fill in App Name, User Support Email, and Developer Contact Email → Save
- Go to APIs & Services → Credentials → Click + Create Credentials → Select OAuth Client ID
- Choose Application Type (e.g. Web Application) → Add your Redirect URI → Click Create
- Copy your Client ID and Client Secret
- Use the same Client ID and Client Secret for Google Sheets, Google Calendar, and Gmail credentials in your workflows


**Calendly Setup & Meeting Link**

- Create an account at Calendly
- Go to Integrations & Apps from the left sidebar → Search Google Calendar → Click Connect
- Sign in with your Google account → Grant required permissions
- Select the calendar where appointments should appear → Click Add to Calendar
- From the Calendly Dashboard → Click Create → Select New Event Type
- Configure meeting details, availability hours, timezone, and booking limits → Click Save & Close
- Open your event type → Click Share → Copy the booking link  
     https://calendly.com/your-username/your-event
- Use this link in follow-up messages


# Identify which wirkflow is of make.com and n8n
**n8n workflows**
- n8n workflows contains only .json extensions

**make.com scenario**
- Make.com workflows contains .blueprint.json at end of file_name

# System Architecture diagram
<img width="4389" height="5077" alt="EXIM Manager@1 2874999046325684x" src="https://github.com/user-attachments/assets/6c58cef7-e279-4528-b7ee-596407655b86" />


 

