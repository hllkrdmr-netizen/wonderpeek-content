# wonderpeek-content

Remote levels for Wonderpeek. The app reads `manifest.json` fresh on every launch and downloads
level files from jsDelivr pinned to a commit (`cdn.jsdelivr.net/gh/hllkrdmr-netizen/wonderpeek-content@<commit>/…`),
verifying each file's sha256. Only data and images: `.json .webp .png .jpg`. No code is ever run.

```
manifest.json            generated: id, version, minAppVersion, files (path, size, sha256)
levels/level_NNN.json    one file per level (same format as the app's assets/game/level_001.json)
sahneler/<scene>/        scene.webp (4096), scene_2048.webp, bg_blur.webp, depth.png, *_mask.png
nesneler/*.png           object sprites
peek/*.png               Peek sprites
```

## Adding or updating a level

1. Put the files in place: `levels/level_NNN.json` plus the scene folder and any new sprites.
2. In the app repo: `node scripts/publish-content.js` (validates, hashes, updates `manifest.json`).
3. Here: `git add -A && git commit -m "Level NNN" && git push`.

Players get it on their next app launch. A level whose files did not change keeps its version.
