# Stride Lab

Sprint technique analysis in a single HTML file (English / Russian).

Film a sprint from the side and Stride Lab:

1. Reads the frame rate from the video file (MP4 / MOV).
2. Tracks the athlete on every frame with an on-device pose model (MediaPipe) and finds each touchdown, toe-off and knee drive for both legs.
3. Sends only those key frames to **Gemini**, which places the shoulder, hip, knee, ankle and toe. The app measures every angle from those points.
4. Calculates ground contact, flight time, step rate and left–right balance across all steps.
5. Builds a kinogram and a technique report with ALTIS-based checks, cues and drills, plus an optional Gemini coach summary.

## How the joints are placed

1. The on-device pose model (MediaPipe **heavy**) tracks every person in frame and follows the one who moves the most, so a standing coach or spectators are ignored.
2. On each key frame, **Gemini Flash** places the shoulder and the hip, knee, ankle, heel and toe of **both legs** on a sharp crop of the sprinter.
3. Where the pose model and Gemini agree, the point is averaged; where they disagree (backlight, motion blur) Gemini is used. If Gemini's crop shows the wrong person, it searches the whole frame for the sprinter.
4. The stance leg is used for touchdown and toe-off, the swing leg for knee drive; the other leg is drawn in silver-blue so a wrong point is easy to spot and drag.

Tested on real race video (4K HEVC, 30–240 fps, block starts, a coach and spectators in frame). Against hand-marked knee and ankle positions, Flash-Lite was off by ~80% of a thigh length on average, the old lite pose model ~15%, the heavy model and Gemini Flash ~7–9%.

## Gemini

Paste a Gemini API key in Step 1 (get one at [Google AI Studio](https://aistudio.google.com/apikey)). The key is stored only in your browser and sent only to Google. Restrict it to your site in Google Cloud if you host this page publicly.

Models: **Flash** (default, about 2,500 tokens per key frame) or **Flash-Lite** (cheaper, but much less precise for joints). A full analysis is about 8–15 requests.

Without a key the app still works: the pose model finds the frames and joints, and you can drag any point to correct it.

## Run

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```
