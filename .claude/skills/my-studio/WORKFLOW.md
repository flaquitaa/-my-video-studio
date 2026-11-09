# Workflow notes (technical, for Claude)

What worked in this cloud environment (my-video-studio):

- Download Drive videos: `curl -sSL -o in.mov "https://drive.usercontent.google.com/download?id=<FILE_ID>&export=download&confirm=t"` (file must be shared "anyone with the link").
- Transcribe: `npm install hyperframes` in a scratch folder, then `NODE_USE_ENV_PROXY=1 npx hyperframes transcribe audio.wav --json > run.log`. Read `transcript.json` (do not redirect stdout into it). Disable telemetry: `npx hyperframes telemetry disable`.
- Whisper timings drift on raw footage. Cut by silence (`silencedetect=noise=-35dB:d=0.35`, pad 0.09 s), then re-transcribe the cut audio for caption timing.
- Graphics: an HTML page with `render(t)`, screenshotted per frame with Playwright (`omitBackground`) and piped into ffmpeg as a qtrle alpha layer, then overlaid on the base cut.
- Loudness: two-pass `loudnorm=I=-14:TP=-1`.
- Rendered videos stay out of git (`.gitignore`).
