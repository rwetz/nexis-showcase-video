---
workflow: general-video
flow: automation
storyboard: no
message: "Nexis is one window for the whole job: find, ask, build, ship."
destination: website-embed
aspect: 1600x1000
language: en
length: 24s
angle: product-showcase
---

## Intent

A silent, seamlessly looping showcase for the nexisdev.org page, in the slot the
removed interactive terminal demo used to fill (between the screenshot gallery
and the CTA). It should feel like the real app in motion: quiet, exact, premium.
The user asked for this from plan.md and chose "HyperFrames + screenshots" over
recording live clips or installing Remotion.

## Assets

- C:\Users\ryan\Dev\nexis-website\assets\*.webp and
  C:\Users\ryan\Dev\nexis-wiki\src\assets\*.webp — real Nexis 1.30.1 dark-theme
  screenshots (1600x1000), captured by Nexis's e2e/specs/screenshots.test.ts.
  Scenes: Spotlight, AI panel + orb, Atlas, SVG Studio, Documents, terminal, editor.

## Customizations

- Seamless loop: the last frame must match the first.
- Deliverables: H.264 MP4 + WebM, each ≤ 3 MB, plus a poster JPG from frame 0.

## Notes

- No audio (muted autoplay).
- Do not show the Models settings shot (it reveals part of a real API key) or
  anything implying the removed terminal exit-status gutter / Explain chip.
- Site embed: <video autoplay muted loop playsinline preload="none" poster>,
  mounted near the viewport, poster-only under reduced motion.
