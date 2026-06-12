# Download VCU Kaltura Video + Transcript

Download a video from VCU Canvas, extract and clean up a transcript, offer to rename the output, and optionally delete the video.

## Steps

1. **Ask the user** to paste the debug info from the video:
   > "Please paste the debug info JSON from the VCU video player (right-click the video > Debug Info > copy all the text)."

2. **Parse** the pasted JSON to extract:
   - `manifestUrl` — the HLS `.m3u8` stream URL
   - `entryId` — used as the default output filename

3. **Download the video** using yt-dlp:
   ```
   PATH="/opt/homebrew/bin:$PATH" /opt/homebrew/bin/yt-dlp --downloader ffmpeg --hls-use-mpegts "<manifestUrl>" -o "/Users/alvinatyr/vcu-video-transcripts/<entryId>.mp4"
   ```

4. **Transcribe the video** using mlx-whisper (this typically takes 5–10 minutes for a lecture-length video):
   ```
   PATH="/opt/homebrew/bin:$PATH" mlx_whisper --model mlx-community/whisper-large-v3-turbo --output-dir /Users/alvinatyr/vcu-video-transcripts /Users/alvinatyr/vcu-video-transcripts/<entryId>.mp4
   ```
   This produces `<entryId>.txt` in the output folder.

5. **Clean up the transcript:** Read the raw `.txt` file and rewrite it — group sentences into logical paragraphs by topic, add section headers where natural breaks exist, and remove filler/repetition. Write the cleaned version back to the same file.

6. **Show the user** the transcript file path and ask:
   > "Transcript is ready at ~/vcu-video-transcripts/<entryId>.txt — does it look correct?"

7. **After confirmation**, offer to rename:
   > "Want to rename the transcript (and video, if keeping it) to something more descriptive? For example: `gastric-ultrasound-lecture`"
   If the user provides a name, rename `<entryId>.txt` (and `<entryId>.mp4` if it still exists) to `<newname>.txt` / `<newname>.mp4`.

8. **Offer to delete the video** to save space:
   > "Want me to delete the video file to save space? The transcript is saved."
   Only delete if the user explicitly confirms.

## Notes

- The `ks=` token in the manifest URL is a time-limited Kaltura Session. If the download returns 403/401, ask the user to reload the video and paste fresh debug info.
- If `manifestUrl` is missing from the debug info, construct it from `partnerId` and `entryId` using the standard Kaltura playManifest URL format.
- Output folder: `/Users/alvinatyr/vcu-video-transcripts/`
- ffmpeg must be on PATH for both yt-dlp HLS download and mlx-whisper audio extraction — always prefix commands with `PATH="/opt/homebrew/bin:$PATH"`.
