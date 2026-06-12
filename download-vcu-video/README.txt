VCU Kaltura Video Downloads + Transcripts
==========================================

This folder contains videos and transcripts downloaded from VCU Canvas (Kaltura player).

INSTALL THIS SKILL
------------------
Tell Claude Code:
  "Install this skill: https://github.com/mdeguzis/random-claude-skills/tree/main/download-vcu-video"

Or manually copy download-vcu-video.md into ~/.claude/commands/

HOW TO USE
----------
1. Open the video on the VCU Canvas/Kaltura website.
2. Right-click the video player > "Debug Info"
3. Copy the full debug info JSON.
4. In Claude Code, run: /download-vcu-video
5. Paste the debug info when prompted.
6. The video is downloaded, then automatically transcribed and cleaned up into paragraph form.
7. You will be offered the option to rename the output files.
8. Confirm the transcript looks correct — Claude will offer to delete the video file to save space.

REQUIREMENTS
------------
- yt-dlp       (install: brew install yt-dlp)
- ffmpeg       (install: brew install ffmpeg  — required for HLS download and audio extraction)
- mlx-whisper  (install: pip3 install mlx-whisper)

TIMING
------
Transcription of a lecture-length video typically takes 5–10 minutes (average ~5 min, up to ~10 min
for longer or more complex recordings). Plan accordingly.

NOTES
-----
- The Kaltura Session (KS) token embedded in the manifest URL expires within a few hours.
  If the download fails with a 403/401, reload the video in the browser and paste fresh debug info.
- Videos are saved as <entryId>.mp4 and transcripts as <entryId>.txt (e.g. 1_780del69.mp4 / .txt).
  You will be offered a chance to rename both to something descriptive after transcription.
- After confirming the transcript, you can delete the .mp4 to reclaim disk space.
