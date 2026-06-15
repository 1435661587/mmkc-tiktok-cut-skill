# mmkc-tiktok-cut-skill
> MMKC project description: Render 9:16 TikTok, Reels, or Shorts videos from AI clips, local assets, or talking-head footage using JSON edit plans and FFmpeg.
> MMKC 项目描述：用 JSON edit plan 和 FFmpeg 把 AI 视频、本地素材或口播素材剪成 9:16 TikTok/Reels/Shorts 成片。


[中文](./README.md) | English

`mmkc-tiktok-cut-skill` is a local FFmpeg editing skill for turning AI videos, talking-head clips, product footage, or multiple source clips into publishable 9:16 TikTok/Reels/Shorts videos.

## Features

- Initialize a structured editing project with raw media, metadata, transcripts, plans, captions, and renders.
- Probe media with `ffprobe` and extract diagnostic frames.
- Optionally transcribe speech.
- Use a JSON edit plan for clips, reframing, captions, overlays, BGM, and export settings.
- Render a 1080x1920 MP4 with FFmpeg and write a render report.

## Install

```bash
mkdir -p ~/.codex/skills
cp -R mmkc-tiktok-cut-skill ~/.codex/skills/
brew install ffmpeg
```

Optionally install Whisper or faster-whisper for transcription.

## Usage

```bash
python3 mmkc-tiktok-cut-skill/scripts/init_project.py \
  mmkc-tiktok-cut-skill/projects/20260611_demo \
  --name demo \
  --inputs "/path/to/source.mp4"

python3 mmkc-tiktok-cut-skill/scripts/probe_media.py \
  mmkc-tiktok-cut-skill/projects/20260611_demo/raw \
  --out mmkc-tiktok-cut-skill/projects/20260611_demo/metadata/media_inventory.json \
  --frames-dir mmkc-tiktok-cut-skill/projects/20260611_demo/diagnostics/frames

python3 mmkc-tiktok-cut-skill/scripts/make_plan.py \
  mmkc-tiktok-cut-skill/projects/20260611_demo \
  --title "TikTok hook" \
  --target-seconds 30

python3 mmkc-tiktok-cut-skill/scripts/render_tiktok_cut.py \
  mmkc-tiktok-cut-skill/projects/20260611_demo/plans/edit_plan.json
```

## Safety

Keep run artifacts, rendered videos, subtitles, transcripts, and diagnostic frames under `projects/` or another local work directory. Do not commit them to the public repository.
