# Sound Synthesis Midterm — Dual‑Tone Synth (Max/MSP)

This Max/MSP patch implements a dual‑tone synthesizer with selectable engines, ADSR envelope shaping, and a rhythmic trigger at 120 BPM (two notes per second). It is designed to avoid clicks between successive notes and to take the fundamental frequency from a **K‑slider**.

##  Features
- **Additive Synth (Odd Harmonics):** Sub‑patch that sums the first **five odd harmonics** of a fundamental.
- **Bell‑Like Synth:** Sub‑patch with two partials: **fundamental** and **fundamental × 1.414**.
- **Engine Selector (Radio Group):** Choose which sub‑patch (Additive or Bell) is active.
- **ADSR Envelope (per trigger):**
  - **Attack:** 50 ms → 1.0
  - **Decay:** 75 ms → 0.7
  - **Sustain:** 0.7 held for 125 ms
  - **Release:** 200 ms → 0.0
- **No Clicks:** Envelope and amplitude ramps ensure smooth transitions.
- **K‑Slider Input:** Fundamental frequency comes from a **K‑slider** UI object.
- **Tempo System:** Triggers at **120 BPM** (2 Hz).

##  Files
- `SoundSynthesis_MidtermProject.maxpat` — main patch
- `img/screenshot.png` — (optional) screenshot of the patch
- `audio/demo.mp3` — (optional) short demo clip (<10 MB)

##  How to Use
1. **Open** `SoundSynthesis_MidtermProject.maxpat` in Max.
2. **Set fundamental** with the **K‑slider**.
3. Use the **radio group** to choose **Additive** or **Bell** engine.
4. **Start the trigger** (120 BPM) and listen.
5. Adjust ADSR parameters if you made them external; defaults are baked in to meet the spec.

##  Implementation Notes
- **Additive sub‑patch:** sums partials at frequencies `f * {1, 3, 5, 7, 9}` with appropriate amplitude scaling to avoid clipping.
- **Bell sub‑patch:** two sine partials at `f` and `f × 1.414` (≈ √2), mixed and sent through the same ADSR.
- **Envelope:** ADSR is applied to signal domain (e.g., `line~`/`function`/`adsr~` approach) to ensure smooth ramps and **no clicks**.
- **120 BPM:** Use `[metro 500]` (ms) → triggers every 500 ms; 120 BPM = 60,000 ms / 120 = **500 ms**.
- **Gain staging:** final output scaled to prevent clipping; monitor with `meter~` if included.

##  Screenshot
- On macOS press **Shift–⌘–4** to capture a region, or **Shift–⌘–5** for window capture.
- Save as `img/screenshot.png` so GitHub shows it in the folder.
- For a clean look: **Lock** the patcher and (optionally) enable **Presentation Mode** before capturing.

##  Requirements
- **Max 8+**
- Basic MIDI/audio interface settings configured in Max

---

© Henry Powell — for educational portfolio use.
