# Nexis showcase loop

The 26-second silent loop in the "One window, every job." (`#tour`) section of
nexisdev.org. It is cut from real app clips (`assets/clips/`) that Nexis's
`e2e/specs/clips.test.ts` screencasts straight from the app's webview: welcome,
Spotlight, terminal, AI agent, Documents and theme switching. Intent and
constraints live in `BRIEF.md`. `assets/shots/` holds the earlier still-image cut's
screenshots.

- Composition: `index.html` (1600×1000, 30 fps, 26.3 s). It closes on a still of the
  welcome clip's first frame, so the last frame equals frame 0 and the loop has no seam.
- New clips: in Nexis, `NEXIS_CLIPS=1 NEXIS_E2E_WORKSPACE=. pnpm test:e2e --spec e2e/specs/clips.test.ts`
  against the screenshot build, then copy `e2e/clips/*.mp4` into `assets/clips/`.
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

## License

Apache-2.0 (see `LICENSE`), like the rest of Nexis. The Geist and Geist Mono
fonts in `assets/fonts/` are © The Geist Project Authors under the SIL Open Font
License 1.1 (`assets/fonts/OFL.txt`).
