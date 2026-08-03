# TTS Web App

A lightweight, single-file text-to-speech web application styled like a vintage newspaper front page.  
It lets users paste text, choose a voice, adjust speaking speed, and listen with live word highlighting.

## Overview

This project is implemented in one standalone HTML file:

- `TTS-web-app.html`

It includes:

- Semantic HTML structure for the reading interface
- Embedded CSS for light/dark newspaper-style themes
- Embedded JavaScript using the browser `SpeechSynthesis` API

No build tools, package manager, or backend services are required.

## Features

- **Text-to-speech playback** using browser-native speech synthesis
- **Voice selection** from available system/browser voices
- **Adjustable playback speed** (0.5x to 2.0x)
- **Pause / Resume / Stop controls**
- **Live word highlighting** while speech is playing
- **Auto-scroll tracking** to keep the current spoken word in view
- **Word counter with limit indicator** (shows count out of 1000 words)
- **Light/Dark theme toggle** with preference saved in `localStorage`
- **Responsive mobile-first layout** with safe-area and viewport handling

## How It Works

1. User enters or pastes text in the manuscript editor.
2. App counts words and displays `N / 1000 words`.
3. On Play, the editor is replaced by a reader view.
4. The text is tokenized into word spans for visual tracking.
5. `SpeechSynthesisUtterance` events update the highlighted word in real time.
6. Voice/rate changes while speaking restart playback from the current word.

## Requirements

- A modern browser with Web Speech API support (`window.speechSynthesis`)
- Audio output enabled on the device

## Run Locally

Because this is a static single-file app, you can run it directly:

1. Clone or download the repository.
2. Open `TTS-web-app.html` in your browser.

Optional (recommended for consistent behavior): serve the folder with any static file server and open the served URL.

## Usage

1. Open the app.
2. Paste or type your text in **The Manuscript** section.
3. Select a **Narrator** voice.
4. Adjust **Tempo** as needed.
5. Click **Play** to start reading.
6. Use **Pause** to pause/resume and **Stop** to end playback.
7. Toggle theme from the moon/sun button in the masthead.

The app uses local system fallback fonts, so it also works offline without external font requests. Draft text, narrator, tempo, and theme are stored in this browser's local storage; avoid saving sensitive manuscripts.

## Project Structure

```text
TTS-web-app/
├── TTS-web-app.html   # Full app (HTML + CSS + JS)
├── README.md          # Project documentation
└── LICENSE            # MIT license
```

## Browser Notes

- Available voices vary by OS, browser, and installed language packs.
- Some browsers load voices asynchronously; this app repopulates voice options whenever the browser reports new voices (with a short fallback timer).
- Chrome (and some other engines) silently stops speaking roughly 15 seconds into a single utterance. To work around this, the app splits the text into small word-safe chunks and chains them automatically, so long manuscripts play through without interruption.
- Playback is paused/resumed by a small internal state machine rather than by polling the browser's `speaking`/`paused` flags, which keeps the Play / Pause / Resume / Stop buttons in sync.
- Your draft text, narrator voice, tempo, and theme are remembered across reloads via browser `localStorage`. Draft text is stored locally in plaintext for this origin; avoid saving sensitive manuscripts.
- If speech controls seem unavailable, the browser may not support `speechSynthesis` or audio may be blocked; the app displays an explanatory status message when the API is unavailable.

## Manual Regression Checks

- Type and paste text, including tabs and multiple spaces; confirm the counter updates immediately and over-limit text is rejected.
- Use text long enough for multiple chunks; pause/resume, change tempo or narrator, and confirm no words are skipped or repeated.
- Test a browser/voice that does not emit boundary events; confirm fallback highlighting advances through the active chunk.
- Hide the page or lock the device during playback; confirm controls show the paused state and Resume continues from the current word.
- Test with SpeechSynthesis unavailable and with blocked `localStorage`; confirm the page remains usable and displays a clear speech-support message.

## Customization Ideas

- Add pitch and volume controls
- Add import/export text support
- Add keyboard shortcuts for playback controls

## License

This project is licensed under the MIT License.  
See `LICENSE` for details.
