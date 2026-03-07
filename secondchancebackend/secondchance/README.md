# Second Chance Backend

This is the Spring Boot backend for the Second Chance hackathon project. It provides REST APIs for answering medical questions via Gemini 1.5, generating automated text-to-speech audio via ElevenLabs, and placing emergency SOS phone calls using Twilio.

## Prerequisites
1. Java 17 installed locally.
2. An active Internet connection.
3. Access to the `application-secret.properties` file with active API Keys.

## Server Deployment (Render)

The backend is officially deployed and running live on the cloud! 

🚀 **Live API URL:** `https://hack-canada-2026.onrender.com`

**Frontend Developers (React Native):**
You do NOT need to run this Spring Boot server locally or set up any `localhost.run` tunnels. Simply point your `fetch()` requests directly to the live URL above. (See `API_REFERENCE.md` for specific endpoints).

**Backend Developers (Java):**
If you need to make changes to the backend:
1. Make your code changes in `secondchance`.
2. Commit and push to the `main` branch.
3. Render is connected to this repository and will **automatically compile and deploy your changes** within 3–5 minutes of pushing.

## How to Test the Project

I have built two custom HTML web pages specifically to help you test the APIs instantly without needing the React Native frontend:

1. **Test Q&A Bot**: Open `test.html` in your web browser. You can type crisis questions and the backend will generate Gemini text and an ElevenLabs MP3 voiceover.
2. **Test Emergency Dialer**: Open `test_sos.html` in your web browser. Click the red button to simulate the mobile app sending your GPS coordinates to trigger a live phone call to your teammate!
