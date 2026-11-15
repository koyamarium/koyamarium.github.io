# Hiroshi Koyama — Writing, Learning, Research & Books

Personal project index: **https://koyamarium.github.io/**

The homepage is a compact public portfolio: a short author introduction and one photograph, four direct entry points (**Articles & essays**, **Learning & research**, **Books**, and **Photographs**), the public contact email. Articles lead to the public note profile, Koyamax (`https://note.com/hr_koyama`); the English entry explicitly labels those articles as Japanese. The language switch translates portfolio introductions, not the external note articles. In English the entry order is learning/research, books, photographs, then Japanese articles; Japanese retains articles first. Displayed numbers and keyboard order follow the selected language. Learning and research lead to `/research/`, which lists five published resources and web works, including the projects below:

- [Theoretical Astrophysics, Step by Step](https://koyamarium.github.io/astronomy-step-by-step/)
- [An Atlas of Numerical Methods](https://koyamarium.github.io/numerical-methods-atlas/)
- [The Art of Thermal Instability](https://koyamarium.github.io/the-art-of-thermal-instability/)
- [Optical Atlas — 光学系のギャラリー](https://koyamarium.github.io/optics/) (Japanese)

It also links to the author's researchmap (`https://researchmap.jp/read0200749`), ORCID (0009-0003-7503-4715), Google Scholar, LinkedIn, and ResearchGate profiles. Japanese and English are available using the language buttons or `?lang=ja` / `?lang=en`. The selected language follows links to the bilingual projects.


## Books

The bilingual [Books page](https://koyamarium.github.io/books/) is generated from `books/catalog.json`. The compact homepage links to it without repeating the individual covers and descriptions. Published books have a verified Amazon ASIN and a link for sampling and purchase. Forthcoming books are explicitly labeled **To be published**, without an invented release date or purchase link. The book editions listed here are Japanese; English descriptions introduce those editions.

To add a book or update availability:

1. Update its public metadata, short descriptions, and `published` / `upcoming` status in `books/catalog.json`. Set `asin` when the Amazon product page is available.
2. Add the authorized cover image under `books/covers/`.
3. Run `node scripts/build-books.mjs` from the repository root. Commit the catalog, generated `books/index.html`, and any changed cover together.
4. Check `/books/?lang=ja` and `/books/?lang=en`. Keep private production notes and submission records outside this repository.

The site hosts cover images and descriptions; reading samples are reached through the Amazon product page. Book manuscripts and EPUB files are not included.

## Homepage editing

The final `#contact` section displays the public address `koyamarium@gmail.com` and links directly to `mailto:koyamarium@gmail.com`. Japanese and English copy explain that the visitor’s email application opens. Keep the default Japanese HTML and the translations in `home.js` synchronized.

Edit `index.html`, `research/index.html`, `home.css`, and `home.js`. Both pages share the paper-and-ink style and Japanese/English text in the `copy` object. Keep default Japanese HTML in sync so the page and all destinations work without JavaScript. Add new learning resources and public web works to `/research/`; keep the homepage's four category links compact. Unreleased apps stay private.

`#portfolio` and `#contact` stay on the homepage. Existing `#writing`, `#books`, and `#photographs` anchors target their entry cards. Old `#projects` links forward to the appropriate work in `/research/` when JavaScript is enabled, with a visible category-card fallback otherwise. The books generator now writes only `/books/index.html` and never reinserts detailed teasers into the homepage. The site uses system fonts, local assets and no framework or external runtime dependencies.

```sh
python3 -m http.server 4180 --bind 127.0.0.1
```

GitHub Pages serves the `main` branch at `/` from this user-site repository. Project sites retain their existing URLs and deployment settings.

## Market Chart Atlas

The bilingual [Market Chart Atlas](https://koyamarium.github.io/market-chart-atlas/) lives in `market-chart-atlas/`, linked from the **Archives & web works** group in `/research/`. It is a static, dependency-free technical indicator gallery: moving averages (SMA / EMA), MACD, Wilder RSI, and Bollinger Bands, compared on the same 12 curated historical cases across eight US stocks and two index ETFs.

- `cases.json`: bilingual observation, question, and retrospective commentary. The observation date is a US trading-session date.
- `data.json`: finite Yahoo Finance daily OHLC/volume snapshots, with source and actual retrieval date. Each case has 130 preceding sessions, the observation session, and 20 following sessions. Prices reflect splits (including subsequent splits), not dividends.
- `app.js`, `style.css`, `index.html`: interactive charts, category/search filters, shareable case anchors, language controls, and accessible per-session slider. Future data and retrospective commentary are hidden until revealed. Initial chart: 81 sessions through observation; reveal: 101 sessions. Indicator warm-up uses preceding data.
- `indicators.mjs`: trailing SMA, fixed prior-20-session high/low reference levels, and close-to-close percentage calculation. These are not trading strategy returns.

Preview from the repository root using the server above and visit `/market-chart-atlas/?lang=ja` or `?lang=en`. No build is needed for GitHub Pages. Refresh snapshots deliberately with `python3 scripts/fetch-market-data.py` (network required). Refreshing can change historical prices when the provider applies subsequent corporate actions. Run `node --test scripts/market-atlas.test.mjs` after dataset or indicator changes. The case selection is educational and retrospective, not a statistical sample or investment recommendation.

### Technical indicator gallery

The primary entry point is now the four-method gallery. Each tile previews the same case with default parameters. Selecting a method preserves the case, observation window, and reveal state. The chart offers per-method sliders, reset, matching-date price and indicator readouts, definitions, equations, interpretation, limitations, and primary-source references. Case selection is also available directly above the chart. Japanese and English are supported throughout.

- `methods.mjs` contains bilingual method descriptions and parameter bounds. MACD is the default. URLs preserve `indicator`, active method parameters, language, and the case hash; old case links still work.
- `indicators.mjs` implements SMA-seeded EMA, MACD and signal/histogram, Wilder RSI, and population-standard-deviation Bollinger Bands. Both flat RSI gains/losses are defined as 50. EMA and RSI use finite historical initialization, so values can differ from services using longer histories.
- `chart.mjs` renders price overlays and separate aligned oscillator panes (fixed 0–100 for RSI). All displayed calculations and scales use only data visible up to the observation date unless the outcome is revealed. SMA, EMA, MACD, RSI, and band calculations use trailing data only.

Example: `/market-chart-atlas/?lang=ja&indicator=macd&fast=12&slow=26&signal=9#nvda-2023`. Indicator definitions link to Fidelity’s official indicator guide and John Bollinger’s band rules. Refreshing the historical dataset does not change the indicator definitions.

## Photographs

`photographs/` is Hiroshi Koyama’s bilingual photography portfolio, led by eight selected photographs across nature, light, architecture and an observatory. The compact homepage presents the author, one selected photograph and four direct entry points: articles, learning/research, books and photographs. The 2007–2008 American travel collection is separate at `photographs/america/`, linked from Series.

Default Japanese HTML includes every photograph, caption and expandable exposure record without JavaScript. `site.js` adds language switching and a keyboard-accessible image viewer (Escape to close, arrow keys to navigate). Images keep their original proportions, except for bounded presentation crops.

Public assets are resized, EXIF-free JPEG viewing copies. Public `catalog.json` files contain only whitelisted descriptive and camera fields; coordinates, HDD paths and complete EXIF stay outside this repository. Restrained tonal adjustments are CSS display filters. AI-generated editing attempts were rejected and are not used. Original photographs stay untouched; people-containing reserve photographs are excluded.

Preview `/photographs/?lang=ja`, `?lang=en`, and `/photographs/america/`. No build step or external dependency is needed.


## Licensing / ライセンス

Original implementation code: **MIT** ([LICENSE](LICENSE)). Text, figures, photographs, book material and data are **excluded** and follow separate terms; see [LICENSING.md](LICENSING.md) and [third-party notices](THIRD_PARTY_NOTICES.md). Public guide: https://koyamarium.github.io/rights/ .

## Research Compass / サイトを案内する

`/guide/` は、利用者の目的から公開資料を探し、質問・抜粋・出典URLを利用者自身のLLMへ手動で渡す日英の案内ページです。質問はブラウザ内だけで処理し、LLM・埋め込みAPI・APIキー・質問保存・運営者の推論従量課金はありません。対象は数値計算アトラスとThermal Instabilityの2サイトに限定し、その公開本文の抜粋と各サイトの概要を収録しています。更新方法、収録範囲、検証の限界は [guide/README.md](guide/README.md) を参照。索引と資料パックは公開後に手動更新します。
