# AI-Powered-Business-Operations-Suite

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

**voiceflow agent**
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
 

