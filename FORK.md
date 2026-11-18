# Our fork

This project is a fork of **PeakCut** by the PeakCut contributors
(https://github.com/haziqahmedqasmi/PeakCut), licensed under the MIT licence —
see `LICENSE`, which is kept unchanged as the licence requires. Bundled caption
fonts remain under the SIL Open Font License (texts in `studio/fonts/`).

Forked on 2026-11-18. Upstream commit at fork time: `1bef2b4` ("Made to work on game streams").

## Changes from upstream

1. **No phoning home.** The update checker no longer points at the upstream
   repository by default (`studio/updates.py`): it stays off until
   `PEAKCUT_UPDATE_REPO` is set to our own repository.
2. **No upstream personal links.** The dashboard's "Star on GitHub" and
   "Follow me" buttons pointed at the original author's repo and Instagram.
   Their defaults are now empty (`studio/config.py`), so the buttons simply
   don't appear until `PEAKCUT_REPO_URL` / `PEAKCUT_FOLLOW_URL` are set to ours.
3. **Caption timing fix (2026-11-18).** On the owner's clips the captions ran
   a steady 0.6–1.0 s behind the voice, whatever the source length.
   `CAPTION_LEAD` in `studio/render.py` is now 0.8, so captions render 0.8 s
   earlier. Fine-tune that one number if clips come out early or still late.

## Rebrand: FlowClip (2026-11-18)

- The product is now named **FlowClip**. All user-visible text — pages, titles,
  emails, messages, docs, cookie and storage names — says FlowClip.
- Internal plumbing keeps the `PEAKCUT_*` environment variable names, so
  existing `.env` files and the test suite keep working unchanged.
- Still pending: the logo artwork in `web/brand/` (logo.svg, logo-light.svg,
  logo-email.png) draws the old wordmark as vector shapes — it needs a new
  FlowClip logo design, not a text edit.

## Still to do

- New FlowClip logo artwork (see above).
- Push to our own GitHub repository, then set `PEAKCUT_UPDATE_REPO` to it.
- Roadmap from the reverse-engineering report
  (`~/workspace/research_notes/peakcut-reverse-engineering/REPORT.md`):
  real database for domain data, encrypted platform tokens, truly chunked
  YouTube uploads.
