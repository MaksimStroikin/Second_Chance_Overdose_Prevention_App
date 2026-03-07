# Second Chance Backend API Documentation

Welcome to the backend! This Spring Boot application handles all the APIs for the Second Chance opioid prevention app.

## 🚀 Live API Base URL
The backend is deployed to the cloud. All React Native requests should be sent to:
**`https://hack-canada-2026.onrender.com`**

*(Note: If the server hasn't been used in 15 minutes, Render puts it to sleep. The very first request to wake it up might take ~50 seconds, but subsequent requests will be instant).*

---

## 🌍 GET Requests (Fetch Data)
These URLs return JSON data for the application.

### 1. Overdose Information Slides
**Endpoint:** `GET /api/info/overdose`
**Returns:** Array of `InfoSlide` objects representing steps to help someone suffering an overdose.

### 2. External Help Slides
**Endpoint:** `GET /api/info/external-help`
**Returns:** Array of `InfoSlide` objects representing therapy groups and helplines.

### 3. Narcan Sites (Live Map Locations)
**Endpoint:** `GET /api/map/narcan-sites?lat=LATITUDE&lng=LONGITUDE`
**Returns:** The 5 closest Narcan availability locations to the user's coordinates.

### 4. Safe Injection Sites (Live Map Locations)
**Endpoint:** `GET /api/map/safe-injection-sites?lat=LATITUDE&lng=LONGITUDE`
**Returns:** The 5 closest safe injection clinics to the user's coordinates.

### 5. Therapy Sites (Live Map Locations)
**Endpoint:** `GET /api/map/therapy-sites?lat=LATITUDE&lng=LONGITUDE`
**Returns:** The 5 closest therapy centers to the user's coordinates.

---

## 📤 POST Requests (Trigger Actions)
These URLs accept data from the frontend and trigger a backend response or action.

### 1. Gemini AI Q&A Chat + ElevenLabs Voiceover
**Endpoint:** `POST /api/qna/send-message`
**Description:** Sends a user question to Google's Gemini 1.5 Flash AI to generate medical advice. The backend then immediately passes that advice to ElevenLabs to generate an MP3 voiceover.
**How to call from React Native:**
```javascript
fetch('https://hack-canada-2026.onrender.com/api/qna/send-message', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ message: "What are the signs of an overdose?" })
})
.then(response => response.json())
.then(data => {
    console.log(data);
    // data.responseMessage -> The text response from Gemini
    // data.voiceover -> The URL path to the generated MP3 file (e.g. "/audio/123abc456.mp3")

    // To play the audio in React Native:
    const audioUrl = `https://hack-canada-2026.onrender.com${data.voiceover}`;
    // Feed `audioUrl` into expo-av or react-native-sound!
});
```

### 2. Trigger SOS Emergency Call
**Endpoint:** `POST /api/sos/emergency-call`
**Description:** Triggers the big red "I need help now" phone call logic, hitting the Twilio API to dispatch a phone call.
**How to call from React Native:**
```javascript
fetch('https://hack-canada-2026.onrender.com/api/sos/emergency-call', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ latitude: 43.6532, longitude: -79.3832 })
})
```

### 3. Build a Route
**Endpoint:** `POST /api/map/build-route`
**Description:** Generates navigation routing logic.
**How to call from React Native:**
```javascript
fetch('https://hack-canada-2026.onrender.com/api/map/build-route', {
  method: 'POST'
})
```
