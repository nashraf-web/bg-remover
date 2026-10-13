# Pre-Launch Verification Checklist

Run through every item before announcing the tool publicly. Check off each one.

## 1. Infrastructure

- [ ] `https://bg.cloudemythos.org` loads (not the `github.io` URL)
- [ ] HTTPS certificate is active (padlock in address bar, no warnings)
- [ ] Page loads in under 5 seconds on broadband
- [ ] No console errors on page load (F12 → Console)
- [ ] Works in Chrome, Edge, Firefox, Safari (desktop)
- [ ] Works on mobile Chrome (Android) and Safari (iOS)
- [ ] `CNAME` file is present in repo root (GitHub Settings → Pages shows custom domain)

## 2. AI model loading

- [ ] Upload a test photo → model download progress bar appears
- [ ] Progress bar shows real percentage (not stuck at 0%)
- [ ] Model finishes downloading (~94 MB, time depends on connection)
- [ ] No "AI runtime could not load" error
- [ ] No "AI could not finish this image" error on first try
- [ ] Second upload is instant (model cached, no re-download)

## 3. Background removal quality

- [ ] Portrait photo → clean cutout, hair edges preserved
- [ ] Product photo (e.g. shoe, bag) → sharp edges, no halo
- [ ] Complex background → subject correctly identified
- [ ] Before/after slider works (drag to compare)
- [ ] Result looks correct at 100% zoom (no artifacts, no distortion)

## 4. Export

- [ ] PNG download works (transparent background verified — open in viewer)
- [ ] JPG download works (white background)
- [ ] WebP download works
- [ ] Batch mode: upload 3+ images → all process
- [ ] Batch ZIP download works and contains all images

## 5. Edge cases

- [ ] Very large image (e.g. 4000×6000) → handled without crash
- [ ] Tiny image (e.g. 100×100) → handled gracefully
- [ ] Non-image file → clear error message (not a crash)
- [ ] Corrupt image → clear error message
- [ ] Offline after model cached → still works (service worker / cache)
- [ ] Private/incognito window → works (fresh model download)

## 6. SEO / GEO

- [ ] `<title>` is descriptive: "Free Background Remover — ..."
- [ ] Meta description present (110–160 chars)
- [ ] H1 is the main keyword heading
- [ ] FAQ section present with real questions
- [ ] FAQPage JSON-LD structured data present (test at validator.schema.org)
- [ ] Open Graph tags present (preview on social shares)
- [ ] Canonical URL set to `https://bg.cloudemythos.org/`

## 7. Monetization

- [ ] Ko-fi button links to `https://ko-fi.com/cloudemythos` (not /huebugs)
- [ ] Ko-fi page shows CloudEmythos branding
- [ ] Pro section says "Coming Soon" (honest — no fake features)
- [ ] No AdSense yet (only after tool is verified working — per plan)

## 8. Legal / compliance

- [ ] No competitor names anywhere in the UI (especially: never "remove.bg")
- [ ] No copied marketing copy from competitors
- [ ] Privacy claim is true: images never leave the device (verify in Network tab — no image uploads)
- [ ] "Free" claims are honest (no hidden limits not disclosed)
- [ ] Footer has © 2026 CloudEmythos

## 9. Performance

- [ ] First model download is the only slow step (expected, ~94 MB once)
- [ ] Inference time per image is reasonable (< 30 sec on mid-range phone)
- [ ] Page doesn't freeze during processing (progress indicators show)
- [ ] Memory doesn't balloon on batch of 10 images

## 10. Analytics (optional, post-launch)

- [ ] Decide: add privacy-friendly analytics (Plausible/Umami) or skip
- [ ] If added: verify no PII collected, consistent with privacy claims

---

**Sign-off:** All boxes checked → ready for public launch (blog articles, Product Hunt, Reddit, Pinterest).
**If any box fails:** fix it, re-deploy, re-check. Do not launch with known failures.
