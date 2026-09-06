# DC HOSA Study Tools & Prep Guides — website

Everything needed to put the whole DC HOSA competitive event library on the web at a
`dchosa.org` address. No build step, no framework, no server. It is static HTML.

```
Study Tools Website/
├── index.html          the landing page — 56 events across 9 categories
├── tools/              41 study tools + 15 prep guides
├── CNAME               the custom domain: study.dchosa.org
├── robots.txt          keeps the site out of search results
├── .nojekyll           tells GitHub to serve the files as they are
└── README.md           this file
```

**41 study tools** — events with a written test. Four-layer study guide, a simulator weighted to
the official 2026-2027 test plan, the full question bank, and for two-round events every rated
step and point value from the official rating sheets.

**15 prep guides** — events with no written test: portfolios, videos, posters, speeches, uploads.
Every required component with its limit, the format rules that disqualify an entry, what judges
score, a timeline built on the DC calendar, and a checklist.

`index.html` links to `tools/<slug>.html` with relative paths, so the folder works identically
opened from your Mac, from a USB stick, or served from the web. Double-click it right now and it
runs.

`CNAME`, `robots.txt` and `.nojekyll` are already filled in. If you want an address other than
`study.dchosa.org`, edit `CNAME` before uploading, or delete it and set the domain in the Pages
settings instead.

---

## Where this is published

| | |
|---|---|
| GitHub account | `hosadistrictofcolumbia-bit` |
| Repository | `hosadistrictofcolumbia-bit/dc-hosa-study-tools` |
| Pages source | branch `main`, folder `/ (root)` |
| GitHub URL | `https://hosadistrictofcolumbia-bit.github.io/dc-hosa-study-tools/` |
| Live address | `https://study.dchosa.org/` |
| DNS record | CNAME `study` → `hosadistrictofcolumbia-bit.github.io` |

The account name ends in `-bit`. Every place a username appears — the GitHub URL, the DNS
record — it has to be `hosadistrictofcolumbia-bit`, not `hosadistrictofcolumbia`. Those are two
different accounts as far as GitHub is concerned.

---

## Publishing to GitHub Pages

A free GitHub account is enough. About ten minutes, once. This is the record of how the site was
set up, and what to repeat if it ever has to be rebuilt.

**1. Make the repository.** github.com → **New repository**. Name it `dc-hosa-study-tools`.
Do not add a README — this folder has one.

Visibility: this repository is currently **public**. Pages publishes from a private repo just as
well on a free account, and private would keep the source HTML off github.com while leaving the
door open to move the site behind a password later. Either works; public means the tool files are
readable by anyone who finds the repo, which is the same material the site already serves openly.

**2. Upload.** On the empty repo page, click **uploading an existing file**. Open this folder in
Finder, select everything, and drag it in. The web uploader accepts folders, so `tools` goes in as
a folder.

Two files start with a dot and Finder hides them. Press **⌘⇧.** to show hidden files, then drag
`.nojekyll` in with the rest. If you miss it the site still works — it is insurance, not a
requirement.

Commit at the bottom of the page.

**3. Turn on Pages.** **Settings → Pages** → Source: **Deploy from a branch**, branch **main**,
folder **/ (root)**. Save, wait about a minute.

The site is then live at `https://hosadistrictofcolumbia-bit.github.io/dc-hosa-study-tools/`. Open
it and click into two or three tools before going further.

**4. Point the DC HOSA address at it.** `CNAME` already requests `study.dchosa.org`, so GitHub
picks it up on the first build and shows it under **Custom domain**, waiting on DNS.

In GoDaddy, DNS for dchosa.org, add one record:

| Type | Name | Value | TTL |
|---|---|---|---|
| CNAME | `study` | `hosadistrictofcolumbia-bit.github.io` | 1 hour |

Copy that value exactly. Usually resolves within the hour. Come back to **Settings → Pages**, and
once the DNS check shows a green checkmark, tick **Enforce HTTPS**.

---

## Troubleshooting

**"Your connection is not private" / certificate error at study.dchosa.org.** The DNS record is
pointing somewhere GitHub cannot match to this account, so GitHub never issues the TLS
certificate. Pages shows *DNS Check in Progress* and *Enforce HTTPS — Unavailable*.

Check what the record actually resolves to. In Terminal:

```
dig +short CNAME study.dchosa.org
```

It must return `hosadistrictofcolumbia-bit.github.io.` — if it returns anything else (a missing
`-bit`, a different account, an A record pointing at the GoDaddy site builder), fix the record in
GoDaddy and wait for it to propagate. Nothing in the repository needs to change.

**Pages settings show the site as live, but the address 404s.** GitHub is serving, DNS is not
resolving to it yet. Confirm the GitHub URL in the table above works first — that isolates whether
the problem is the site or the domain.

**A tool page 404s but the landing page works.** The filename in `tools/` does not match the link
in `index.html`. Filenames are case-sensitive on GitHub Pages and were not on your Mac.

**Changes uploaded but the site still shows the old version.** Pages takes up to a minute to
rebuild, and Safari and Chrome cache aggressively. Hard-reload with **⌘⇧R**.

---

## What the site is and is not

Every page carries `noindex, nofollow`, and `robots.txt` disallows crawlers. The site will not
appear in Google, so another state association will not find it by searching. A DC member with the
link is one tap in — no password, no account.

That is obscurity, not security. It does not stop a member forwarding the link. It was chosen
deliberately: a password is friction, and friction falls hardest on exactly the members this was
built for. If the tools ever do start spreading, a host with real password protection can be added
later without changing any of these files.

There is nothing confidential here. Original practice questions, published rating sheets, published
references. The confidential exam analysis and the secret Round Two scenarios live elsewhere and
are never published.

---

## Updating

Replace the file in `tools/`, keep the same filename, upload. The URL never changes.

Do not reorganise `tools/` into subfolders. One flat directory with slug filenames means
`study.dchosa.org/tools/phlebotomy.html` stays that address forever. Category grouping lives in the
landing page, where changing it costs nothing — and events do move categories between seasons.

The build system that generates all of this is in `../Build System/`, with `MAINTENANCE.md`
covering how to add an event or change the landing page. **Never upload that folder** — it is the
workshop, not the product.

---

*Built from the official 2026-2027 HOSA competitive event guidelines. September 2026.*
