# Mycota chapter — Quarto manuscript project

*Phenotypic and Genotypic Adaptation of Fungi to a Warming and Destabilized Planet*
(Kontoyiannis & Lewis). Converted from `source/chapter_draft.docx` on 2026-09-14.

## Layout

| File | Purpose |
|---|---|
| `_quarto.yml` | Project config (`type: manuscript`); HTML + Word outputs, Springer author-date CSL, numbered sections to depth 3 |
| `index.qmd` | The chapter. YAML front matter carries title, authors, affiliations, corresponding author, keywords and abstract |
| `references.bib` | 119 entries: 117 built from the DOIs in the Word reference list via Crossref, plus 2 placeholders (`wurster2020`, `money2024`) |
| `springer-basic-author-date.csl` | Springer Basic (author-date) style from the CSL repository |
| `styles.css` | Highlights `[VERIFY]` markers in the HTML output |
| `figures/fig1.png … fig5.png` | The five figures from the Word file (2055 px wide, 300 dpi) — already meet Mycota's separate-file requirement |
| `index_terms.txt` | The index-term list from the end of the draft (Mycota indexing is done in Word, so this stays outside the manuscript) |
| `source/` | Original Word draft and the Mycota author instructions |
| `_manuscript/` | Rendered output (`index.html`, `index.docx`) — regenerate with `quarto render` |

## Rendering

```
quarto render            # HTML + docx into _manuscript/
quarto preview           # live HTML preview
quarto render --to docx  # Word only
```

Requires Quarto ≥ 1.4 (tested with 1.7.32). No R/Python execution is needed; everything is static.

## What was converted

- **Headings**: manual numbers stripped; Quarto numbers sections (`number-sections: true`, depth 3, matching Mycota's three-level limit). Every heading has an id (`#sec-2-4` etc.) so "Section 2.4" in the text is now `@sec-2-4` and renders as "Sect. 2.4".
  The draft had Section 2's top heading at level 2 by mistake; it is now level 1.
- **Citations**: all 300-odd in-text author–year citations became `[@key]` / `@key` citations. Keys are `firstauthorsurname+year` (`hawksworth2017`), with `smithcasadevall2022` vs `smith2022` to separate the two Smith 2022 papers. Every cited key resolves to a bib entry; every bib entry except `money2024` is cited.
- **Reference years**: for 6 records the Crossref year differed from the year in the Word reference list (online-first vs. issue year). The Word list's year was kept, since the draft says those were corrected deliberately: `baker2022, brown2018, chamilos2006, lockhart2017, morano2011, nicholls2010`. See `year_overrides.log`.
- **Tables 1–3**: converted to pipe tables with captions and labels (`@tbl-mechanisms`, `@tbl-claims`, `@tbl-disasters`). Citations inside the "Key references" column are live citations.
- **Figures**: inserted after the paragraph that first cites each one, with labels `@fig-framework`, `@fig-thermal`, `@fig-mechanisms`, `@fig-timeline`, `@fig-disasters`.
- **Section 10.4**: the ten priority questions were split across 20 broken list items in the Word file; they are re-joined into 10.
- The two `[VERIFY]` references (Wurster et al. 2020; Money 2024) are placeholder bib entries so the document renders; their `note` fields say what is missing.

## Things for the authors to check (search `VERIFY` and `TO CONFIRM` in index.qmd)

1. **Figure captions** — none existed in the Word draft. All five were drafted from the figure content and are marked `[CAPTION TO CONFIRM]`. Fig. 4B needs the bibliographic database and query stated. Fig. 5 duplicates Table 3; consider keeping one.
2. **Fig. 3 was never cited** in the draft. It is placed at the top of Section 3 inside a callout note; add a cross-reference (`@fig-mechanisms`) where it belongs and delete the callout.
3. **Ten `[VERIFY]` markers** carried over from the draft (unpublished/presented data; Wurster 2020; Money 2024). They render highlighted in HTML and bold in Word; delete the `[**VERIFY** …]{.verify}` spans once resolved.
4. **Corresponding-author e-mail**: the draft had `dkontoyi@mdandserson.org` (typo); corrected to `mdanderson.org` in the YAML — please confirm.
5. **ORCIDs** are not in the YAML; add `orcid:` under each author if wanted.
6. **Word output for submission**: Springer's production team reformats anyway, but if you want house styles, put a template at `springer-reference.docx` and uncomment `reference-doc` in `_quarto.yml`. Index terms still have to be marked in Word after rendering (Mycota uses Word's index function).
7. **Acknowledgements** is an empty unnumbered section at the end of the body.
