# baemon

Unofficial 3D seat-view simulator for **2026-27 BABYMONSTER WORLD TOUR [CHOOM] in Jakarta**
at Indonesia Arena, GBK Senayan (Saturday 17 October 2026, 18:30 WIB).

Open `index.html` in a browser (it loads three.js r128 from cdnjs). The whole site is that one file.

## What it does

- **My seat**: first-person view from any seat at eye height, seated or standing. Drag to look
  around; scroll, pinch or use the Eyes / 2× / 4× buttons to zoom.
- **Arena**: orbit the whole arena. It opens from behind the stage, the same angle as the official
  seat map, with every section tinted in its ticket colour. Click a section to sit there.
- **Seat panel**: pick a seat from the map (drawn like the official one: stage at the bottom, side A
  on the right), the section list, or the row and seat sliders. It shows the distance to the main
  stage and to the runway / T-stage, eye height, the angle off the main screen, how much of the
  main and side screens a sightline raycast can see, how big a member looks at arm's length, and
  the TV size the main screen looks like. It flags restricted-view seats and anything in the way.
- **Fans**: every ticket is a fan, about 14,000 of them, at two levels of detail near you and as
  lightstick glows further out. Most wave the BABYMONSTER lightstick (black handle, white globe,
  red horns). Others film on their phones (you see the screen from behind), hold up slogan banners,
  wear glowing devil-horn headbands, BABYMONSTER tour tees or a hijab, carry a merch tote bag, and
  VIP ticket holders wear the laminate and lanyard. One pose shader moves every fan: a 120 bpm
  bounce, a sway that travels round the bowl, fists pumping, and arms down when the house lights
  are up. Security staff stand along the pit.
- **Lightsticks**: *Sync* imitates central control, where the show sets every stick's colour. It
  cycles through a red pulse, white twinkle, a red-and-white wave round the bowl, the seat map in
  lights (each fan glows in their ticket colour), a pink-to-purple fade from floor to roof, and A/B
  call and response. *Red* and *White* hold one colour. **My lightstick** puts your own stick in
  your hand at the bottom of the view, synced with everyone else's.
- **Show**: seven stand-in figures (generic, not likenesses) dance on the main stage, walk the
  runway single file to the T-stage and come back on a 60-second loop, each under a follow spot.
  The main LED screen plays CHOOM graphics (title card, the emblem on the beat, a dance
  equaliser, glitch static, strobe tiles); the side screens show a live camera feed from FOH that
  cuts between the members. Moving-head beams, red lasers, flame jets every 30 seconds and a
  confetti drop every 90 seconds. **House** brings the arena lights up and empties the stage.
- **Countdown**: D-day and a live countdown to showtime under the title.
- **Visitor counter**: "N visitors so far · M today" under the title (see below).

## Data

Ticket categories and prices follow the official seat map. Prices exclude 10% government tax,
the 6% platform fee and the convenience fee:

| Category | Type | Price |
| --- | --- | --- |
| VIP Soundcheck A–B | Festival standing | IDR 3,500,000 |
| MONSTIEZ VIP Box | Numbered seating | IDR 4,150,000 |
| CAT 1 | Numbered seating | IDR 3,150,000 |
| CAT 2 | Numbered seating | IDR 2,400,000 |
| CAT 3 A–B | Numbered seating, restricted view | IDR 1,400,000 |
| CAT 4 A–B | Numbered seating, restricted view | IDR 1,100,000 |

Where each category sits follows the official map:

- **Floor:** the main stage across the open end of the horseshoe, a runway into the floor ending
  in a T-stage, the two VIP Soundcheck pens (A and B) either side of them, and the sound desk (FOH)
  behind the pens.
- **Lower tier:** CAT 1 round both sides and the far end, with the wheelchair positions on the
  cross-aisle at the far corners; CAT 3 A/B at the ends nearest the stage.
- **MONSTIEZ VIP Box:** a two-row balcony ring in front of glass suites between the tiers.
- **Upper tier:** CAT 2 round both sides and the far end; CAT 4 A/B at the ends nearest the stage.
- **Behind and beside the stage:** draped off, not on sale.

The VIP Soundcheck and MONSTIEZ VIP Box package benefits are listed in the panel. Indonesia Arena
seats about 16,000 (13,000 fixed and 3,000 telescopic seats). The bowl shape, row counts, section
numbers, stage and screen sizes are **estimates**, so confirm your seat on your ticket and the
official map. Showtime (18:30 WIB) comes from ticket listings; open-gate times are announced by
the promoter. The member count is the `MEMBERS` constant near the top of the script.

Not affiliated with YG Entertainment, TEM Presents, Live Nation or Indonesia Arena.

## Visitor counter

The published site shows "N visitors so far · M today" under the title. It counts each browser
once in total and once per Jakarta day: the first visit adds one and leaves a flag in the browser,
and later visits only read the numbers. It uses [Abacus](https://github.com/JasonLovesDoggo/abacus),
a free counter service that needs no account. It skips `localhost` and files opened from disk, so
local testing never changes the count; every published copy (GitHub Pages, a Hostinger domain)
adds to the same total. If the service is slow or down, the line simply stays hidden.

- **See the total any time:** https://abacus.jasoncameron.dev/get/jn1xia.github.io/baemon-visitors
  (today's count is under the key `baemon-day-YYYYMMDD`, for example `baemon-day-20261017`).
- **Protect the count (optional, but only possible before the counter goes live):** anyone who
  knows the address could add fake visits, so it helps to own the counter. Open
  https://abacus.jasoncameron.dev/create/jn1xia.github.io/baemon-visitors in a browser and save
  the `admin_key` it shows somewhere private (never in this repo). With that key you can later
  correct the number with Abacus's `/set` call. Once the live site has counted a single visit,
  `/create` is refused for good.
- **Limits:** this counts browsers, not people. The same person counts again on another device,
  after clearing browser data, and in each app's built-in browser (Instagram, TikTok and WhatsApp
  keep separate storage). Browsers that block storage only see the totals and are not counted.
  Abacus is a free hobby service with no uptime promise, so the line may sometimes be missing.

### Full stats dashboard (optional)

For visitors per day, countries, devices and where people came from, sign up free at
[GoatCounter](https://www.goatcounter.com). It sets no cookies. Pick a site code, then put it in
`GOATCOUNTER_CODE` near the end of `index.html`. Ad blockers block GoatCounter, so its dashboard
misses those visitors; the public counter above is not on those lists.

## Deploy

The site is the single `index.html` file (plus `.nojekyll`), so any static host works.

### GitHub Pages (free)

1. Go to **Settings → Pages → Build and deployment**.
2. Set **Source** to "Deploy from a branch", pick the branch that holds `index.html` (for example
   `ccr-d296b8da-msdmvb`, or `main` once it is merged) and the folder `/ (root)`, then **Save**.
3. The site goes live at https://jn1xia.github.io/baemon/ in about a minute. Every later push to
   that branch republishes it.

### Hostinger

Hostinger no longer has a free plan (its free host, 000webhost, closed in 2024), so GitHub Pages
is the free option. On a paid Hostinger plan: open **hPanel → Websites → File manager**, go to
`public_html` (or the folder of the domain you want), upload `index.html`, and the site is live on
that domain. The visitor counter there adds to the same total as GitHub Pages.
