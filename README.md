# TTS Web App

A lightweight, single-file text-to-speech web application styled like a vintage newspaper front page.  
It lets users paste text, choose a voice, adjust speaking speed, and listen with live word highlighting.

## Overview

This project is implemented in one standalone HTML file:

- `/home/runner/work/TTS-web-app/TTS-web-app/TTS-web-app.html`

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
2. Open `/home/runner/work/TTS-web-app/TTS-web-app/TTS-web-app.html` in your browser.

Optional (recommended for consistent behavior): serve the folder with any static file server and open the served URL.

## Usage

1. Open the app.
2. Paste or type your text in **The Manuscript** section.
3. Select a **Narrator** voice.
4. Adjust **Tempo** as needed.
5. Click **Play** to start reading.
6. Use **Pause** to pause/resume and **Stop** to end playback.
7. Toggle theme from the moon/sun button in the masthead.

## Project Structure

```text
TTS-web-app/
├── TTS-web-app.html   # Full app (HTML + CSS + JS)
├── README.md          # Project documentation
└── LICENSE            # MIT license
```

## Browser Notes

- Available voices vary by OS, browser, and installed language packs.
- Some browsers load voices asynchronously; this app repopulates voice options multiple times to handle that behavior.
- If speech controls seem unavailable, ensure the browser supports `speechSynthesis` and that audio is not blocked.

## Customization Ideas

- Add persistent text drafts via `localStorage`
- Add pitch and volume controls
- Add import/export text support
- Add keyboard shortcuts for playback controls

## License

This project is licensed under the MIT License.  
See `/home/runner/work/TTS-web-app/TTS-web-app/LICENSE` for details.
