# cartoon-stick

A Claude skill that makes vertical (9:16) cartoon stick-figure animations, 20 to 60 seconds long, for YouTube Shorts, Instagram Reels and TikTok. Think "what if" explainers: a hook, a common belief, a twist, and a payoff, told by a narrator over bright, hand-drawn-in-code stick figures.

Made by **Storyteller ID**.

## What you get

- A finished `.mp4` at 1080x1920, 30 fps
- Stick people with big white heads and expressive faces, drawn entirely in code (no image assets)
- Word-synced captions: 1 to 2 words, lowercase, Poppins Bold, placed in the lower third
- Whip transitions, push-ins, impact bursts, and a quiet synthesised music bed with sound effects
- A worked example included: `engine/template` is a finished 37 s reel, "What if pirate eye patches had nothing to do with missing eyes?"

## How it works

When the skill starts it always asks two questions:

1. **How long?** 20, 30, 40 seconds, or a custom length.
2. **Which audio?**
   - **Provided audio**: the voiceover is generated from the script with the built-in voice (Kokoro, free). ElevenLabs is also supported if you set `ELEVENLABS_API_KEY`.
   - **My own audio**: you supply your own voiceover recording and the skill animates to it.

Then it uses your topic or script if you gave one; otherwise it picks the best idea itself and writes the script for you to approve.

After you approve the script, it generates the voice, aligns every word, designs about one shot every 3 to 3.5 seconds, checks a few stills, mixes the sound, renders the frames in a headless browser, and encodes the video with ffmpeg.

## Requirements

- Python 3.9+
- Node.js and npm
- ffmpeg
- Internet access to PyPI, npm and github.com (for the one-time install)
- About 0.8 GB of disk for the voice and word-timing models

Works in Claude.ai (code execution), Cowork, Claude Code, or any normal terminal. Claude Code is not required.

## Install

Copy the `cartoon-stick/` folder into your skills directory, or upload the `.skill` file in your Claude app's skill settings.

The first run does a one-time setup (about 1.5 minutes) into a cache folder, `~/.cache/cartoon-stick-kit` by default (override with `CS_KIT`):

```bash
bash cartoon-stick/scripts/setup.sh
```

This installs Playwright and Chromium (reused if already present), the Python packages, and the models: Kokoro for the voice and Parakeet for word timing.

## Use it

In Claude, run `/cartoon-stick`, or just ask for a stickman, cartoon stick, stick figure or "what if" explainer video.

To try the example by hand:

```bash
cp -r cartoon-stick/engine/template ./reels/pirate
WORKERS=$(nproc) bash cartoon-stick/engine/make.sh ./reels/pirate
```

Rendering draws every frame in a browser, so a 37 s reel takes roughly 10 to 20 minutes on 3 CPU cores. More cores are faster. In sandboxes that kill commands after about 10 minutes, run it in the background:

```bash
WORKERS=$(nproc) nohup bash cartoon-stick/engine/make.sh ./reels/pirate > make.log 2>&1 &
tail -3 make.log
```

`make.sh` options:

```bash
make.sh <reel-folder>                  # reuse the voice already in audio/, or the free Kokoro take
make.sh <reel-folder> kokoro           # new take in the built-in voice
make.sh <reel-folder> elevenlabs       # new ElevenLabs take (needs ELEVENLABS_API_KEY)
make.sh <reel-folder> path/to/take.mp3 # your own recording
AUDIO_ONLY=1 make.sh <reel-folder>     # remix the sound only, reuse the last picture
```

## Project layout

```
cartoon-stick/
├── SKILL.md                  # the skill instructions Claude follows
├── scripts/
│   └── setup.sh              # one-time install of browser, packages and models
└── engine/
    ├── make.sh               # voice -> word timings -> sound -> frames -> .mp4
    ├── tools/                # render.js, tts_kokoro.py, tts_elevenlabs.py, align.py
    └── template/             # a complete example reel
        ├── script.json       # voiceover, one sentence per entry
        ├── captions.json     # optional caption text swaps
        ├── audio.py          # music and SFX, synthesised in code
        ├── audio/            # voiceover and reference word timings
        └── web/              # shots.js, chars.js, env.js, lib.js, main.js, fonts
```

A reel is just one folder. The shot list lives in `web/shots.js`, the stick rig and faces in `chars.js`, and props such as sky, sea, ships and barrels in `env.js`.

## Language

Everything is in English: scripts, voiceover and captions. The built-in voice and the word aligner are English-only, and English keeps captions and shots in sync with the voice. If your script or recording is in another language, sync will drift; translating it to English first is recommended.

## Credits and licenses

- Created by **Storyteller ID**
- Voice: [kokoro-onnx](https://github.com/thewh1teagle/kokoro-onnx)
- Word timing: [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) with NVIDIA Parakeet
- Rendering: [Playwright](https://playwright.dev/) and ffmpeg
- Fonts: Poppins and Lora, both under the SIL Open Font License (license texts are in `engine/template/web/fonts/`)

## License

The skill is released under the [MIT License](https://github.com/storytellerid/cartoon-stick/blob/main/LICENSE). Copyright (c) 2026 Storyteller ID.
