# Faceless YouTube Shorts pipeline on Windows — free guide + repurposing service

Turn one long 16:9 video into ready-to-post vertical **Shorts, Reels and TikToks**:
true 9:16 framing, burned-in captions, and **distinct moments** (not the same
60 seconds re-cropped five times).

- 📖 **Free technical guides (the whole stack, no signup):**
  - [How to build a faceless YouTube Shorts pipeline on Windows](https://aldow3n-a11y.github.io/shorts-repurposing/guide.html) — ffmpeg vertical converter, free TTS, free b-roll APIs, measured view data.
  - [Automate video editing with Python](https://aldow3n-a11y.github.io/shorts-repurposing/python-video-automation.html) — batch processing, caption burn-in, TTS narration, stock b-roll, measured results.
  - [How to earn as an AI freelancer from Indonesia](https://aldow3n-a11y.github.io/shorts-repurposing/freelance.html) — verified platforms (Outlier, Appen, Sribu), real rates, payout rails.
  - [How to sell shorts repurposing as a freelance service](https://aldow3n-a11y.github.io/shorts-repurposing/sell-service.html) — demand data, pricing, delivery workflow, first-client playbook.
- 🛒 **Done-for-you service (pricing + 30-second demo reel):** [https://aldow3n-a11y.github.io/shorts-repurposing/](https://aldow3n-a11y.github.io/shorts-repurposing/)

AI-assisted, human-reviewed, disclosed up front.

---

## The stack (all free)

| Component | Role | Cost |
|---|---|---|
| **Python + ffmpeg** | the actual video math — 16:9 → 1080×1920 | free |
| **Fish Audio TTS** | human-sounding narration for generated video | free tier |
| **Pexels + Pixabay APIs** | stock b-roll pulled programmatically | free API keys |
| **Remotion** (optional) | animated lower-thirds, on-screen charts | free/OSS |

No GPU required. One conversion runs in **20–60 s** on a mid-range laptop CPU.

## The core trick: one ffmpeg filter chain

Scale a copy of the frame to fill the vertical canvas, blur + darken it as the
background, then overlay the original at full width and centred — no black bars, and
captions burned into the source stay readable because the foreground keeps full width.

```
[0:v]scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920,boxblur=20:2,eq=brightness=-0.18[bg];[0:v]scale=1080:-2[fg];[bg][fg]overlay=(W-w)/2:(H-h)/2
```

Runnable:

```bash
ffmpeg -y -hide_banner -loglevel error -i input.mp4 \
  -filter_complex "[0:v]scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920,boxblur=20:2,eq=brightness=-0.18[bg];[0:v]scale=1080:-2[fg];[bg][fg]overlay=(W-w)/2:(H-h)/2" \
  -c:v libx264 -preset veryfast -crf 21 -c:a aac -b:a 128k \
  -movflags +faststart short.mp4
```

Full walkthrough — batch mode, audio-energy cut detection, the before/after proof
reel, and the Windows/MSYS path pitfall — is in the
[guide](https://aldow3n-a11y.github.io/shorts-repurposing/guide.html).

## Why "distinct moments" is a compliance requirement

YouTube tightened its **inauthentic content** policy in July 2025 and enforced it in a
January 2026 wave: mass-produced, templated or minimally-modified reused content is not
eligible for monetisation. A Short that is your long video re-cropped is that exact
pattern. Five *different* high-energy moments, each with its own hook, are not. Same
source file, completely different risk profile.

## Measured data (our own channel, not industry averages)

| What was measured | Result |
|---|---|
| First episode, 4 h after going public | **0 views** |
| Rank on a search for its own exact title | **25th of 25** |
| Channel findable by searching its name | **No** |
| AI-explainer keywords scored for winnability | **8 of 8 saturated** (incumbents 15k–947k subs) |
| Views needed for 4,000 watch hours @ ~90 s/view | **~320,000** |
| Same 4,000 hours @ ~9 min/view | **~53,000** |

Three conclusions, all against the common advice:

1. **Tags do not buy rank on a channel with no history** — ranking last on your own
   exact title is an authority problem, not a metadata problem.
2. **Length is a 6× lever** on the hardest monetisation gate (320k vs 53k views).
   Chasing dozens of 60-second Shorts is the most expensive route to 4,000 hours.
3. **Only build for queries where the top-10 title-match is ~zero.** Score the
   competition *before* writing a script — ten search results cost a fraction of one
   upload's API quota and hours less than a render.

**The pipeline is the asset; the channel is not.** A channel needs authority you cannot
shortcut with tooling. A buyer of clips needs only a working deliverable — which this
stack produces in under a minute per clip.

---

## Done-for-you pricing

| Package | Price | What you get |
|---|---|---|
| Starter | **$15** | 3 Shorts, source up to 20 min, 1 revision |
| Growth | **$35** | 6 Shorts, source up to 40 min, hook-first re-order, 2 revisions |
| Channel Pack | **$75** | 10 Shorts, source up to 60 min, titles/descriptions/hashtags + vertical thumbnails |
| Monthly retainer | **$249/mo** | 20 Shorts from your uploads |

Add-ons: +3 Shorts $12 · 24 h rush $10 · vertical thumbnail set $8.

**How to order:** open a request through the pre-filled issue form linked on the
[offer page](https://aldow3n-a11y.github.io/shorts-repurposing/). A quote comes back the same day; payment is arranged after you
agree to it. You keep full control of scheduling and your logins — nothing is ever
posted on your behalf.

## AI disclosure

The rendering, cut detection and draft copy are produced by software (including AI
components); a human reviews every deliverable before it ships. This README and the
linked guide were written with AI assistance. The commands above are from a pipeline in
production and the numbers in the table are our own measurements.

## Topics

`ffmpeg` · `youtube-shorts` · `video-automation` · `faceless-youtube` · `python` ·
`windows` · `short-form-video` · `content-repurposing` · `tts` · `remotion` ·
`python-video-automation` · `batch-video-editing` · `freelance` · `indonesia`
