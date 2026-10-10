# RRB Pharmacist (CEN 05/2026) brochure

Interactive one-page brochure for the Pharmakaksha batch for the Railway Recruitment Boards' Pharmacist (Entry Grade) computer-based test under CEN 05/2026 (Paramedical Categories). Live at **https://rrb26.pharmakaksha.com/**.

It is styled as an editorial poster: cream, deep red and black, a giant "118" hero, huge condensed numerals and italic serif asides. Dates and plan weeks show their status (open now, upcoming, done) as the dates pass. It prints cleanly to PDF (no sticky bars, every syllabus group open). It has a countdown to the next important date, an index bar, the official dates, posts by RRB, eligibility and age limits, the application fee, the selection steps, the paper pattern, a +1 / −⅓ score calculator, a guessing guide, what the batch includes, the official syllabus, a week-by-week study plan, fees with offers, contact details and social links. It is a single static `index.html`, so no build step is needed.

## Editing the details

Open `index.html` and find `const CONFIG` near the bottom. It holds the fee and offers, the registration close date, batch start, the CBT date, contact links and the share message.

- **CBT date:** RRB has not announced it yet. When it does, set `exam`, for example `"2027-01-20T09:00:00+05:30"`. The countdown, the "CBT date" field and the exam row in the plan then use it.
- **Countdown dates:** `MILESTONES`, just below `CONFIG`. The hero and sticky bar count down to the soonest upcoming one.
- **Study plan:** the `PLAN` list further down, one entry per week.
- **Links:** the register, chat, channel and email links are also written into the HTML, so they work even if the script fails. If you change one in `CONFIG`, change it in the HTML too (search for the old URL).
- **Analytics:** the Cloudflare Web Analytics snippet sits just before `</body>` in `index.html`. To turn analytics off, delete that one line.

After 31 Oct (`regClose`) the page switches by itself: the status badge says closed, the free-trial card hides and the Register buttons become "Ask about the next batch" and open the WhatsApp chat.

## Share images

`og-image.jpg` (1200×630) is the preview card WhatsApp and Telegram show when the link is shared. `marketing/whatsapp-status-1080x1920.jpg` is for WhatsApp Status. Both are rendered from the HTML in `marketing/src/`. If you change the fee, dates or offer, edit those files and run:

```bash
sh marketing/src/render.sh
```

Then bump `?v=1` on the `og:image` URL in `index.html` so apps fetch the new card. Also update the `og:image:alt` and `og:description` text, which repeat the fee and closing date.

## Publish on GitHub Pages

The repository is `ajreddys/rrb-2026-pharmacist`. Pages is set to **Source = GitHub Actions**, and the workflow in `.github/workflows/deploy.yml` publishes on every push to `main`:

```bash
git add -A && git commit -m "Update brochure" && git push
```

Progress shows under the repository's **Actions** tab.

### Custom domain: rrb26.pharmakaksha.com

The `CNAME` file already contains `rrb26.pharmakaksha.com`.
The DNS record (Type `CNAME`, Host `rrb26`, Value `ajreddys.github.io`) is in place, and the custom domain is set in **Settings → Pages**. Once GitHub has issued the certificate, tick **Enforce HTTPS** there if it isn't on already.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The brochure page (styles and script included) |
| `logo.jpg` | Pharmakaksha logo, used in the header and as the favicon |
| `og-image.jpg` | Link preview card |
| `CNAME` | The custom domain `rrb26.pharmakaksha.com` |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |
| `.github/workflows/deploy.yml` | Deploys the site files to GitHub Pages |
| `templates/` | Alternative designs (modern ed-tech app, departure board, railway ticket), not deployed. See `templates/README.md` for reusing one in a new project |
| `marketing/` | WhatsApp Status image, plus the HTML sources and render script for both images (not deployed) |

## Source

Exam facts come from the detailed CEN 05/2026 (Paramedical Categories), notice dated 12.09.2026. That PDF sits in this folder but is not committed (see `.gitignore`).

- **Posts:** 118 Pharmacist posts (UR 54, SC 19, ST 21, OBC 15, EWS 9) across 20 RRBs. Chennai 15, Mumbai 12, Kolkata 10, Malda 9, Ranchi 8, Prayagraj 7, Ajmer, Bengaluru, Gorakhpur, Guwahati and Patna 6 each, Ahmedabad, Chandigarh and Secunderabad 5 each, Muzaffarpur 4, Bhopal, Bilaspur and Siliguri 2 each, Bhubaneswar and Jammu-Srinagar 1 each.
- **Paper:** 100 questions in 90 minutes, ⅓ mark off per wrong answer. Qualifying marks: 40% UR/EWS, 30% OBC and SC, 25% ST.
- **Shortlist:** document verification is called 1:1 per vacancy, RRB-wise.

Recheck these if RRB publishes a revised vacancy table or the CBT schedule.
