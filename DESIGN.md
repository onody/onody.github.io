# DESIGN.md — Portfolio Site Specification

> This file is the single source of truth for the portfolio site design.
> When asking Claude to generate or update the site, pass this file as context.

---

## Philosophy

Radical minimalism. No decorations. No animations (except subtle transitions).
Every element must earn its place. If it can be removed, remove it.
Inspired by joshpuckett.me — text-first, link-first, zero noise.

---

## Layout

- Single page, single column
- Max content width: `640px`
- Centered horizontally, top-aligned
- Padding: `80px 24px` (top/bottom, left/right)
- No navbar. No footer. No sidebar.
- Language toggle button: top-right, fixed position

---

## Color

```
Background:   #0f0f0f
Text:         #e8e8e8
Muted text:   #888888
Link:         #e8e8e8  (same as text — no blue links)
Link hover:   #ffffff
Accent line:  #2a2a2a  (used for <hr> or section dividers)
Lang toggle:  background #1a1a1a, text #888, hover text #e8e8e8
```

---

## Typography

### Fonts (Google Fonts)

```
English: "Inter" — weight 400, 500
Japanese: "Noto Sans JP" — weight 400, 500
```

Both loaded via Google Fonts. `Noto Sans JP` covers all Japanese characters and
pairs naturally with `Inter` for mixed EN/JA text.

```css
font-family: 'Inter', 'Noto Sans JP', sans-serif;
```

Loading example:
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500&family=Noto+Sans+JP:wght@400;500&display=swap" rel="stylesheet">
```

### Scale

```
Body:       16px / line-height 1.75
H1 (name):  22px / font-weight 500
H2 (section): 13px / uppercase / letter-spacing 0.08em / color #888
Links:      16px / no underline by default / underline on hover
Small/meta: 13px / color #888
```

---

## Language Toggle

- Button fixed at top-right: `position: fixed; top: 24px; right: 24px;`
- Shows current inactive language: when displaying EN → button shows `JA`, and vice versa
- Default: **English**
- On click: swap all `[data-en]` / `[data-ja]` text nodes
- Button style: minimal pill — `border: 1px solid #2a2a2a`, `border-radius: 4px`, `padding: 4px 10px`, `font-size: 12px`
- No page reload. Pure JS toggle.

### Implementation pattern

```html
<span data-en="Product Manager" data-ja="プロダクトマネージャー"></span>
```

```js
let lang = 'en';
function toggleLang() {
  lang = lang === 'en' ? 'ja' : 'en';
  document.querySelectorAll('[data-en]').forEach(el => {
    el.textContent = el.dataset[lang];
  });
  document.querySelector('#lang-btn').textContent = lang === 'en' ? 'JA' : 'EN';
}
// Init
document.querySelectorAll('[data-en]').forEach(el => {
  el.textContent = el.dataset.en;
});
```

---

## Sections

Order (top to bottom):

1. **Name** — `<h1>` with name. No handle, no emoji.
2. **Bio** — 2–3 sentences. Role, company, interests. Hyperlinks to relevant places.
3. **Work** — `<h2>WORK</h2>` section with list of projects/roles
4. **Writing** *(optional)* — `<h2>WRITING</h2>` with article links
5. **Contact** — single line with links (LinkedIn, GitHub, X, email)

---

## Links

- No underline by default
- `text-decoration: underline` on hover
- `text-underline-offset: 3px`
- External links open in `_blank` + `rel="noopener"`
- Color: same as body text (`#e8e8e8`) — links should not visually scream

---

## Content

### EN

**Name:** Kohei Onodera

**Bio:**
Product Manager at Rakuten Group, building an ad-delivery platform that processes 10B+ requests/month. I work across design, engineering, and management — owning a product end-to-end is where I operate best. Native Japanese speaker; business-level English.

**Work:**

| Company | Role | Period |
|---|---|---|
| Rakuten Group | Product Manager / Engineering Manager | 2019–present |
| Supership | Product Manager / Full-Stack Engineer | 2016–2019 |
| Freelance | Engineer | 2014–2016 |
| iAct | Web Director / Engineer | 2009–2014 |
| Fubuki | Web Director | 2006–2008 |

Rakuten: Led ad-delivery product from zero to 10B req/month, achieving profitability. Managed a global engineering team of 20+.
Supership: DSP platform handling hundreds of billions of requests/month. MVP Award 2017.

**Contact:**
[LinkedIn](https://www.linkedin.com/in/kohei-onodera-172630ba/) · [X](https://x.com/koheionod) · [GitHub](https://github.com/onody) · [Email](mailto:onodera212@gmail.com)

---

### JA

**Name:** 小野寺 耕平

**Bio:**
楽天グループのプロダクトマネージャー。月間100億リクエストの広告配信プラットフォームを担当。デザイン・エンジニアリング・マネジメントを横断し、プロダクト全体を動かすのが強み。日本語ネイティブ、英語でのビジネスコミュニケーション可能。

**Work:**

| 会社 | 役割 | 期間 |
|---|---|---|
| 楽天グループ株式会社 | プロダクトマネージャー / エンジニアリングマネージャー | 2019年〜現在 |
| Supership株式会社 | プロダクトマネージャー / フルスタックエンジニア | 2016〜2019年 |
| フリーランス | エンジニア | 2014〜2016年 |
| 株式会社アイアクト | Webディレクター / エンジニア | 2009〜2014年 |
| 株式会社フブキ | Webディレクター | 2006〜2008年 |

楽天: 広告配信プロダクトを0から月間100億リクエスト・黒字化まで牽引。グローバル20名超のエンジニア組織をマネジメント。
Supership: 月間数千億リクエストのDSPプラットフォームを担当。2017年MVP賞受賞。

**Contact:**
[LinkedIn](https://www.linkedin.com/in/kohei-onodera-172630ba/) · [X](https://x.com/koheionod) · [GitHub](https://github.com/onody) · [Email](mailto:onodera212@gmail.com)

---

## What to keep out

- No profile photo (optional — add only if intentional)
- No skill bars or progress indicators
- No icons (except as text characters if needed)
- No dark/light mode toggle (dark only)
- No animations except `transition: color 0.15s ease` on links

---

## Analytics

Google Analytics 4 — Measurement ID: `G-6PRQ5XJ0NZ`

Embed in `<head>` of `index.html`:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-6PRQ5XJ0NZ"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-6PRQ5XJ0NZ');
</script>
```

---

## Update workflow

1. Edit this `DESIGN.md` with new content, color tweaks, or section changes
2. Pass to Claude: `「DESIGN.mdを元にindex.htmlを更新して」`
3. Claude generates updated HTML/CSS as a single `index.html` file
4. Push to `onody/onody.github.io` via GitHub MCP → `main` branch

---

*Last updated: 2026-05-04*