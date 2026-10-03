# Clinic display

Looping video/photo player for old iPads (tested target: iPad 2, iOS 9.3.5).

## Folder layout (put this on the Mac's shared folder)

```
clinic-display/
  player.html
  playlist.txt      (optional — order of play)
  videos/
    01-sitting-after-tkr.mp4
    02-running-after-tkr.mp4
    ...
```

## Use

1. On the iPad, open Safari and go to `http://<mac-address>/clinic-display/player.html`.
2. Tap **Tap to start** once. It then loops all day.
3. Turn on Guided Access (triple-click Home) so it can't be closed.

To update: drop new files into `videos/` (and list them in `playlist.txt`, or delete
`playlist.txt` to play everything A–Z). The iPad picks up changes at the end of each loop.

## Converting videos for iPad 2

```
ffmpeg -i input.mp4 -vf "scale=576:1024:force_original_aspect_ratio=decrease,pad=576:1024:(ow-iw)/2:(oh-ih)/2,fps=30" \
  -c:v libx264 -profile:v main -level 3.1 -pix_fmt yuv420p -crf 23 -preset slow \
  -c:a aac -b:a 128k -ar 44100 -movflags +faststart output.mp4
```
