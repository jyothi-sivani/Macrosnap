🥗 MacroSnap

MacroSnap is an AI-powered nutrition chat app built with Streamlit. A user enters their name and WhatsApp number once, then chats with an AI nutrition buddy by typing a food question or attaching a photo of a meal. The app replies with an instant estimate of calories, protein, carbs and fat. One button sends a short summary of the conversation straight to the user's WhatsApp.

Calorie and macro values are estimates, not medical or dietary advice.

Features
Chat with an AI nutrition buddy using text or meal photos
Instant calorie and macro estimates in a clean table
Name and WhatsApp number entered once per session
One-click WhatsApp summary of the whole conversation
Clear chat and switch user options in the sidebar
Tech stack
Python 3.9+
Streamlit for the chat interface
Google Gemini API (google-genai) for chat and vision
Twilio WhatsApp API (sandbox) for sending summaries

No OpenCV, no MediaPipe and no model training are needed.

Project structure
macrosnap/
├── app.py                          # the app itself
├── prompts.py                      # the AI's personality and instructions
├── requirements.txt                # dependencies
├── .gitignore                      # keeps secrets.toml out of Git
└── .streamlit/
    └── secrets.toml.example        # template for your API keys
Setup
1. Get your keys
Gemini API key: create one for free in Google AI Studio (Get API key > Create API key).
Twilio credentials: create a free Twilio account. Your Account SID and Auth Token are on the Console home page.
2. Install
bash
python -m venv venv

# Windows
venv\Scripts\activate
# Mac / Linux
source venv/bin/activate

pip install -r requirements.txt
3. Add your keys

Copy .streamlit/secrets.toml.example to .streamlit/secrets.toml and fill in your values:

toml
GEMINI_API_KEY = "your-gemini-api-key"
GEMINI_MODEL = "gemini-2.5-flash"

TWILIO_ACCOUNT_SID = "ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
TWILIO_AUTH_TOKEN = "your-twilio-auth-token"
TWILIO_WHATSAPP_FROM = "whatsapp:+14155238886"

Every line must be either a comment starting with # or a KEY = "value" pair. Never commit secrets.toml or share your keys.

4. Join the Twilio WhatsApp sandbox
In the Twilio Console, open Messaging > Try it out > Send a WhatsApp message.
From the WhatsApp number you will use in the app, send join <your-two-word-code> to the sandbox number (usually +1 415 523 8886). Scanning the QR code on that page fills in the message for you.
Wait for Twilio's confirmation reply.

Sandbox membership lasts 72 hours. Send the join message again when it expires.

5. Run
bash
streamlit run app.py

The app opens at http://localhost:8501.

How to use
1.Enter your name and WhatsApp number (a 10-digit Indian number is treated as +91).
2.Type a question such as "calories in 2 idlis and sambar", or attach a meal photo.
3.Read the estimate, and keep chatting if you like.
4.Click Send summary to WhatsApp in the sidebar.
Troubleshooting
Problem	Fix
"Missing GEMINI_API_KEY"	The file must be named .streamlit/secrets.toml and be valid TOML. Check for a missing # on comment lines or a missing quote. Run streamlit run app.py from the macrosnap folder.
Gemini authentication error	Create a fresh key in Google AI Studio and replace the old one.
Model not found (404)	Change GEMINI_MODEL in secrets.toml to a current Gemini Flash model.
"Your number is not connected to a Sandbox"	Send join <your-code> from your WhatsApp number to the sandbox number, with nothing else added.
Twilio error when sending	Rejoin the sandbox, then check the Account SID and Auth Token.
accept_file error	Run pip install -U streamlit (version 1.43 or newer is needed).
Security notes
Keep secrets.toml out of Git (it is listed in .gitignore).
If a key is ever exposed, delete it in its console and create a new one.
Credits

Built in a workshop using Gemini and Twilio.
