# spectrumX — Android AI Assistant starter

This is a starter project, not a signed/compiled APK. It contains:
- Native Kotlin Android client (Jetpack Compose)
- Backend Node.js/Express with OpenAI-compatible chat endpoint, web search via Tavily, image input support, and a basic memory endpoint
- Voice input via Android SpeechRecognizer and spoken replies via TextToSpeech
- Explicit Android app launching via package launch intents
- Local conversation history in app memory (not yet encrypted/persisted across restarts)

## Before you begin
You need:
- Android Studio on a computer to build the APK (or use a trusted cloud Android build service; mobile-only compilation is more difficult)
- An AI provider API key with access to a vision-capable model
- Optional Tavily API key for web search

Never put API keys in the Android app or public GitHub repository. Put them in the backend `.env` file or hosting provider's secret/environment settings.

## Backend setup
1. Install Node.js 20+.
2. In `server/`, copy `.env.example` to `.env`.
3. Set `OPENAI_API_KEY`, and optionally `TAVILY_API_KEY`.
4. Run:
   npm install
   npm start
5. The server listens on port 3000.

For Android emulator, use `http://10.0.2.2:3000`. For a physical phone, use your computer's LAN IP address during local testing, or deploy the backend with HTTPS and use that URL.

## Android setup
1. Open `android/` in Android Studio.
2. Allow Gradle sync and install the Android SDK requested by the project.
3. In `app/src/main/java/com/spectrumx/assistant/MainActivity.kt`, change `BASE_URL` to your deployed HTTPS backend URL. For emulator-only testing, use `http://10.0.2.2:3000/`.
4. Build > Build Bundle(s) / APK(s) > Build APK(s).
5. Install the debug APK on your own test phone. Android may ask you to allow installs from that source.

## Features and limitations
- AI chat: backend API call.
- Voice: Android speech recognition and TTS; recognition availability depends on device/language services.
- Memory: `/api/memory` stores short user-approved memories in server process memory only. It resets when the server restarts. Add a database and user authentication before real deployment.
- Web search: Tavily if `TAVILY_API_KEY` is configured.
- Image understanding: image picker sends selected image as base64 data URL to a vision-capable model.
- Open apps: only apps the user explicitly chooses from the provided action buttons; Android does not allow unrestricted silent app/device control.
- This starter has no login, account isolation, production rate limiting, or encrypted cloud memory. Do not expose publicly without adding these protections.
