# CLAUDE.md

Guidance for Claude (and humans) working on the Mud Tavern Volunteer Fire and Rescue (MTVFR) website.

## What this is

Public website for Mud Tavern Volunteer Fire and Rescue, a 100% volunteer department near Decatur, Alabama.

- Live site: https://www.mudtavernfire.org (custom domain via `CNAME`, DNS at Cloudflare)
- GitHub Pages fallback: https://mud-tavern-fire-rescue.github.io
- Owners: Mike Russell and zmweske. Changes that affect the other owner's work should be coordinated.

## Stack

- Jekyll static site, Bootstrap 4, custom CSS in `assets/css/MTVFR_final.css`
- No theme. Single layout: `_layouts/default.html`
- Deployed by GitHub Actions: `.github/workflows/monthly-rebuild.yml`

## Where things live

| What | Where |
|---|---|
| Most editable text | `_data/*.yml` |
| Menu (header nav) | `_data/navigation.yml` |
| About blurb, donate info, footer, calendar/form/newsletter embed URLs | `_data/misc_ref.yml` |
| Homepage photo and caption | `_data/homepage_highlight.yml` |
| Monthly safety tips | `_data/monthly_tips.yml` (keys are full month names) |
| Preparedness page text | `_data/prep.yml` |
| Volunteer page text | `_data/volunteer.yml` |
| Members and auxiliary (currently hidden in `pages/about.html`) | `_data/members.yml`, `_data/aux_members.yml` |
| Page templates | `pages/` (each sets its URL with `permalink:`) |
| Shared pieces (header, footer, tip box, etc.) | `_includes/` |
| Images and PDFs | `assets/images/<section>/` |

Prefer editing YAML in `_data/` over editing HTML. Text values may contain simple HTML (`<a>`, `<br>`). Quote any YAML value that contains a colon.

## Do not touch

- `lindsay-mtvfr/`: an older hand-built version of the site kept for reference. Excluded from the build.
- `CNAME`: changing it breaks the custom domain.
- `.github/workflows/` and `_config.yml` deploy settings: only change when the task is specifically about deployment.

## Local preview

```bash
docker compose up
# then open http://localhost:4000
```

Note: the Gemfile pins Jekyll 4.3, but the deploy workflow uses `actions/jekyll-build-pages`, which builds with the GitHub Pages gem (Jekyll 3.x). Watch for differences between local preview and the live site.

Always preview and check every page you changed before committing.

## Deploying

- The workflow runs on every push to `main`, on a schedule (1st of each month), and on manual dispatch from the Actions tab. Merging a pull request into `main` publishes it.
- The monthly run is what rotates the homepage safety tip, because the tip is chosen at build time from `site.time`.
- GitHub disables scheduled workflows on public repos after 60 days with no commits. If the tip on the live site is stale, re-enable the workflow in the Actions tab and run it manually.

## Workflow

1. Create a branch for each change.
2. Make the change and preview locally.
3. Commit with a short, plain description of what changed.
4. Open a pull request for the other owner to review. Do not push directly to `main` unless asked.

## Content rules

- No incident, call, or patient details on the site, even anonymized. No photos that show patients, victims, or identifiable scenes.
- Member names, photos, and bios only with that member's consent.
- Anything that speaks for the department (policy, positions, fundraising claims) needs approval from department leadership before publishing.
- Safety and medical guidance must match current mainstream sources (Ready.gov, NFPA, American Red Cross, CDC). Do not invent statistics. Link to the source when citing one.
- Keep the department's email obfuscated as it is now unless told otherwise.
- Resize photos to roughly 1600 px on the long side or smaller before adding them. Use descriptive alt text.
- American English, plain and friendly tone, written for neighbors rather than firefighters.

## Known cleanup items

- `_config.yml` still has Jekyll default title, email, and description.
- Footer copyright year is hard-coded in `_data/misc_ref.yml`.
- Homepage caption description is placeholder Lorem ipsum.
- Volunteer text links to `/contact`, which is hidden from the menu.
- See the README to-do list for the longer roadmap.
