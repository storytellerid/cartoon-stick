# cartoon-stick

> Made by **Storyteller ID**.

## Introduction

**cartoon-stick** is a skill that makes vertical (9:16) cartoon stick-figure animations, 20 to 45 seconds long. The videos are built for **YouTube Shorts, Instagram Reels and TikTok**, especially short, funny, easy-to-follow "what if" explainers.

The skill handles the whole process from start to finish: finding ideas, writing the script, generating the voiceover, animating the scenes, adding music and sound effects, and rendering a ready-to-upload `.mp4`. A finished example is included: a 37-second reel titled *"What if pirate eye patches had nothing to do with missing eyes?"*

Run it with `/cartoon-stick`, or just ask for a stickman, cartoon stick, stick figure or "what if" explainer video for Shorts, Reels or TikTok.

## Features

### Three ways to start
Every time the skill runs, it first asks where you want to begin and how long the video should be.

- **10 ideas or scripts**: Claude writes 10 ideas, you pick one, and Claude writes the script.
- **I already have a script and a voiceover**: Claude only makes the animation.
- **I have a script but no voiceover**: Claude generates the voiceover from your script, then animates it.

### Flexible length
Choose 20, 30 or 40 seconds, or set a custom length (15 to 60 seconds recommended). Script length and shot count adjust automatically to the length you pick.

### Hook, Twist and Source rule
Every idea and every script always shows these three parts:

- **Hook**: the opening line that holds the viewer from the first second.
- **Twist**: the surprising turn or fact that flips the common belief.
- **Source**: a checkable source. Claude searches the web for it and never invents a source or URL. Claims that are only theories are worded cautiously.

### Voiceover
- Free built-in voice with **Kokoro**.
- **ElevenLabs** support (requires an API key).
- Or use your own recording.
- Every word is aligned to the voice automatically, so captions and visuals stay in sync. If you swap the voice but keep the same words, the animation adapts by itself with no re-editing.

### Stick-figure animation
- Stick characters with big white heads and expressive faces.
- Backgrounds, props and characters are all drawn in code, with no external image assets.
- Bright saturated palette with ink outlines, soft contact shadows, slow push-ins with handheld drift, and whip transitions with motion blur.
- Impacts come with a burst, a shake and a flash.
- Layouts respect Instagram's safe area so faces and key props are never cropped.

### Automatic captions
Shorts-style captions in Poppins Bold: white with a dark outline, one to two words at a time, lowercase, placed about 70% down the screen. Caption text can be swapped through `captions.json`, for example turning "twenty five" into "25".

### Music and sound effects
Music and sound effects are synthesized in code. The music is a quiet plucked underscore that ducks under the voice, and sound effects are placed on the exact words they belong to.

### Upload-ready output
The final result is a 1080x1920 `.mp4` at 30 fps with normalized loudness. Before the full render, you can preview a few still frames to check the look.

### Runs anywhere
The skill works in Claude.ai, Cowork, Claude Code or any terminal with a shell, and Claude Code is not required. It needs ffmpeg, Node, Python 3.9+ and an internet connection for the one-time setup, which takes about 1.5 minutes and downloads roughly 0.8 GB of voice models.

## Notes

- Ideas, scripts, voiceover and captions are all in **English**, because the built-in voice (Kokoro) and the word aligner (Parakeet) only support English. If your script or recording is in another language, sync can drift, and the skill will offer to translate it to English.
- Rendering draws frames one by one in a browser, so a 37-second reel takes roughly 10 to 20 minutes on 3 CPU cores, and less with more cores.
