# FlowClip — Usage Guide for Maximum Clipping Results

How to get the best clips out of FlowClip: the setup that matters, the workflow,
and the settings worth touching. Everything here is based on how the tool
actually works under the hood.

## 1. One-time setup that decides your clip quality

**Pick a good AI model — this is the single biggest quality lever.**
FlowClip's "clip scout" is an AI that reads the transcript and picks the moments
a stranger would keep watching. A weak model picks weak moments.

- **Settings → AI**, choose a provider, paste the key, press **Find models**,
  pick the model, then **Save and test**.
- Good defaults: **Gemini 2.5 Flash** (fast, cheap, strong at this), or
  **Groq — llama-3.3-70b-versatile** (very fast). Claude / GPT-class models also
  work well. Avoid the smallest "mini/nano" models for scouting if you can —
  they miss context and jokes.
- **No key at all** still works, but clips are then picked by *loudness only*
  (score fixed at 50, hook "WAIT FOR IT"). Fine for a test, not for results.
- A local model via **Ollama** costs nothing but scouts noticeably worse and
  slower. Use it for privacy or offline work, not for best picks.

**Install ffmpeg** if the dashboard says it's missing — nothing renders without it.

## 2. The workflow (per video)

1. Paste a **YouTube / Twitch / Kick link** or upload a file.
2. FlowClip downloads **audio first** and transcribes it on your own machine
   (the speech model is local — audio never leaves your computer). If the
   YouTube video has good captions, it uses those first and only re-transcribes
   the chosen clips locally for word-perfect caption timing.
3. The AI scout reads the transcript in windows, scores every candidate moment
   **0–100**, writes the hook (max 5 words), title, description and hashtags,
   and marks the loud/exciting spots it noticed.
4. Clip boundaries are **snapped to real sentence ends** — clips start and stop
   where a thought completes, not mid-sentence.
5. Each clip renders at **1080×1920 (9:16)** with word-by-word pop captions and
   the hook on screen, audio normalised to −14 LUFS.
6. Review, then post yourself or let the scheduler do it.

Long videos are fine: anything over ~20 minutes is processed in 10-minute
blocks, and if you stop halfway, the work is checkpointed and resumes.

## 3. Source material — what clips well

- **Clear, single-speaker speech wins**: podcasts, commentary, interviews,
  lectures, story-time videos. The scout can only pick what the transcript shows.
- **Streams with an active Twitch chat** clip best live (see §6) — chat spikes
  are one of the two judges.
- Music-heavy or near-silent videos give the scout nothing to read; loudness
  fallback is all you get.
- Two people talking over each other, heavy background music, or bad mic audio
  hurt transcription, and every later step inherits that.

## 4. Clip settings per creator (workspace)

Each creator/workspace has its own settings. The defaults are sane:

- **Clip length: 15–60 seconds.** For TikTok/Reels/Shorts, most winners land at
  25–45 s. Shorten the max if your clips feel padded; lengthen it for
  story/podcast moments that need the full build-up.
- **Max clips per video: 6.** Raise it for long podcasts (more raw material),
  lower it when you only want the very best.
- Overlapping candidates are de-duplicated automatically — the higher-scored
  one wins.
- **Gaming streams:** pick the game in the creator settings. FlowClip has
  built-in rules and forced hashtags for 23 games, and it auto-detects the
  facecam area so the layout keeps your face in frame.

## 5. Captions and layout

- Three caption styles; all use **word-pop captions** timed from the real
  speech, with the active word enlarged.
- Layouts: blurred-fill, zoom, crop, and a gameplay layout. For a talking head,
  keep the speaker centred — the crop follows the detected face area.
- **Urdu/Hindi content:** transcription handles it, and captions are always
  rendered in **Roman script** automatically (that's how the audience reads
  them anyway). Other languages are translated line-by-line by the AI.

## 6. Live clipping (streams)

- Add the creator's channel and start a live session. FlowClip records a
  **rolling 20-minute buffer** — anything older than 20 minutes is gone, so
  start the session when the stream starts.
- A clip is made when **two independent judges agree**: one reads only the
  transcript (is this moment actually good?), the other reads only the signals
  (loudness spike, chat spike). This kills most false alarms.
- Other triggers: the regular ~3-minute check, a spike, the streamer **saying
  the word "clip"**, your own custom trigger words, or the manual button.
- Chat spikes count **distinct chatters, not message count** — one person
  spamming doesn't trigger a clip. Chat signal works on **Twitch**; YouTube and
  Kick live clipping relies on loudness + transcript.
- Live renders go through a separate queue, so a live clip doesn't wait behind
  a long VOD job.

## 7. Reviewing — where results are actually made

- **Scores are a ranking, not a promise.** A 90 in a boring video can be worse
  than a 70 in a great one. Watch the first 2 seconds of every clip you post:
  if the hook doesn't land instantly, the clip won't travel, whatever the score.
- Edit the title/hook when the AI's wording is flat — the hook text stays on
  screen for the whole clip.
- Check captions on one clip per batch. If a word is consistently wrong, it's
  the source audio, not the caption engine.

## 8. Posting

- Connect **YouTube, Instagram, TikTok** once (the one-time app setup is in
  DEPLOY.md). Posting uses the official APIs — no browser automation.
- **Auto-post threshold: score ≥ 75.** Below that, clips wait for your review.
  Raise it if auto-posts disappoint; lower it only for channels you trust.
- **Spacing and caps** (per creator): default gap ~45 minutes between posts,
  daily cap ~6. Platforms punish burst-posting; the spacing is doing you a
  favour — don't set the gap to 0.
- **TikTok warning:** until your TikTok app is audited by TikTok, API posts land
  as **private**. After any first post, open TikTok and check the visibility;
  if it's "Only me", either finish the audit or post that account manually /
  through TikTok Studio.
- YouTube uploads get **#Shorts** appended automatically. View counts are
  tracked for YouTube and Instagram (TikTok's API doesn't share them back).

## 9. Looking after the install

- Keep the folder path **short** (`C:\flowclip`) — long paths break the speech
  model on Windows.
- FlowClip pauses new work when the machine is nearly full (under ~3 GB free
  disk, very high CPU, or low RAM). If jobs "won't start", check disk space
  first — rendered clips pile up in the data folder.
- Everything lives in the **data folder** (jobs, clips, settings, connected
  accounts). Back that folder up and you've backed up FlowClip. Move it only
  through the dashboard's storage settings, not by hand.
- One FlowClip process serves everyone on that machine; don't start it twice.

## 10. Quick recipe — best results, minimal effort

1. Gemini 2.5 Flash (or Groq 70B) key in Settings → AI.
2. One workspace per creator, right game selected for gamers.
3. Feed it clear-speech videos or go live with the session running from the
   start of the stream.
4. Clip length 20–50 s for short-form; 6 clips per video to start.
5. Review everything under score 75 yourself; let ≥75 auto-post with the
   default spacing.
6. After posting to TikTok, verify the post is actually public.
