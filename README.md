# Scary Sound Listener

Simple single-page app that listens to your microphone and plays a random MP3 from a selected folder when it detects sound above a configurable threshold.

Files
- `Scary_Sound.html` — main single-page application. Open this in a browser.
- `Sounds/` — your folder for MP3 files (you can also pick any folder or drag & drop files into the page).

Quick usage
1. Open a Chromium-based browser (Chrome or Edge recommended) and open `Scary_Sound.html`.
2. For the most reliable behavior run a local server and open the page via `http://localhost:8000/Scary_Sound.html` (see below).
3. Click **Pick Sounds folder** and select the folder that contains your `.mp3` files, or use the fallback **Or choose folder via file picker**, or drag & drop MP3s to the drop area.
4. Tune the **Threshold** and **Cooldown** to your liking. Lower threshold = more sensitive.
5. Click **Start listening** and allow microphone access when the browser prompts you.
6. Make a sound — when the app detects audio louder than the threshold it will pick a random MP3 from the loaded list and play it.

Local server (recommended)
Serving the files over a local server avoids security restrictions and provides the best compatibility for the Directory Picker.

PowerShell (Windows) examples:
```powershell
# If Python is available in PATH
python -m http.server 8000

# Or using the Windows Python launcher
py -m http.server 8000
```

Then open in your browser:

    http://localhost:8000/Scary_Sound.html

Notes & troubleshooting
- Directory Picker: supported in Chromium-based browsers. If your browser doesn't support it, use the file-picker fallback or drag & drop.
- Microphone permission: the browser will request access. If you deny it, the app cannot listen.
- Autoplay: some browsers block autoplay of audio unless the page has a prior user gesture. If playback is blocked, click the audio control's Play button or click anywhere on the page once (the app attempts to resume the AudioContext on first click).
- If you want the app to automatically use the `Sounds/` folder without picking it inside the page, run a local server and navigate to the file listing at `http://localhost:8000/Sounds/` and add MP3s there; then use the file picker or drag & drop to load them into the app.

````markdown
# Scary Sound Listener

Simple single-page app that listens to your microphone and plays a random MP3 from a selected folder when it detects sound above a configurable threshold.

Files
- `Scary_Sound.html` — main single-page application. Open this in a browser.
- `prank.html` — the lightweight "Elf sound effect prank" page: listen for 1 or 2 quick sounds and play a specific clip from `Sounds/`.
- `Sounds/` — your folder for MP3 files (the sample files `hi.mp3` and `hi-mommy-child-voice.mp3` are included in this repo).

Quick usage
1. Open a Chromium-based browser (Chrome or Edge recommended) and open `prank.html` or `Scary_Sound.html`.
2. For the most reliable behavior run a local server and open the page via `http://localhost:8000/prank.html` (see below). Browsers often restrict microphone and autoplay features on pages opened via file://.
3. Click **Start listening** and allow microphone access when the browser prompts you.
4. Make one short audible sound (a tap, clap, or "hi"). The page will play `Sounds/hi.mp3`.
5. Make two short sounds in quick succession (two claps). The page will play `Sounds/hi-mommy-child-voice.mp3`.

Local server (recommended)
Serving the files over a local server avoids security restrictions and provides the best compatibility.

PowerShell (Windows) examples:
```powershell
# If Python is available in PATH
python -m http.server 8000

# Or using the Windows Python launcher
py -m http.server 8000
```

Then open in your browser:

    http://localhost:8000/prank.html

Notes & troubleshooting
- Microphone permission: the browser will request access. If you deny it, the app cannot listen.
- Autoplay: some browsers block autoplay of audio unless the page has a prior user gesture. If playback is blocked, click anywhere on the page to give a user gesture; the page attempts to resume the AudioContext on first click.
- Sensitivity: use the slider labeled "Sensitivity" to tweak detection. Lower values are more sensitive (catch quieter sounds) but may give false positives.
- If the app doesn't detect sounds reliably, try increasing the input volume or decreasing the threshold slightly.

Prank details & limitations
- Detection algorithm: the page uses a simple RMS (volume) peak detector with a short debounce and a ~900ms grouping window to distinguish single vs double sounds. It's intentionally simple; it works well for obvious taps or claps but may fail for very quiet or very noisy environments.
- Reliable operation requires a modern Chromium-based browser (Chrome, Edge). Some browsers may behave differently.

Customization ideas
- Improve detection by adding a short-time average, bandpass filtering, or dedicated clap-detection logic.
- Add automatic loading of the `Sounds/` directory when served from a local server (would require a tiny server-side script to list files).

If you'd like, I can add a small helper script to auto-generate a JSON manifest of the `Sounds/` folder so the page can load sounds automatically when run from a local server.

---
Generated: November 9, 2025 (updated with `prank.html` instructions)

````
