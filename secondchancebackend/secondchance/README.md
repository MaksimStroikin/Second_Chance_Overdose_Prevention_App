# Second Chance Backend

This is the Spring Boot backend for the Second Chance hackathon project. It provides REST APIs for answering medical questions via Gemini 1.5, generating automated text-to-speech audio via ElevenLabs, and placing emergency SOS phone calls using Twilio.

## Prerequisites
1. Java 17 installed locally.
2. An active Internet connection.
3. Access to the `application-secret.properties` file with active API Keys.

## How to Run the Server Locally

Since our Twilio webhook requires a public URL to reach this computer for audio files, you MUST run this project using two separate terminals inside VS Code.

### Step 1: Open the Public Tunnel
1. Open a terminal in VS Code.
2. Run the following command to expose port 8080 to the internet:
   ```bash
   ssh -R 80:localhost:8080 nokey@localhost.run
   ```
3. Look at the output. It will give you a public URL (e.g., `https://2b1811ce78a559.lhr.life`).
4. Keep this terminal open and running! Do not type anything else into it.

### Step 2: Update Application Properties
1. Open `src/main/resources/application-secret.properties` (or create it if you cloned fresh and it was ignored by git).
2. Look for the `app.base.url=` line.
3. Paste the brand new `localhost.run` URL you just copied from the previous step. Save the file.

### Step 3: Start Spring Boot
1. In VS Code, click the `+` button in the terminal panel to open a **second, separate terminal tab**.
2. Make sure you are in the `secondchance` root folder.
3. Run the Spring Boot server:
   ```bash
   ./gradlew bootRun
   ```
4. Wait for the console to say `Tomcat started on port 8080`.

## How to Test the Project

I have built two custom HTML web pages specifically to help you test the APIs instantly without needing the React Native frontend:

1. **Test Q&A Bot**: Open `test.html` in your web browser. You can type crisis questions and the backend will generate Gemini text and an ElevenLabs MP3 voiceover.
2. **Test Emergency Dialer**: Open `test_sos.html` in your web browser. Click the red button to simulate the mobile app sending your GPS coordinates to trigger a live phone call to your teammate!
