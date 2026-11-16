# Stride Lab

Sprint technique analysis in a single HTML file (English / Russian).

Film a sprint from the side and Stride Lab:

1. Reads the frame rate from the video file (MP4 / MOV).
2. Tracks the athlete on every frame with an on-device pose model (MediaPipe) and finds each touchdown, toe-off and knee drive for both legs.
3. Sends only those key frames to **Gemini**, which places the shoulder, hip, knee, ankle and toe. The app measures every angle from those points.
4. Calculates ground contact, flight time, step rate and left–right balance across all steps.
5. Builds a kinogram and a technique report with ALTIS-based checks, cues and drills, plus an optional Gemini coach summary.

## Gemini

Paste a Gemini API key in Step 1 (get one at [Google AI Studio](https://aistudio.google.com/apikey)). The key is stored only in your browser and sent only to Google. Restrict it to your site in Google Cloud if you host this page publicly.

Models: **Flash-Lite** (default, cheapest, about 1,500 tokens per frame) or **Flash** (a little more precise). A full analysis is about 8 calls.

Without a key the app still works: the pose model finds the frames and joints, and you can drag any point to correct it.

## Run

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```
