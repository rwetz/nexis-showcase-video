# Nexis showcase loop

The 25-second silent loop in the "One window, every job." (`#tour`) section of
nexisdev.org. It is built from real Nexis 1.30.1 screenshots (`assets/shots/`),
captured by Nexis's `e2e/specs/screenshots.test.ts`. Intent and constraints live
in `BRIEF.md`.

- Composition: `index.html` (1600×1000, 30 fps, 25 s). The welcome screen opens
  and closes the timeline, so the last frame equals frame 0 and the loop has no seam.
- Checks: `npm run check`

## Re-render for the site

FFmpeg must be on PATH (`winget install --id Gyan.FFmpeg -e`).

```bash
npx --yes hyperframes@0.8.112 render --format mp4 --crf 14 -o renders/master.mp4
cd renders
ffmpeg -y -i master.mp4 -vf "scale=1280:800:flags=lanczos" -c:v libx264 -preset veryslow -tune animation -crf 27 -pix_fmt yuv420p -profile:v high -movflags +faststart -an nexis-showcase.mp4
ffmpeg -y -i master.mp4 -vf "scale=1280:800:flags=lanczos" -c:v libvpx-vp9 -b:v 0 -crf 40 -row-mt 1 -deadline good -cpu-used 1 -an nexis-showcase.webm
ffmpeg -y -i master.mp4 -frames:v 1 -vf "scale=1280:800:flags=lanczos" -q:v 3 nexis-showcase-poster.jpg
```

Keep each video under 3 MB, then copy the three files to
`nexis-website/public/video/`.
