@../NATAN_LOC/CLAUDE_ECOSYSTEM_CORE.md

# IDEALORO-PREVIEW — Contesto Specifico (Oracode OS3)

> Sito Staff IdealOro — compro oro, investimento, gioielleria. Firenze.
> **Organo cliente WebAgency FlorenceEGI** — biglietto da visita per dimostrare standard ecosistema.
> Stack: Astro 5 SSG + TypeScript 5 strict + Tailwind v4 + PHP 8 minimale (form)
> URL futuro: preview.florenceegi.com | Sottodominio staging TBD
> Path: /home/fabio/IDEALORO-PREVIEW/ | Branch: main

---

## Ruolo nell'Organismo

Organo **esterno** (dominio cliente, non `.florenceegi.com`) ma sotto governance LSO completa:
- Firma OS3 su ogni file
- DOC-SYNC in `EGI-DOC/docs/idealoro-firenze/`
- Registry organi + ORGAN_INDEX
- Trigger Matrix applicata
- Pillar 6+1 rispettati

**Scopo strategico**: mostrare al mondo come lavora FlorenceEGI WebAgency.
Ogni decisione tecnica deve essere difendibile in case study pubblico.

---

## Stack

```
Frontend   → Astro 5 (SSG), zero-JS default, LCP target <1s
Styling    → Tailwind v4 + CSS tokens (palette gold luxury)
Typing     → TypeScript 5 strict, paths aliases (~/*, @components/*)
Content    → Content Collections (FAQ + Blog) IT + EN
i18n       → Astro built-in (it default, en prefix /en/)
Build out  → Static files (dist/) → deploy anywhere (S3+CF, nginx, Vercel)
Form       → public/mail.php (PHP 8, SMTP + CSRF + honeypot, 0 dipendenze)
Icons      → Inline SVG (no icon font — speed first)
Fonts      → Cormorant Garamond (serif luxury) + Inter (sans body)
```

---

## Architettura sezioni (anti-ridondanza vs sito attuale)

```
Home            → hero "DIAMO VALORE" + trust signals + FAQ rich
Compro Oro      → oro+argento+oggetti unificati (era 2 sezioni)
Investimento    → Sterline+Lingotti+digitale unificati (era 3 sezioni)
Gioielleria     → custom + upcycling
Quotazioni      → tabella live + archivio
Perizie         → stime, lasciti ereditari
FAQ             → AEO core (FAQPage JSON-LD)
Blog            → content freshness
Chi siamo       → OAM + trust + FlorenceEGI signature discreta
Contatti        → form + WhatsApp + mappa + orari + tel cliccabile
```

Eliminato: duplicazione card, sezione "NFT-EGI" standalone.

---

## SEO / AEO / GEO (strategia E=Everywhere)

**Tutte le pagine DEVONO includere:**
1. `<title>` e `<meta description>` distintivi (no template)
2. OG tags (og:image 1200×630)
3. Canonical + hreflang IT/EN
4. Schema.org JSON-LD appropriato:
   - Home: LocalBusiness + JewelryStore + WebSite + BreadcrumbList
   - FAQ: FAQPage
   - Blog: BlogPosting + Person (author)
   - Quotazioni: Dataset (prezzi live)
5. Answer-first: prima frase sotto h1 risponde domanda primaria in ≤40 parole
6. Sezioni stand-alone (AI estrae chunks)
7. Factual density > keyword density
8. Tabelle dati (AI preferisce strutturato)

---

## File critici

```
src/layouts/Base.astro            → Meta + schema.org JSON-LD centralizzato
src/lib/schema.ts                 → Helpers typed LocalBusiness, FAQPage, etc.
src/i18n/{it,en}.json             → Chiavi atomic (mai interpolazione chiave)
src/content/faq/                  → MDX con frontmatter {q, a_it, a_en, order}
src/components/*.astro            → Componenti puri, no client JS salvo dove serve
public/mail.php                   → Form backend standalone
scripts/scrape-assets.mjs         → Download immagini da preview.florenceegi.com
docs/audit-gialloorofirenze-it.md → Report audit criticita (→ PDF via pandoc)
```

---

## P0 Specifici IDEALORO-PREVIEW

| # | Regola | Enforcement |
|---|--------|-------------|
| P0-100 | **Zero JS runtime salvo necessita** | Astro `client:load` solo su componenti che richiedono interattivita reale. Default `<script>` inline minimi |
| P0-101 | **Ogni pagina ha schema.org** | Base layout enforce JSON-LD. No page senza struttura |
| P0-102 | **i18n atomic** | `t('home.hero.title')` mai `t('home.hero', {name})` |
| P0-103 | **Lighthouse gate** | Build deve raggiungere Performance 95+, SEO 100, Accessibility 100 |
| P0-104 | **Asset via Astro Image** | Mai `<img>` raw — sempre `<Image />` per WebP+sizes auto |
| P0-105 | **AI-oriented copy** | Prima frase sotto h1 = risposta 40 parole. Tabelle per dati. Dati fattuali verificabili |

---

## Comandi

```bash
npm install                          # install deps
npm run dev                          # localhost:4330
npm run build                        # static build dist/
npm run preview                      # serve dist/
npm run scrape                       # download assets da preview.florenceegi.com
npm run audit:pdf                    # genera PDF audit (richiede pandoc + xelatex)
```

---

## Regole operative

1. **Sempre branch `main`** — no feature branch (team = 1 dev)
2. **Commit atomici** con tag standard: `[FEAT]`, `[FIX]`, `[CONFIG]`, `[I18N]`, `[SEO]`, `[DOC]`, `[CHORE]`
3. **Firma OS3 obbligatoria** su ogni file (Astro/TS/PHP)
4. **Immagini**: max 200KB post-ottimizzazione, WebP+AVIF
5. **Lingua default route**: IT (no prefix). EN su `/en/`
6. **Revisione Fabio prima di deploy staging**

---

## SSOT Documentazione

Path: `/home/fabio/EGI-DOC/docs/idealoro-firenze/`
- `00_OVERVIEW.md` — identita organo + perimetro
- `01_STACK_E_ARCHITETTURA.md` — scelte tecniche + rationale
- `02_SEO_AEO_GEO_STRATEGY.md` — playbook ottimizzazione
- `03_DEPLOY.md` — pipeline staging + prod (pending)

---

*IDEALORO-PREVIEW — Organo cliente WebAgency FlorenceEGI — v1.0.0 (2026-04-17)*
