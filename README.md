# Shinobi Vision — Jutsu AR

A browser-based hand-tracking AR experience. Physical left-hand open palm charges **Rasengan**; physical right-hand open palm charges **Chidori**. At 100% the corresponding cinematic MP4 effect is composited over the live camera with black-background removal and synchronized audio.

## Run

Use a local web server (for example VS Code Live Server) and open `index.html`. Webcam access generally requires localhost or HTTPS.

## Included

- MediaPipe Hands, up to two hands
- Physical left/right hand routing
- Progressive chakra charging
- Cinematic Rasengan and Chidori overlays
- Black-background video keying for transparent-looking effects
- Hand-positioned and hand-scaled jutsu placement
- Web Audio API charging sound + jutsu sound scheduling
- Futuristic HUD, telemetry, event stream, reset control

No backend or database is required.
