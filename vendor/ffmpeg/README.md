# Vendored ffmpeg.wasm

These files power the **Highlight video** feature — a real build of FFmpeg
compiled to WebAssembly, running entirely in the visitor's browser. Nothing
here talks to a server; it's vendored (rather than loaded from a CDN) so the
site has no third-party runtime dependency and works the same way GitHub
Pages serves everything else.

## What's here

| Path | From | Version | License |
|---|---|---|---|
| `ffmpeg/` | [`@ffmpeg/ffmpeg`](https://www.npmjs.com/package/@ffmpeg/ffmpeg) (`dist/esm`) | 0.12.15 | MIT |
| `util/` | [`@ffmpeg/util`](https://www.npmjs.com/package/@ffmpeg/util) (`dist/esm`) | 0.12.2 | MIT |
| `core/` | [`@ffmpeg/core`](https://www.npmjs.com/package/@ffmpeg/core) (`dist/esm`) | 0.12.10 | GPL-2.0-or-later |

Source for all three: [ffmpegwasm/ffmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm)
on GitHub. `core/` is an actual compiled build of [FFmpeg](https://ffmpeg.org/)
itself (with libx264 enabled for H.264 encoding, hence the GPL license,
distinct from the MIT-licensed JS wrapper in `ffmpeg/` and `util/`) — its
`LICENSE` file here is the standard GPL-2.0 text; the corresponding FFmpeg
source is publicly available from the FFmpeg project and the ffmpeg.wasm
build scripts linked above.

Deliberately using the **single-threaded** core build (not `core-mt`): the
multi-threaded build needs `Cross-Origin-Opener-Policy`/
`Cross-Origin-Embedder-Policy` response headers, which GitHub Pages has no
way to set. Single-threaded is slower but works unmodified on static hosting.

## Updating

```
npm init -y  # in a scratch directory
npm install @ffmpeg/ffmpeg@<version> @ffmpeg/core@<version> @ffmpeg/util@<version>
```

Then copy `dist/esm/*` from each package into the matching folder here
(`ffmpeg/`, `util/`, `core/` — core only needs `ffmpeg-core.js` and
`ffmpeg-core.wasm`). No build step or bundler involved — the ESM files
import each other with plain relative paths, so they work as static files
as-is.
