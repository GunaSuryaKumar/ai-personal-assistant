# ai-personal-assistant

AI Personal Assistant
A Flask-based AI Personal Assistant that provides a web interface for interacting with various features, including time/date queries, note-taking, weather updates, and AI chatbot responses via the Eden AI API. The app is designed to run locally with full functionality (including voice input and screenshots) and can be deployed to Render's free tier with some features disabled due to server limitations.
Features

Web Interface: User-friendly UI built with Flask and Tailwind CSS for entering commands and viewing responses.
Time and Date: Retrieves and displays the current time or date.
Note-Taking: Saves and retrieves notes using SQLite (temporary storage on Render).
Weather Updates: Fetches weather information for a specified city using the OpenWeatherMap API.
AI Chatbot: Integrates with Eden AI's chatbot API for general queries and assistance.
Voice Input (Local Only): Uses speech recognition for hands-free command input (disabled on Render).
Screenshots (Local Only): Captures screenshots of the current screen (disabled on Render).
Text-to-Speech (Local Only): Speaks responses aloud (disabled on Render).

Prerequisites

Python 3.10.7 or higher
Git
A GitHub account for Render deployment
API Keys:
Eden AI API Key for chatbot functionality
OpenWeatherMap API Key for weather updates



Project Structure
ai-personal-assistant/
├── app.py              # Main Flask application
├── templates/
│   └── index.html      # Web interface template
├── requirements.txt    # Python dependencies
├── render.yaml         # Render deployment configuration
└── README.md           # This file

Local Setup

Clone the Repository
git clone https://github.com/yourusername/ai-personal-assistant.git
cd ai-personal-assistant


Create a Virtual Environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate


Install Dependencies
pip install -r requirements.txt


Set Environment Variables (Optional for Local)

Create a .env file or export variables:export EDEN_AI_API_KEY="your-eden-ai-key"
export OPENWEATHERMAP_API_KEY="your-openweathermap-key"


If not set, the app uses a default Eden AI key (replace with your own for production).


Run the App
python app.py


Open http://localhost:5000 in a browser to access the web interface.



Deployment to Render
Render's free tier is used to host the app, with some features (voice input, screenshots, text-to-speech) disabled due to server limitations.
Steps

Push to GitHub

Create a GitHub repository (e.g., ai-personal-assistant).
Push your local project:git remote add origin https://github.com/yourusername/ai-personal-assistant.git
git branch -M main
git push -u origin main




Sign Up for Render

Visit render.com and sign up using GitHub.
No credit card is required for the free tier.


Create a Web Service

In the Render Dashboard, click "New" > "Web Service".
Connect your GitHub account and select the ai-personal-assistant repository.
Configure:
Name: ai-personal-assistant
Environment: Python
Branch: main
Build Command: pip install -r requirements.txt
Start Command: gunicorn app:app
Plan: Free


If using render.yaml, Render auto-configures these settings.


Set Environment Variables

In the Render Dashboard, go to your service > "Environment" tab.
Add:
PYTHON_VERSION: 3.10.7
EDEN_AI_API_KEY: Your Eden AI API key
OPENWEATHERMAP_API_KEY: Your OpenWeatherMap API key
RENDER: true (disables audio/screenshot features)


Example:PYTHON_VERSION=3.10.7
EDEN_AI_API_KEY=your-eden-ai-key
OPENWEATHERMAP_API_KEY=your-openweathermap-key
RENDER=true




Deploy

Click "Create Web Service" or let Render deploy from render.yaml.
The build takes a few minutes (free tier is slower).
Access your app at https://ai-personal-assistant.onrender.com (or your custom URL).


Update the App

Make changes locally, commit, and push:git add .
git commit -m "Update app"
git push origin main


Render auto-deploys on each push.



Usage

Web Interface:

Enter commands in the text box (e.g., "time", "date", "take a note buy milk", "weather in London").
Click "Send Command" to process.
Use "View Notes" to see saved notes.
Voice input is disabled on Render but works locally if hardware is available.


Available Commands:

time: Shows current time.
date: Shows current date.
screenshot: Takes a screenshot (local only).
note <content>: Saves a note (e.g., "note buy milk").
weather in <city>: Fetches weather (e.g., "weather in London").
get_notes: Displays all notes (via "View Notes" button).
exit: Exits the app (stops processing).
Any other query: Sent to Eden AI's chatbot.


Notes:

On Render, notes are stored in /tmp/notes.db and may be lost on redeployment due to free tier limitations.
Weather requires a valid OpenWeatherMap API key.
Voice, screenshot, and text-to-speech features require local hardware (microphone, display, audio).



Limitations

Render Free Tier:
Apps sleep after 15 minutes of inactivity, causing a wake-up delay (up to 50 seconds).
No persistent storage; SQLite data in /tmp may be lost on redeployment.
Limited to 750 hours/month (sufficient for one app running 24/7).


Disabled Features on Render:
Voice input (pyaudio): No microphone access.
Text-to-speech (pyttsx3): No audio hardware.
Screenshots (pyscreeze): No display.
These features work locally with appropriate hardware.


Eden AI: Ensure your API key has sufficient quota.
Weather: Requires an OpenWeatherMap API key.

Troubleshooting

App Fails to Load:
Check Render's "Logs" tab for errors (e.g., missing dependencies, invalid API keys).
Verify gunicorn is in requirements.txt and the start command is gunicorn app:app.
Ensure environment variables are set correctly.


Eden AI Errors:
Confirm your API key is valid and has quota.
Check network connectivity in logs.


Weather Errors:
Ensure OPENWEATHERMAP_API_KEY is set.
Test with a valid city name (e.g., "weather in London").


Notes Not Persisting:
On Render, SQLite uses /tmp, which is temporary. Consider a paid plan or external database (e.g., MongoDB Atlas) for persistence.


Slow Load Times:
Free tier apps sleep after inactivity. Expect delays on first load.



Contributing
Contributions are welcome! To contribute:

Fork the repository.
Create a feature branch (git checkout -b feature-name).
Commit changes (git commit -m "Add feature").
Push to the branch (git push origin feature-name).
Open a pull request.

License
This project is licensed under the MIT License.
Acknowledgments

Flask for the web framework.
Eden AI for chatbot integration.
OpenWeatherMap for weather data.
Render for free hosting.
Tailwind CSS for styling.

