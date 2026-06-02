# 🏫 Air Force School Avadi — Website Audit & Revamp Plan
### Executive Report | Prepared June 2026

---

## 1. Executive Summary

Air Force School Avadi ([afschoolavadi.com](https://afschoolavadi.com/)) is a prestigious CBSE-affiliated school established in 1975, serving 4,800+ students with 160+ staff. The school has won **"Best AF School in IAF"** multiple times.

**The website, however, does not reflect this excellence.** Built on ~2008-era technology (XHTML 1.0, MooTools 1.11, table-based layouts), it is not mobile-responsive, has significant accessibility violations, and contains security concerns including a web crawler script that has scraped hundreds of Google pages into the repository.

This report provides a detailed audit across 8 dimensions, a content inventory of all data to preserve, and a **6-week phased revamp plan** to deliver a modern, mobile-first, drop-in template the school can adopt.

---

## 2. Current Website Scorecard

| # | Dimension | Score | Grade | Summary |
|---|-----------|:-----:|:-----:|---------|
| 1 | **UI / Visual Design** | 2/10 | F | Late-2000s aesthetic. `<font>`, `<center>`, `<marquee>` tags. Blinking text animations. No modern design language. |
| 2 | **Mobile Responsiveness** | 1/10 | F | Fixed 960px width. No `<meta viewport>`. No media queries. Completely broken on mobile devices. |
| 3 | **Code Quality & Architecture** | 2/10 | F | XHTML 1.0 Transitional. MS Word-exported HTML with `MsoNormal` classes. Header/footer/nav duplicated across 50+ files. |
| 4 | **Security** | 2/10 | F | MooTools 1.11 (2007) with known CVEs. `crawler.js` web scraper included. Hundreds of scraped Google pages in repo. Footer links use `http://`. |
| 5 | **Accessibility (WCAG)** | 1/10 | F | `<marquee>` tags (seizure risk). Blinking text. Missing `alt` attributes. No semantic HTML. No keyboard navigation support. |
| 6 | **SEO** | 2/10 | F | Same generic `<title>` on every page. Typo in meta keywords ("Edication"). No structured data. No Open Graph tags. No sitemap. |
| 7 | **Performance** | 3/10 | D | Unoptimized JPG images (300-500KB each). No lazy loading. No minification. MooTools 64KB library loaded on every page. |
| 8 | **Content Management** | 2/10 | F | All content hardcoded in static HTML. Updating any page requires editing raw HTML. No CMS, no templates, no reuse. |

> [!CAUTION]
> **Overall Score: 1.9 / 10** — The website is critically outdated and needs a complete rebuild, not patches.

---

## 3. Detailed Findings

### 3.1 UI / Visual Design Issues

| Issue | Location | Severity |
|-------|----------|----------|
| `<marquee>` scrolling text | [index.html:129](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/index.html#L129), [index.html:138](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/index.html#L138), [index.html:172](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/index.html#L172) | 🔴 Critical |
| Blinking text animations (`.blink_red`, `.blink_blue`, `.blink_green`) | [index.html:37-74](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/index.html#L37-L74) | 🔴 Critical |
| Deprecated `<font>`, `<center>` tags throughout | All HTML files | 🔴 Critical |
| Fixed 960px container width | [style.css:150](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/css/style.css#L150) | 🔴 Critical |
| Image-based UI elements (navigation, borders, shadows) | [style.css](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/css/style.css) | 🟡 Medium |
| Table-based layouts for all content | [Admission.html:74](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/Admission.html#L74), [ContactUs.html:90](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/ContactUs.html#L90) | 🟡 Medium |
| Inconsistent "Last Update" dates across pages | index.html vs ContactUs.html | 🟡 Medium |

### 3.2 Security Concerns

| Issue | Detail | Severity |
|-------|--------|----------|
| **MooTools 1.11** (2007) | [mootools-release-1.11.js](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/js/mootools-release-1.11.js) — 64KB library with known Prototype Pollution vulnerabilities | 🔴 Critical |
| **Web Crawler Script** | [crawler.js](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/crawler.js) — A "Text and Image Crawler" script from DynamicDrive loaded on pages like [ContactUs.html:35](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/ContactUs.html#L35) | 🔴 Critical |
| **Scraped Google Content** | Repo contains 100+ scraped files: `privacy.html` (660KB), `terms.html` (611KB), `pricing.html` (1.1MB), `marketplace.html` (1.2MB), etc. — potential legal/IP risk | 🔴 Critical |
| HTTP links in footer | Footer links use `http://` instead of `https://` | 🟡 Medium |
| No Content Security Policy | No CSP headers or meta tags | 🟡 Medium |

### 3.3 Accessibility Violations (WCAG 2.2)

| WCAG Criterion | Violation | Severity |
|----------------|-----------|----------|
| 2.3.1 Three Flashes | Blinking/marquee text can trigger seizures | 🔴 Critical |
| 1.1.1 Non-text Content | Many images lack `alt` text | 🔴 Critical |
| 1.3.1 Info and Relationships | No semantic HTML5 (`<header>`, `<nav>`, `<main>`, `<footer>`) | 🔴 Critical |
| 2.1.1 Keyboard | No visible focus indicators, no skip navigation | 🟡 Medium |
| 4.1.1 Parsing | Malformed HTML (unclosed `<b>` tags, `<p>` inside `<h1>`) | 🟡 Medium |

### 3.4 SEO Deficiencies

| Issue | Detail |
|-------|--------|
| **Title Tags** | Every page uses the same title: "Air Force School - Avadi" — no page-specific titles |
| **Meta Description** | Same generic description on all pages: "Air Force School - Avadi" |
| **Meta Keywords** | Contains typo: "Edication" instead of "Education" |
| **Heading Hierarchy** | Multiple `<h1>` tags on homepage. No proper hierarchy |
| **Structured Data** | No JSON-LD, Schema.org, or Open Graph markup |
| **Sitemap** | No XML sitemap found |
| **Favicon** | Typo: `rel="shorcut icon"` instead of `rel="shortcut icon"` |

---

## 4. Content Inventory — Data to Preserve

All content below must be extracted and migrated to the new template.

### 4.1 Core Pages (50+ HTML files)

| Page | File | Content Type | Key Data |
|------|------|-------------|----------|
| **Homepage** | [index.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/index.html) | Welcome + Mission + Awards + Sidebar | Welcome text, mission statement, awards table (Best AF School 2012-2023), achievement images, sidebar links |
| **About School** | [AboutSchool.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/AboutSchool.html) | School profile | History (est. 1975), 4800+ students, 160+ staff, Principal/VP profiles, SMC, PTA details |
| **Academics** | [Academics.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/Academics.html) | Academic resources | Links to 13 curriculum docs, 6 SQP sets, question banks, CBSE publications |
| **Admission** | [Admission.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/Admission.html) | Admission info | 8-point admission procedure, age limits, general rules, fee info, payment links |
| **Infrastructure** | [Infrastructure.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/Infrastructure.html) | Facilities | Labs, library, sports, smart classrooms with photos |
| **Achievements** | [Achivements.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/Achivements.html) | Results & awards | Board results tables, student achievements, competition wins |
| **Gallery** | [Gallery.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/Gallery.html) | Photo galleries | Event-organized photo collections |
| **Contact Us** | [ContactUs.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/ContactUs.html) | Contact details | Address: Avadi, Chennai-600055. Tel: 044-26842045. Email: afschoolavadi@gmail.com. Admission contacts |
| **MPD** | [MPD.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/MPD.html) | CBSE disclosure | Affiliation data, infrastructure info, staff details, fee structure, results |
| **Results** | [results.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/results.html) | Academic results | Multi-year board exam performance data |
| **Circulars** | [circulars.html](file:///d:/Projects/AirForce Avadi/afschoolavadi.com/circulars.html) | Notices | Active circulars (57KB of content) |

### 4.2 Secondary Pages

| Category | Files | Content |
|----------|-------|---------|
| Curriculum Docs | `curriculum_2015.html` through `curriculum_2027.html` (13 files) | Year-wise curriculum details |
| Sample Papers | `SQP_CLASSX_*.html`, `SQP_CLASSXII_*.html` (6 files) | Class X & XII sample question papers |
| Question Banks | `qbclass10.html`, `qbclass12.html` | Subject-wise question banks |
| CENBOSEC | `cenbosec*.html` (6 files) | CENBOSEC notifications by semester |
| Misc | `Holidays.html`, `NEET.html`, `FitIndia.html`, `TC_Format.html`, `Carrier.html`, `Announcements.html`, `FAQ-1.html`, `annualreport.html`, `healthmanual.html`, `tenders.html`, `manual.html`, `NonViolence.html`, `hpc.html`, `skill-education.html`, `ai.html` | Various school information |

### 4.3 Media Assets

| Type | Location | Count | Notes |
|------|----------|:-----:|-------|
| Site Graphics | `images/` | ~48 files | Header, nav, footer, icons, backgrounds |
| Award Photos | `images/Awards_2026/` | ~23 photos | Award ceremony images |
| Achievement Photos | `Achivements/2026/` | 16+ images | Student achievement photos |
| Infrastructure Photos | `Infrastructure/` | Multiple | Facility images |
| Gallery Photos | `Gallery/` | Multiple dirs | Event-organized photo collections |
| Documents/PDFs | `Documents/`, root | Multiple | Admission forms, student lists |

### 4.4 External Integrations

| Service | URL | Purpose |
|---------|-----|---------|
| **ChaloSchools** | `https://chaloschools.in/web/webportal/#/sign-in` | Online fee payment portal |
| **SBI Collect** | `https://www.onlinesbi.com/sbicollect/icollecthome.htm?corpID=890789` | Online payment collection |
| **Email** | `afschoolavadi@gmail.com` | Primary school email |

---

## 5. Revamp Plan — Modern Template Architecture

> [!IMPORTANT]
> The revamp will use **plain HTML5 + Vanilla CSS + Vanilla JavaScript** (no frameworks) so the school's existing web team or any basic hosting can serve it with zero build steps. This is critical for a school website — it must be dead simple to deploy and update.

### 5.1 Template Architecture

```
afschoolavadi-revamp/
├── index.html                    # Homepage
├── about.html                    # About School
├── academics.html                # Academics Hub
├── admission.html                # Admission Info
├── infrastructure.html           # Infrastructure
├── achievements.html             # Achievements & Results
├── gallery.html                  # Photo Gallery
├── contact.html                  # Contact Us
├── mpd.html                      # Mandatory Public Disclosure
├── circulars.html                # Circulars & Notices
├── css/
│   ├── variables.css             # Design tokens (colors, spacing, fonts)
│   ├── reset.css                 # Modern CSS reset
│   ├── layout.css                # Grid/flexbox responsive layout
│   ├── components.css            # Reusable component styles
│   └── pages.css                 # Page-specific styles
├── js/
│   ├── navigation.js             # Mobile nav toggle, dropdown
│   ├── gallery.js                # Lightbox photo viewer
│   └── announcements.js          # Accessible ticker/slider
├── assets/
│   ├── images/                   # Optimized site images (WebP format)
│   ├── photos/                   # Gallery photos (organized by year/event)
│   ├── documents/                # PDFs and downloadable files
│   └── icons/                    # SVG icons
├── includes/                     # Reusable HTML partials
│   ├── header.html               # Common header (loaded via JS include)
│   ├── footer.html               # Common footer
│   └── sidebar.html              # Common sidebar
└── sitemap.xml                   # XML sitemap for SEO
```

### 5.2 Design System

| Token | Current | New |
|-------|---------|-----|
| **Primary Color** | `#0099CC` (cyan) | `#1B3A5C` (Air Force Navy Blue) |
| **Secondary Color** | `#65C80B` (green) | `#D4A843` (Gold/Brass) |
| **Accent Color** | `#CC3300` (red) | `#2E86AB` (Sky Blue) |
| **Background** | Background images (jpg) | Clean whites + subtle gradients |
| **Typography** | Arial, system fonts | Inter (Google Font) + system fallbacks |
| **Layout** | Fixed 960px + floats | CSS Grid + Flexbox, fully responsive |
| **Breakpoints** | None | 375px / 768px / 1024px / 1440px |

### 5.3 Key Template Features

| Feature | Replaces | Benefit |
|---------|----------|---------|
| **Responsive CSS Grid layout** | Fixed 960px + floats | Works on all screen sizes |
| **Reusable HTML includes** | Copy-pasted header/footer in 50+ files | Change once, applies everywhere |
| **Accessible announcement banner** | `<marquee>` + blinking text | Pausable, screen-reader friendly, WCAG compliant |
| **CSS-only image lightbox** | None (raw images) | Professional gallery viewing |
| **Modern table styling** | Raw HTML tables with inline styles | Responsive, sortable data tables |
| **WebP images** | Unoptimized JPGs (300-500KB) | 60-80% smaller file sizes |
| **JSON-LD structured data** | Nothing | Rich search results in Google |
| **SVG icons** | Image-based UI elements | Crisp at any resolution, tiny file sizes |
| **CSS custom properties** | Hardcoded colors | Easy branding updates |
| **Print stylesheet** | None | Clean printing for circulars/results |

---

## 6. Implementation Timeline — 6 Weeks

### Phase 1: Foundation & Cleanup (Week 1-2)

| Task | Deliverable | Priority |
|------|------------|----------|
| Remove all non-school files (scraped Google pages, `crawler.js`, hash-named files) | Clean repository | 🔴 P0 |
| Set up template folder structure | `afschoolavadi-revamp/` directory | 🔴 P0 |
| Create CSS design system (`variables.css`, `reset.css`, `layout.css`) | Design token file + responsive grid | 🔴 P0 |
| Build reusable header component with responsive navigation | `includes/header.html` + `navigation.js` | 🔴 P0 |
| Build reusable footer component | `includes/footer.html` | 🔴 P0 |
| Optimize and convert images to WebP | `assets/images/` | 🟡 P1 |

---

### Phase 2: Core Pages (Week 3-4)

| Task | Deliverable | Priority |
|------|------------|----------|
| Build Homepage with hero section, mission, awards, announcements | `index.html` | 🔴 P0 |
| Build About School page with staff profiles | `about.html` | 🔴 P0 |
| Build Admission page with structured info cards | `admission.html` | 🔴 P0 |
| Build Contact page with embedded map + contact cards | `contact.html` | 🔴 P0 |
| Build Academics page with organized document links | `academics.html` | 🔴 P0 |
| Build Infrastructure page with photo grid | `infrastructure.html` | 🟡 P1 |
| Build Achievements page with results tables + gallery | `achievements.html` | 🟡 P1 |

---

### Phase 3: Secondary Pages & Features (Week 5)

| Task | Deliverable | Priority |
|------|------------|----------|
| Build Gallery page with lightbox viewer | `gallery.html` + `gallery.js` | 🟡 P1 |
| Build Mandatory Public Disclosure page | `mpd.html` | 🟡 P1 |
| Build Circulars/Notices page | `circulars.html` | 🟡 P1 |
| Add accessible announcement ticker | `announcements.js` | 🟡 P1 |
| Add SEO meta tags, Open Graph, JSON-LD to all pages | All HTML files | 🟡 P1 |
| Create XML sitemap | `sitemap.xml` | 🟢 P2 |
| Add print stylesheet | `css/print.css` | 🟢 P2 |

---

### Phase 4: Testing & Handover (Week 6)

| Task | Deliverable | Priority |
|------|------------|----------|
| Lighthouse audit — target 90+ on all 4 categories | Audit report | 🔴 P0 |
| Cross-browser testing (Chrome, Firefox, Safari, Edge) | Test report | 🔴 P0 |
| Mobile device testing (iOS Safari, Android Chrome) | Test report | 🔴 P0 |
| WCAG 2.2 AA accessibility audit | Compliance report | 🟡 P1 |
| Create deployment guide for school admin | Documentation | 🟡 P1 |
| Create content update guide (how to edit pages) | Documentation | 🟡 P1 |
| Handover package (template + docs + migration guide) | Final deliverable | 🔴 P0 |

---

## 7. Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| School may not have technical staff to update HTML | High | Provide detailed content-update documentation with video walkthrough |
| Some pages have large amounts of tabular data (results, curriculum) | Medium | Build responsive table components that handle data gracefully |
| External payment links (SBI Collect, ChaloSchools) may change | Medium | Document all external URLs; make them easily configurable |
| Image assets may be low resolution | Medium | Optimize what exists; recommend high-res replacements in handover |
| `crawler.js` / scraped content may have legal implications | High | **Remove immediately** as first action in Phase 1 |

---

## 8. Success Criteria

| Metric | Current | Target |
|--------|---------|--------|
| Lighthouse Performance | ~30 | 90+ |
| Lighthouse Accessibility | ~20 | 95+ |
| Lighthouse Best Practices | ~40 | 95+ |
| Lighthouse SEO | ~30 | 95+ |
| Mobile Usable | ❌ No | ✅ Yes |
| Page Load Time (3G) | >8s | <3s |
| WCAG 2.2 AA Compliant | ❌ No | ✅ Yes |
| Pages requiring manual HTML editing for header change | 50+ | 1 (the include file) |

---

## User Review Required

> [!IMPORTANT]
> **Approval needed on the following decisions before work begins:**
>
> 1. **Tech Stack**: Plain HTML5/CSS/JS (recommended for simplicity) vs. a framework like Astro or Next.js?
> 2. **Color Scheme**: Should we keep the current cyan/green or move to the proposed Air Force Navy Blue/Gold?
> 3. **Content Scope**: Should we migrate ALL secondary pages (13 curriculum files, 6 SQP files, etc.) or consolidate them?
> 4. **Hosting**: Will the school continue using the same hosting, or is there flexibility to move to GitHub Pages, Netlify, etc.?
> 5. **Shall I begin Phase 1 immediately** (cleanup + foundation)?

## Open Questions

> [!WARNING]
> - The repository contains a **web crawler/scraper** (`crawler.js`) and hundreds of scraped Google pages (privacy policies, pricing pages, YouTube content). Was this intentional? These should be removed immediately as they pose **legal and security risks**.
> - Some pages (like `Admission.html` and `ContactUs.html`) have different "Last Update" dates and different header configurations (one says "Hello Guest!" with Login/Register, another shows the payment buttons). Which version is canonical?
