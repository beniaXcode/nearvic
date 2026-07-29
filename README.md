# profile.nearvic.com

Personal landing page for Yahia Mohamed Benabbou — Senior DevOps & DevSecOps Engineer,
Cloud Solutions Architect, SRE.

Single static HTML file. No build step, no dependencies.

## Preview locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Opening `index.html` directly with `file://` works too, but a local server matches
production more closely.

## Deploy

**Cloudflare Pages / Netlify / Vercel** — connect the repo, leave the build command empty,
set the output directory to the repo root.

**Netlify, no repo:** drag the folder onto <https://app.netlify.com/drop>.

**GitHub Pages:**

```bash
git init && git add -A && git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:<user>/nearvic-profile.git
git push -u origin main
# Settings → Pages → deploy from main, root
```

Then point `profile.nearvic.com` at the host with a CNAME record.

## Working on it with Claude Code

```bash
cd nearvic-profile
claude
```

`CLAUDE.md` loads automatically at session start and carries the design system, positioning
rules and open items. Read it before making changes — several decisions in there were made
deliberately and shouldn't be reversed by accident.

Run `/memory` to see which instruction files are active.

## Structure

```
index.html    the entire site — inline CSS, JS and SVG sprite
CLAUDE.md     project context for Claude Code
docs/         supporting material (resume, roadmap, positioning docs)
```
