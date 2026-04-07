# n8n 50 FPS Image-Sequence Video Generator

This repository contains an n8n workflow template that:

1. Accepts `text_prompt`, `negative_prompt`, `audio_url`, and `duration_seconds` input.
2. Validates duration is between **5 seconds and 1800 seconds (30 minutes)**.
3. Generates exactly `duration_seconds * 50` frame prompt schemas.
4. Sends one schema block per frame to:
   `https://ppbprahann.app.n8n.cloud/webhook/e665ed44-516c-45a2-afe6-c291e2d7f02a`
5. Collects generated image URLs, downloads assets, and renders a 50 FPS MP4 with audio.
6. Returns the resulting video binary from the original webhook response.

## Workflow file

- `workflows/video_generator_50fps.json`

## Input payload example

```json
{
  "text_prompt": "A futuristic city at sunset, smooth camera pan",
  "negative_prompt": "blurry, low quality, watermark, distorted",
  "audio_url": "https://example.com/audio/song.mp3",
  "duration_seconds": 12,
  "width": 1024,
  "height": 1024
}
```

## Notes

- The workflow assumes `python3` and `ffmpeg` are available in your n8n runtime.
- Image webhook responses are expected to include one of:
  - `image_url`
  - `url`
  - `output_url`
- Rendering very long videos at 50 FPS can require significant compute and storage.
