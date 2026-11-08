# AGENTS.md

Math animation scenes (ManimCE) for the MasterMathematics YouTube channel.
Repo: https://github.com/matthiasmitwittfogel/math-in-shapes

## Structure

- `shorts/` — one self-contained Manim scene file per YouTube Short, named `YYYYMMDD_topic.py`.
- `videos/` — longer videos, one subdirectory per video, named `YYYYMMDD_topic/`.
- `covers/` — committed `.jpg` YouTube thumbnails, one per scene.
- `tools/` — cover generators (`build_covers.py`, `build_sixths_cover.py`).
- `render_all.py` — batch-renders every scene discovered in `shorts/` and `videos/`.
- `work/` — cover-build scratch (TeX, manifests). Git-ignored, never commit.
- `media/` — Manim render output. Git-ignored.

## Setup & Build

```bash
uv sync                                # install deps from uv.lock (Python >= 3.11)
uv sync --extra voiceover              # optional: manim-voiceover + Azure TTS
```

## Render

```bash
uv run manim -pqm shorts/20230905_apple_logo.py AppleLogo   # single scene
uv run python render_all.py                                  # all scenes, medium quality
uv run python render_all.py --dry-run                        # list what would render
```

Quality presets: `-ql` (480p15), `-qm` (720p30, default), `-qh` (1080p60), `-qk` (4K).
`render_all.py` never auto-plays; add `-p` for preview.

## Covers

```bash
uv run python tools/build_covers.py
```

Requires a working LaTeX install (MiKTeX on Windows) for Tex-based mobjects.

## Conventions

- Style: `ruff` + `black`, line-length 100, target py311 (see `pyproject.toml`).
- Scene files are plain ManimCE scripts; voiceover is opt-in and must stay disabled by default.
- Secrets go in `.env` (git-ignored); never commit Azure credentials.
- README keeps a table mapping every scene file to its YouTube URL — update it when adding a scene.
