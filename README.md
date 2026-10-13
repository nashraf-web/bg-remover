# BG Remover — GitHub Pages Deployment

Free, private, in-browser AI background remover. 100% client-side — no uploads, no server, no API costs.

**Live URL (after deployment):** https://bg.cloudemythos.org

## What's in this folder

| File | Size | Purpose |
|------|------|---------|
| `index.html` | 2.1 MB | The complete tool (UI + logic). Model/ORT extracted to separate files. |
| `CNAME` | — | Custom domain for GitHub Pages (`bg.cloudemythos.org`) |
| `assets/models/birefnet-lite-fp16.onnx` | 94 MB | BiRefNet-lite AI model (MIT license). Downloads with progress bar on first use, then cached by the browser. |
| `assets/ort/ort.all.min.js` | 804 KB | ONNX Runtime JS loader (local fallback if both CDNs fail) |
| `assets/ort/ort-wasm-simd-threaded.wasm` | 14 MB | WASM inference engine |
| `assets/ort/ort-wasm-simd-threaded.mjs` | 24 KB | WASM JS glue |
| `assets/ort/ort-wasm-simd-threaded.jsep.wasm` | 27 MB | WebGPU-enhanced WASM (progressive enhancement) |
| `assets/ort/ort-wasm-simd-threaded.jsep.mjs` | 48 KB | JSEP JS glue |

**Total: ~137 MB.** All files are under GitHub's 100 MB per-file push limit.

## How it works

1. User opens the page → ORT runtime loads (jsDelivr → unpkg → local fallback)
2. User uploads an image → model downloads once via `fetch()` with a real progress bar (~94 MB)
3. Inference runs in-browser via WASM → transparent PNG result
4. Model is cached by the browser (`cache: 'force-cache'`) — subsequent visits are instant

## Deployment steps

### 1. Create the GitHub repository

```bash
cd ~/workspace/bg-remover-deploy/site
git init
git add .
git commit -m "Deploy BG remover v1.0 — self-hosted BiRefNet"
git branch -M main
git remote add origin https://github.com/<username>/bg-remover.git
git push -u origin main
```

> **Note:** The 94 MB model file is under GitHub's 100 MB limit, so no Git LFS needed.
> First push will take a few minutes due to total size (~137 MB).

### 2. Enable GitHub Pages

1. Go to the repo → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main**, folder: **/ (root)**
4. Save. GitHub will serve the site at `https://<username>.github.io/bg-remover/`
5. The `CNAME` file tells GitHub to also serve it at `bg.cloudemythos.org`

### 3. Set up the subdomain DNS

At your DNS provider (IONOS):

| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME | `bg` | `<username>.github.io.` | 3600 |

- Wait for DNS propagation (usually 10 min – 2 hours)
- GitHub Pages will automatically provision HTTPS (Let's Encrypt) — check **Settings → Pages** for the certificate status
- Do NOT use A records — GitHub Pages requires CNAME for subdomains

### 4. Verify

Open https://bg.cloudemythos.org and run through [DEPLOY_CHECKLIST.md](./DEPLOY_CHECKLIST.md).

## Updating the site later

1. Edit files locally in this `site/` folder
2. `git add . && git commit -m "Update description" && git push`
3. GitHub Pages redeploys automatically (~1 min)

**Do NOT edit the live site via GitHub's web editor for binary files** — always push from local.

## Rollback

```bash
git log --oneline          # find the previous good commit
git revert <commit-hash>   # or: git reset --hard <commit-hash> && git push --force
```

## License notes

- **BiRefNet-lite model:** MIT license — free for commercial use
- **ONNX Runtime Web:** MIT license
- **JSZip:** MIT license
- Site code: © 2026 CloudEmythos
