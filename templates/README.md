# Brochure templates

Alternative designs for a Pharmakaksha batch page. Each is a complete, single-file page with the same content and behaviour as the live `index.html`: a countdown, the important dates with live status, posts by RRB, eligibility, the score calculator, the syllabus, the week-by-week plan and the pricing. None of these files is deployed. The workflow only publishes the root `index.html`.

| File | Look |
| --- | --- |
| `departure-board.html` | Station departure board: black and amber, split-flap tiles, live clock, DEPARTED / BOARDING statuses. Dark only. |
| `ticket.html` | Railway ticket, the same style as the AP brochure (apur26.pharmakaksha.com). Light and dark. |

The live page uses the editorial-poster design (cream, red and black).

## Previewing one

Open the file in a browser. The `../logo.jpg` paths point at the logo in the repository root.

## Starting a new project from a template

1. Copy the template into the new project's folder as `index.html`, and copy `logo.jpg` next to it.
2. In the copy, change `../logo.jpg` to `logo.jpg` (it appears twice: the favicon and the header image).
3. Edit the script near the bottom:
   - `CONFIG` holds the fee, promo code, offers, registration close, batch start, exam date, links, share text and analytics token.
   - `MILESTONES` holds the dates the countdown runs to.
   - `PLAN` holds the week-by-week study plan.
4. Edit the exam facts in the HTML: the `<head>` tags for link previews (title, description, `og:url`, `og:image`, `canonical`), the hero text, the important-dates list, posts by board, eligibility, fees, the paper pattern, the qualifying marks in the calculator buttons and the syllabus groups.
5. For a different marking scheme, change the score formula in `calc()` (for example `3 * c - w` for +3 / −1) and the guessing numbers.
6. Copy `.github/workflows/deploy.yml`, `CNAME` and `.nojekyll` from this repository, and put the new subdomain in `CNAME` and the workflow name.

Each page needs no build step. It loads its fonts from Google Fonts and everything else is inline.
