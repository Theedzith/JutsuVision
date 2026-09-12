<h1 align="center">🌀 Shinobi Vision — Jutsu AR</h1>

<p align="center">
  <strong>Cast real ninjutsu with your bare hands — right in the browser.</strong><br />
  Open your <strong>left palm</strong> to charge a <strong>Rasengan</strong> &nbsp;·&nbsp; Open your <strong>right palm</strong> to unleash a <strong>Chidori</strong>.
</p>

<p align="center">
  <img alt="Tracking" src="https://img.shields.io/badge/tracking-MediaPipe%20Hands-25c7ff?style=flat-square" />
  <img alt="Audio" src="https://img.shields.io/badge/audio-Web%20Audio%20API-9a78ff?style=flat-square" />
  <img alt="Code" src="https://img.shields.io/badge/code-Vanilla%20JS-55e6ad?style=flat-square" />
  <img alt="Build" src="https://img.shields.io/badge/build-none-f4f7ff?style=flat-square" />
  <img alt="Backend" src="https://img.shields.io/badge/backend-none-ff657c?style=flat-square" />
</p>

A real-time AR experience that turns your **webcam into a ninja training ground.** MediaPipe tracks your hands, a live *chakra* meter builds while you hold an open palm, and at 100% a cinematic **Rasengan** or **Chidori** fires — composited onto your camera feed with black-background keying and synchronized sound.

> 💡 One HTML file. No frameworks, no backend, no database, no installs. Just open it, allow the camera, and *believe it*.

---

## ✨ Features

- 🖐️ **Two-hand tracking** — MediaPipe Hands follows up to two hands and routes them by *physical* side, so your real left hand always charges Rasengan and your real right hand always charges Chidori
- 🔷 **Progressive chakra charging** — hold an open palm and watch the meter fill; release it and watch your power drain away
- 🔁 **Channel discipline** — chakra is one shared meter; switching hands mid-charge resets it (a true shinobi commits to one jutsu)
- 🎬 **Cinematic jutsu overlays** — full-screen MP4 effects anchored to your hand and scaled to the screen
- 🎞️ **Real-time video keying** — per-pixel black-background removal makes the effects look transparent over the live camera, no green screen required
- 🔊 **Immersive audio** — a synthesized Web Audio charge hum that swells while you focus, plus the signature MP3 sound effects on release
- 🎛️ **Futuristic HUD** — FPS / latency / hand-count telemetry, per-hand power gauges, a glowing chakra core, live event log, and a RESET control
- 🧩 **Zero local dependencies** — everything loads from CDNs; perfect for demos, labs, and classroom projects

---

## 🚀 Getting Started

**Webcam access requires localhost or HTTPS** — opening `index.html` straight from disk (`file://`) will be blocked by the browser.

**Option A — VS Code Live Server** *(recommended)*
1. Install the **Live Server** extension
2. Right-click `index.html` → **Open with Live Server**
3. Press **START** and allow camera access

**Option B — Python**
```bash
python3 -m http.server 8080
# then open http://localhost:8080 and press START
```

**Option C — Node**
```bash
npx serve .
```

All options need an internet connection for the MediaPipe / font CDNs, plus a webcam (or a virtual-camera tool for testing without hardware).

---

## 🎮 How to Use

1. Press **START** (this also unlocks audio, which satisfies browser autoplay rules)
2. Hold up an **open palm** with fingers splayed — the gauge starts climbing
3. At **100% chakra** the jutsu **releases** 🌀⚡
4. Swap hands and re-charge to try the other jutsu
5. Hit **RESET** anytime to clear the field and cooldown

---

## 🧠 How It Works

### Gesture detection
An *open palm* is detected when **at least 3 of 4 fingers** are splayed — each finger joint must extend past ~129° and stretch beyond its base knuckle — and the thumb-to-pinky span is **1.4× wider than the palm**.

### The charge loop
- Holding an open palm fills the meter to **100% in ~3 seconds**
- Releasing the palm makes chakra **decay**
- Switching hands mid-charge **resets** the meter
- Each hand also tracks its own "hold power" that fades when the hand drops

### The release
| Jutsu | Hand | Visual | Duration |
|---|---|---|---|
| 🌀 Rasengan | Left | 1.62× screen width | 6.2 s |
| ⚡ Chidori | Right | 1.34× screen width | 3.1 s |

Each jutsu is **anchored to your hand position**, scaled to the screen, and followed by a short cooldown window before you can release again.

### The compositing trick
The effects are MP4s shot on a black background. A per-pixel keyer reads each video frame and drops dark pixels (max RGB < 46 fully transparent, < 100 partially), leaving only the glowing jutsu composited over the live camera feed.

---

## ⚙️ Tech Stack

| Layer | Tech |
|---|---|
| Hand tracking | [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker) (CDN) |
| Rendering | HTML5 Canvas 2D — hand landmarks, keying, compositing |
| Audio | Web Audio API — synthesized charge tone + decoded MP3 jutsu SFX |
| Code | Vanilla JavaScript · HTML5 · CSS3 (single file) |
| Typeface | Inter + Orbitron (Google Fonts) |

## 📁 Project Structure

```text
.
├── index.html           # The entire app — markup, styles, and logic
├── assets/
│   ├── rasengan_sound.mp3   # Rasengan SFX
│   ├── chidori_sound.mp3    # Chidori SFX
│   ├── naruto.mp4           # Rasengan cinematic overlay
│   └── sasuke.mp4           # Chidori cinematic overlay
└── README.md
```

> 🎬 *A screen recording of the charge-and-release flow would make this README shine — drop it in as `assets/demo.gif` and add a **Demo** section above.*

## 🧪 Compatibility

Modern Chromium browsers (Chrome, Edge, Brave) recommended, followed by Safari / Firefox. Requires a webcam and WebRTC `getUserMedia`. Lower-end machines may see reduced frame rates during tracking.

## 🛠️ Troubleshooting

| Problem | Fix |
|---|---|
| “Camera permission blocked” | Allow camera access in the site permissions and press **START** again |
| Camera won't start | Serve over localhost or HTTPS — `file://` never works |
| Nothing tracks on Firefox | Use Chrome/Edge for the best MediaPipe performance; inspect the console for errors |
| Sound doesn't play | Interact with the page first (autoplay policy) — pressing **START** unlocks audio |
| Low FPS | Close other tabs, improve lighting, and use a Chromium browser for GPU-accelerated canvas |
| “Effect asset failed to load” | Confirm `assets/*.mp4` and `assets/*.mp3` exist next to `index.html` and that you're using a server |

## 🔍 Debugging

A minimal debug handle is exposed on the window for tinkerers:

```js
window.__SHINOBI__; // { state, start, reset, trigger, processResults }
```

You can drive the whole app from the console — `trigger('left')` fires a Rasengan, for example.

## 📄 License

No `LICENSE` file is included yet, so the default *all rights reserved* rules apply. If you'd like to share this openly, add a license file (e.g. MIT) and update the badge above.

---

<p align="center">Made with ⚡ for Naruto fans who are also ML nerds 🌙</p>
