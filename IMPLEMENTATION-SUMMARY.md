# NEET Ranker — Multi-Page Rearchitecture: Implementation Summary

## What changed

The single `index.html` (login-gate + app in one file) is now split in two:

| File | Role | Indexed? |
|---|---|---|
| `index.html` | Public landing page: hero, features, methodology, calculator, mistake-matrix demo, strategy blog, FAQ | Yes |
| `dashboard.html` | The actual app — 100% of your original Firebase auth, Firestore CRUD, Chart.js charts, mistake analysis, About modal, and Shepherd tour, unmodified | No (`noindex`, intentionally — see below) |
| `about-us.html`, `contact.html`, `privacy-policy.html`, `terms-of-service.html` | The four AdSense-mandatory footer pages, with real content, not stubs | Yes |
| `robots.txt`, `sitemap.xml` | Point crawlers at the five public pages, exclude the app | — |

**Nothing in your app logic was removed or rewritten.** I diffed `dashboard.html` against your original file line-by-line: the only changes are the nav bar (added a "Home" link), the footer (added legal links), and two edits described below. Every Firebase call, Firestore listener, Chart.js instance, mistake-tagging function, and the Shepherd tour fire exactly as before — I ran your inline scripts through a Node syntax check and cross-referenced all 55 `getElementById` calls against the HTML to confirm nothing broke.

Two small things I fixed while I was in there, both pre-existing in your original file, not something introduced during this rebuild:
- Two links in the About modal ("Official Website" / "Official Bot") were still the literal placeholder text `YOUR_OFFICIAL_WEBSITE_URL` / `YOUR_OFFICIAL_BOT_URL`. I filled them in using the URLs your own `readme.md` documents (`sakssenowner.netlify.app` and `t.me/NEELAXMI_OFFICIAL`) — worth a quick check that those are still current.
- `style.css` from your zip is a single unclosed CSS rule and isn't linked from any page, so I left it out of the deliverable rather than ship a broken, unused file.

## Why `dashboard.html` is set to `noindex`

Google doesn't just want *a* crawlable page somewhere on the site — it evaluates whatever page it lands on. Since `dashboard.html` is still just an auth gate with no static content, indexing it would put a thin/duplicate page in Google's index next to your rich landing page, which works against you. Keeping it `noindex` while `index.html` carries all the SEO weight is the standard pattern for gated apps.

## Before you deploy: placeholders to replace

I used `https://neetranker.example.com` throughout (canonical tags, Open Graph, JSON-LD, sitemap) since I don't know your real domain — `.example.com` is the reserved placeholder domain, chosen so nothing accidentally points at a live site. Find-and-replace it across all files with your real domain before launch. Also replace:
- `support@neetranker.example.com` in `contact.html` (clearly flagged there too) with an inbox you actually monitor.
- The commented-out `ca-pub-XXXXXXXXXXXXXXXX` / `data-ad-slot="XXXXXXXXXX"` in the three `adsense-slot` divs in `index.html`, once AdSense approves you and issues real IDs.

## AdSense submission checklist

1. **Deploy first, apply second.** AdSense reviews the live URL, so get this hosted (Netlify/Vercel/Firebase Hosting all work) before applying.
2. Fill in the domain/email placeholders above.
3. Have a real person skim `privacy-policy.html` and `terms-of-service.html` — I wrote them to accurately describe what the app actually does (Firebase auth, Firestore storage, no hidden tracking), but they're a starting point, not legal advice. Given most users are likely minors preparing for an entrance exam, it's worth a lawyer's pass, particularly against India's DPDP Act if you're targeting Indian users.
4. Verify Firestore security rules actually restrict reads/writes to the owning user — with a public marketing site now driving more traffic to `dashboard.html`, it's a good moment to double check rather than assume.
5. Submit the root domain, not `dashboard.html`, when you apply.

## Search Console checklist

1. Add and verify the property (domain or URL-prefix) for your real domain.
2. Submit `sitemap.xml` under Sitemaps.
3. Use URL Inspection on `index.html` to request indexing once live.
4. The `WebSite` schema includes a `SearchAction` pointing at `index.html?q={search_term_string}` — this is wired to a real feature (the FAQ/blog search box actually filters on that query param), not decorative schema, but Google still decides at its own discretion whether to surface a sitelinks search box.
5. After a couple of weeks, check the FAQ rich-result status under Enhancements — the visible FAQ accordion text matches the `FAQPage` JSON-LD exactly, which is what Google's guidelines require for eligibility.

## Content notes

- The rank/percentile bands in the Calculator and the general score guidance are explicitly labeled **indicative, not an official prediction** — NEET cutoffs shift with difficulty and normalization every year, so I avoided asserting false precision on something this high-stakes for students.
- No fabricated testimonials, review counts, or usage stats anywhere — I skipped `aggregateRating` schema entirely since you have no real reviews yet; fake rating markup is a common cause of AdSense/Search Console manual actions, so it's better added later once genuine.
- The three blog articles are original, full-length (not thin teasers) and expand in place via native `<details>`, so the full text is in the HTML for crawlers while the initial view stays compact for readers.
