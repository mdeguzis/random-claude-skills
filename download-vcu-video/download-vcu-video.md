# Download VCU Kaltura Video

Download a video from VCU Canvas using Kaltura debug info.

## Steps

1. **Ask the user** to paste the debug info from the video:
   > "Please paste the debug info JSON from the VCU video player (right-click the video > Debug Info > copy all the text)."

2. **Parse** the pasted JSON to extract:
   - `manifestUrl` — the HLS `.m3u8` stream URL
   - `entryId` — used as the output filename

3. **Run the download** using yt-dlp:
   ```
   yt-dlp "<manifestUrl>" -o "/Users/alvinatyr/vcu-video-transcripts/<entryId>.mp4"
   ```
   Use the full path `/opt/homebrew/bin/yt-dlp` if `yt-dlp` is not found in PATH.

4. **Confirm** the file was saved to `/Users/alvinatyr/vcu-video-transcripts/`.

## Notes

- The `ks=` token in the manifest URL is a time-limited Kaltura Session. If the download returns 403/401, ask the user to reload the video and paste fresh debug info.
- If `manifestUrl` is missing from the debug info, construct it from `partnerId` and `entryId` using the standard Kaltura playManifest URL format.
- Output folder: `/Users/alvinatyr/vcu-video-transcripts/`
