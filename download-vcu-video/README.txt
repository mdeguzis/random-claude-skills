VCU Kaltura Video Downloads
===========================

This folder contains videos downloaded from VCU Canvas (Kaltura player).

HOW TO DOWNLOAD A VIDEO
-----------------------
1. Open the video on the VCU Canvas/Kaltura website.
2. Right-click the video player > "Debug Info"
3. Copy the full debug info JSON.
4. In Claude Code, run: /download-vcu-video
5. Paste the debug info when prompted.
6. The video will be saved to this folder.

REQUIREMENTS
------------
- yt-dlp (install: brew install yt-dlp)

NOTES
-----
- The Kaltura Session (KS) token embedded in the manifest URL expires within a few hours.
  If the download fails with a 403/401, reload the video in the browser and grab fresh debug info.
- Videos are saved as MP4 files named by their Kaltura entry ID (e.g. 1_780del69.mp4).
