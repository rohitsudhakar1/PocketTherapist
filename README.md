# Pocket Therapist

An Android app that combines journaling with AI-driven mental wellness support. Users record how they feel; the app classifies the emotion and sentiment from the entry and returns personalized song picks, nearby help, and short evidence-based wellness exercises.

Built as the team project for **ECE 454 (Mobile Computing Systems)** at the University of Wisconsin–Madison, Fall 2025.

## Team

- Yana Gupta
- Rishab Gupta
- Simar Tathgir
- Rohit Sudhakar

## Features

- **Journaling.** Plain-text entries with swipe-to-delete, edit dialogs, and a per-day activity view.
- **Emotion classification.** Per-entry detection across six classes (sadness, joy, love, anger, fear, surprise). On-device rule-based fallback, with a RoBERTa-based model staged for TensorFlow Lite inference.
- **Sentiment scoring.** Negative / neutral / positive scoring fed into the recommendation prompt.
- **AI recommendations (Google Gemini).** Three flows: song picks, nearby help (therapist types, support groups, crisis lines), and short wellness suggestions (2–10 min interventions).
- **Crisis detection.** Pattern matcher that surfaces an alert dialog and crisis-line resources when language signals risk.
- **AI consent + onboarding.** Explicit consent flow before any text leaves the device, plus a first-run onboarding experience.
- **Activity tracking.** Background service + boot receiver maintain a daily activity store for context-aware recommendations.

## Tech

- **Language:** Kotlin
- **AI:** Google Gemini Pro (recommendations), RoBERTa (emotion/sentiment, on-device path)
- **Backend services:** Firebase (Realtime Database + storage)
- **Build:** Gradle (Kotlin DSL), Android Studio

## Setup

1. Clone the repo and open it in Android Studio.
2. Create a `.env` file at the project root with:
   ```
   GEMINI_API_KEY=your_gemini_api_key_here
   ```
3. Provide your own `app/google-services.json` from a Firebase project of your own (the one committed in history points to the team project and may be revoked).
4. Sync Gradle, then run on an emulator or physical device.

## Repository layout

```
app/
  src/main/java/com/example/pockettherapist/
    api/                  Gemini + network wrappers
    adapters/             RecyclerView adapters
    *.kt                  Fragments, services, stores, model wrappers
  src/main/res/           Layouts, drawables, themes
  src/main/assets/models/ Local ML model weights
```

Key files:
- `RecommendationEngine.kt` — three Gemini flows (songs / nearby help / wellness).
- `EmotionModelPredictor.kt`, `SentimentModelPredictor.kt` — model wrappers + keyword fallbacks.
- `CrisisDetector.kt` — risk-language detection.
- `ActivityTrackingService.kt`, `BootReceiver.kt` — background daily activity capture.
- `AIConsentManager.kt`, `FirstTimeStore.kt` — consent + onboarding state.

See `RECOMMENDATION_ENGINE_README.md` for the recommendation pipeline in detail.

## Note

This is a private portfolio mirror. The team development repository lives at `yanagupta1/PocketTherapist`.
