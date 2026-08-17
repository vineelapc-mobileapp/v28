# EEE Practice App — v28

Teachers can now upload a video file directly, not just paste a link — and
either way, students see nothing until the "Video is ready" box is
explicitly ticked, for both correct and wrong answers, everywhere a video
could show up.

## The honest tradeoff (read this first)

Your whole question bank lives in one file (`questions.json`) that every
student re-downloads each time they open the app. A video link adds
almost nothing to that file's size. A video file uploaded directly gets
embedded as raw data inside that same file - so it directly affects how
much every student downloads, every time.

That's why direct upload is capped at ~15 MB (roughly a short 1-2
minute clip at modest quality). Longer or higher-quality videos should
still use a Link (YouTube unlisted, Google Drive) - same as before,
completely free, no size limit, and the question bank stays light for
students on mobile data.

## Folder structure

```
v28/
├── app.js                    # *NEW* Plays uploaded video files natively; all video visibility now requires an actual source too
├── upload.js                    # *NEW* "Upload Video File" button, 15 MB size check, updated exports
├── index.html                      # *NEW* <video> element added alongside the existing iframe
├── style.css                          # *NEW* Styling for the native video player
├── upload.html, home.html, manifest*.json, data/   # Unchanged from v27
├── service-worker.js                                  # Cache bumped to v28
├── libs/, icons/
└── README.md

v27/, v26/, v25/, v24/, v23/, v22/, v21/, v20/, v19/, v18/, v17/, v16/, v15/, v14/, v13/, v12/, v11/, v10/, v9/, v8/, v7/, v6/, v5/, v4/, v3/, v2/, v1/   # All untouched
```

## How to add a video (Teacher Upload)

Every question now shows two video options, either one works:

1. Video link - paste a YouTube/Drive URL, exactly as before. Best for
   anything longer than a minute or two.
2. "Upload Video File" - pick a video directly from your phone/
   computer. Shows a live preview player and a "Remove uploaded video"
   option once attached. Files over 15 MB are rejected with a clear
   message telling you to use a link instead.

Either way, nothing reaches students until you tick "Video is ready -
show it to students". Unticked, students see zero video-related UI in
any case - no popup, no "Watch Video Solution" link, anywhere, for correct
or wrong answers. This lets you publish a question with just the text
explanation the moment it's written, and add the video whenever it's
actually ready, from anywhere.

## What students see

Identical experience whether the video is an uploaded file or a link -
same popup, same "Watch Video Solution" links in both the correct-answer
and wrong-answer panels, same Results screen link. An uploaded file plays
in a native video player right in the app; a link plays via embedded
YouTube/Drive player, same as before.

## Verified before shipping

Tested the complete pipeline for real: uploaded an actual video file
through Teacher Upload, confirmed the preview player and size-check both
work, downloaded the resulting data, loaded it as a student, answered
wrong, tapped Watch Now, and confirmed a real video genuinely plays back
with correct duration and dimensions - not just that the code looks right.

## Changelog

### v28 — Direct video file upload (alongside links)
- **<span style="color:red">**\*NEW\*** "Upload Video File" button</span>** in Teacher Upload - pick a video directly, no link needed, for short clips.
- **<span style="color:red">**\*NEW\*** 15 MB size cap with a clear warning</span>** steering longer videos back to a Link, since file size directly affects every student's download.
- **<span style="color:red">**\*NEW\*** Native video playback</span>** for uploaded files, alongside the existing iframe for links.
- **<span style="color:red">**\*NEW\*** Video visibility requires both the Ready tick AND an actual source</span>** (file or link) - can't accidentally show an empty video prompt.
- **<span style="color:red">**\*NEW\*** Exports (CSV, PPT) reflect the new video-file field</span>**.
- No changes to question editing, math rendering, Teacher PIN protection, or anything else from v27.

## Still pending

- Real question content for the syllabus topics
- Bring back "Ask a Doubt" once students are onboarded (from v17)
- Firebase backend for Student Marks + Doubts tabs (still your call — see v10)
- Level-2 unlock gated on Level-1 score
- Desktop `.exe` project not yet synced past v7
